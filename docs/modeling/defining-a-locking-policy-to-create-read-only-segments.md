---
title: 定义锁定策略以创建只读段
description: 了解如何为程序定义一个策略，以便锁定 DSL (模型的部分或所有特定于域) ，以便可以读取但不能更改它。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: e445e59fc91fc97cf85b28ee339c604c1e4c6261333d9e15ac66d746a0422aa0
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121316872"
---
# <a name="defining-a-locking-policy-to-create-read-only-segments"></a>定义锁定策略以创建只读段
Visual Studio 可视化和建模 SDK 的不可变 API 允许程序锁定部分或所有特定于域的语言 (DSL) 模型，以便可以读取但不能更改该模型。 例如，可以使用此只读选项，以便用户可以要求同事批注和查看 DSL 模型，但不允许他们更改原始模型。

 此外，作为 DSL 的作者，可以定义锁定 *策略。* 锁定策略定义允许、不允许或强制锁定。 例如，发布 DSL 时，可以鼓励第三方开发人员使用新命令扩展它。 但是，也可使用锁定策略来防止它们更改模型指定部分的只读状态。

> [!NOTE]
> 可以通过使用反射来规避锁定策略。 它为第三方开发人员提供了明确的边界，但不提供强大的安全性。

 有关详细信息和示例，请参阅 Visual Studio[可视化和建模 SDK](https://code.msdn.microsoft.com/Visualization-and-Modeling-313535db)网站。

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="setting-and-getting-locks"></a>设置和获取锁
 可以在存储、分区或单个元素上设置锁。 例如，此语句将阻止删除模型元素，还会阻止更改其属性：

```csharp
using Microsoft.VisualStudio.Modeling.Immutability; ...
element.SetLocks(Locks.Delete | Locks.Property);
```

 其他锁值可用于防止角色中关系、元素创建、分区之间的移动和重新排序链接的更改。

 锁同时应用于用户操作和程序代码。 如果程序代码尝试进行更改， `InvalidOperationException` 将引发 。 在撤消或重做操作中将忽略锁。

 可以使用 发现元素在给定集内是否具有任何锁，并且可以使用 获取元素的当前 `IsLocked(Locks)` 锁集 `GetLocks()` 。

 无需使用事务即可设置锁。 锁数据库不是存储的一部分。 如果设置锁以响应存储中值的更改（例如在 OnValueChanged 中）时，应允许属于撤消操作一部分的更改。

 这些方法是命名空间中定义的扩展 <xref:Microsoft.VisualStudio.Modeling.Immutability> 方法。

### <a name="locks-on-partitions-and-stores"></a>分区和存储上的锁
 锁还可以应用于分区和存储。 在分区上设置的锁适用于分区中的所有元素。 因此，例如，以下语句将阻止删除分区中所有元素，而不管它们自己的锁状态如何。 不过，仍可在单个元素 `Locks.Property` 上设置其他锁（如 ）：

```csharp
partition.SetLocks(Locks.Delete);
```

 在 Store 上设置的锁将应用于其所有元素，而不管该锁在分区和元素上的设置如何。

### <a name="using-locks"></a>使用锁
 可以使用锁来实现方案，如以下示例所示：

- 不允许更改所有元素和关系（表示注释的元素和关系除外）。 这允许用户在不更改模型的情况下对模型进行批注。

- 不允许更改默认分区，但允许更改关系图分区。 用户可以重新排列关系图，但不能更改基础模型。

- 不允许对 Store 进行更改，在单独的数据库中注册的一组用户除外。 对于其他用户，关系图和模型是只读的。

- 如果关系图的布尔属性设置为 true，则不允许对模型进行更改。 提供菜单命令以更改该属性。 这有助于确保用户不会意外进行更改。

- 不允许添加和删除特定类的元素和关系，但允许属性更改。 这为用户提供了一个固定窗体，用户可在此窗体中填充属性。

## <a name="lock-values"></a>锁定值
 可以在存储、分区或单个 ModelElement 上设置锁。 Locks 是 `Flags` 一个枚举：可以使用"&#124;"合并其值。

- ModelElement 的锁始终包括其分区的锁。

- 分区的锁始终包括存储的锁。

  不能在分区或存储上设置锁，同时禁用单个元素上的锁。

|值|如果 为 `IsLocked(Value)` true，则意味着|
|-|-|
|无|无限制。|
|属性|无法更改元素的域属性。 这不适用于由关系中域类的角色生成的属性。|
|添加|无法在分区或存储中新建元素和链接。<br /><br /> 不适用于 `ModelElement` 。|
|移动|如果 为 true，则不能在分区之间 `element.IsLocked(Move)` 移动元素;如果 `targetPartition.IsLocked(Move)` 为 true，则不能移动元素。|
|删除|如果在元素本身上设置此锁，或者对要传播删除的任何元素（如嵌入的元素和形状）设置此锁，则不能删除元素。<br /><br /> 可以使用 `element.CanDelete()` 来确定是否可以删除元素。|
|排序|无法更改角色播放器上的链接顺序。|
|RolePlayer|无法更改此元素中源的链接集。 例如，不能在此元素下嵌入新元素。 这不会影响此元素作为目标的链接。<br /><br /> 如果此元素是链接，则其源和目标不受影响。|
|全部|其他值的位或。|

## <a name="locking-policies"></a>锁定策略
 作为 DSL 的作者，可以定义锁定 *策略*。 锁定策略会调整 SetLocks () ，以便可以阻止设置特定锁或强制必须设置特定锁。 通常，你将使用锁定策略来阻止用户或开发人员意外逆逆 DSL 的预期使用，其方式与声明变量 的方式相同 `private` 。

 还可使用锁定策略对依赖于元素类型的所有元素设置锁。 这是因为在首次从文件创建或反反化元素时，始终 `SetLocks(Locks.None)` 调用 。

 但是，不能在元素的生命周期内使用策略来改变元素上的锁。 若要实现此效果，应该使用对 的调用 `SetLocks()` 。

 若要定义锁定策略，必须：

- 创建用于实现 <xref:Microsoft.VisualStudio.Modeling.Immutability.ILockingPolicy> 的类。

- 将此类添加到通过 DSL 的 DocData 提供的服务。

### <a name="to-define-a-locking-policy"></a>定义锁定策略
 <xref:Microsoft.VisualStudio.Modeling.Immutability.ILockingPolicy> 具有以下定义：

```csharp
public interface ILockingPolicy
{
  Locks RefineLocks(ModelElement element, Locks proposedLocks);
  Locks RefineLocks(Partition partition, Locks proposedLocks);
  Locks RefineLocks(Store store, Locks proposedLocks);
}
```

 对 Store、Partition 或 ModelElement 调用 时 `SetLocks()` ，将调用这些方法。 在每个方法中，都提供了一组建议的锁。 可以返回建议集，也可以添加和减去锁。

 例如：

```csharp
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Immutability;
namespace Company.YourDsl.DslPackage // Change
{
  public class MyLockingPolicy : ILockingPolicy
  {
    /// <summary>
    /// Moderate SetLocks(this ModelElement target, Locks locks)
    /// </summary>
    /// <param name="element">target</param>
    /// <param name="proposedLocks">locks</param>
    /// <returns></returns>
    public Locks RefineLocks(ModelElement element, Locks proposedLocks)
    {
      // In my policy, users can never delete an element,
      // and other developers cannot easily change that:
      return proposedLocks | Locks.Delete);
    }
    public Locks RefineLocks(Store store, Locks proposedLocks)
    {
      // Only one user can change this model:
      return Environment.UserName == "aUser"
           ? proposedLocks : Locks.All;
    }
```

 确保即使其他代码调用，用户也可以始终删除元素 `SetLocks(Lock.Delete):`

 `return proposedLocks & (Locks.All ^ Locks.Delete);`

 禁止更改 MyClass 中每个元素的所有属性：

 `return element is MyClass ? (proposedLocks | Locks.Property) : proposedLocks;`

### <a name="to-make-your-policy-available-as-a-service"></a>使策略作为服务可用
 在 `DslPackage` 项目中，添加一个新文件，其中包含类似于以下示例的代码：

```csharp
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Immutability;
namespace Company.YourDsl.DslPackage // Change
{
  // Override the DocData GetService() for this DSL.
  internal partial class YourDslDocData // Change
  {
    /// <summary>
    /// Custom locking policy cache.
    /// </summary>
    private ILockingPolicy myLockingPolicy = null;

    /// <summary>
    /// Called when a service is requested.
    /// </summary>
    /// <param name="serviceType">Service requested</param>
    /// <returns>Service implementation</returns>
    public override object GetService(System.Type serviceType)
    {
      if (serviceType == typeof(SLockingPolicy)
       || serviceType == typeof(ILockingPolicy))
      {
        if (myLockingPolicy == null)
        {
          myLockingPolicy = new MyLockingPolicy();
        }
        return myLockingPolicy;
      }
      // Request is for some other service.
      return base.GetService(serviceType);
    }
}
```

---
title: 定义锁定策略以创建只读段
description: 了解如何为程序定义策略，以部分或完全锁定特定于域的语言 (DSL) 模型，使其可供读取但不能更改。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: c10fc92d222ebda2ad7e81549c91413d95825f2a
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126671877"
---
# <a name="defining-a-locking-policy-to-create-read-only-segments"></a>定义锁定策略以创建只读段
Visual Studio 可视化和建模 SDK 的不可变性 API 允许程序部分或全部锁定特定于域的语言 (DSL) 模型，使其可供读取但不能更改。 使用此只读选项的一个例子是，让用户能够要求同事批注和审阅 DSL 模型，但禁止同事更改原始模型。

 此外，作为 DSL 的作者，你可以定义锁定策略。 锁定策略定义允许、不允许或强制的锁。 例如，当你发布 DSL 时，可以鼓励第三方开发人员使用新命令来扩展它。 但也可以使用锁定策略，来防止他们更改模型指定部分的只读状态。

> [!NOTE]
> 可以使用反射来规避锁定策略。 它为第三方开发人员提供清晰的边界，但不提供强大的安全性。

 有关详细信息和示例，请参阅 Visual Studio [可视化和建模 SDK](https://code.msdn.microsoft.com/Visualization-and-Modeling-313535db) 网站。

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="setting-and-getting-locks"></a>设置和获取锁
 可以在存储、分区或单个元素上设置锁。 例如，此语句将阻止删除模型元素，并且还会阻止更改其属性：

```csharp
using Microsoft.VisualStudio.Modeling.Immutability; ...
element.SetLocks(Locks.Delete | Locks.Property);
```

 可使用其他锁值防止更关系、创建元素、在分区之间移动以及对链接进行重新排序。

 锁适用于用户操作和程序代码。 如果程序代码尝试进行更改，将引发 `InvalidOperationException`。 “撤消”或“恢复”操作中会忽略锁。

 可以使用 `IsLocked(Locks)` 来发现某个元素是否具有给定集合中的任何锁，还可以使用 `GetLocks()` 获取元素上的当前锁集合。

 无需使用事务即可设置锁定。 锁定数据库不属于存储。 如果设置锁定来响应存储中某个值的更改（例如 OnValueChanged 中），则应允许属于“撤消”操作的更改。

 这些方法是在 <xref:Microsoft.VisualStudio.Modeling.Immutability> 命名空间中定义的扩展方法。

### <a name="locks-on-partitions-and-stores"></a>分区和存储上的锁
 也可以将锁应用于分区和存储。 在分区上设置的锁适用于该分区中的所有元素。 因此，比如下面的语句就将阻止删除分区中的所有元素，而不考虑它们自己的锁的状态。 尽管如此，仍可在单个元素上设置其他锁（例如 `Locks.Property`）：

```csharp
partition.SetLocks(Locks.Delete);
```

 在存储区设置的锁适用于其所有元素，不考虑该锁在分区和元素上的设置。

### <a name="using-locks"></a>使用锁
 可以使用锁来实现各种方案，如以下示例：

- 禁止对除表示注释的元素和关系以外的所有元素和关系进行更改。 这样，用户便可以在不更改模型的情况下对其进行批注。

- 禁止更改默认分区，但允许更改关系图分区。 用户可以重新排列关系图，但不能更改基础模型。

- 禁止对存储进行更改，但在单独的数据库中注册的一组用户除外。 对于其他用户，关系图和模型是只读的。

- 如果关系图有一个布尔属性设置为 true，则不允许对模型进行更改。 提供菜单命令以更改该属性。 这有助于确保用户不会无意中进行更改。

- 禁止添加和删除特定类的元素和关系，但允许属性更改。 这为用户提供了一个固定的窗体，用户可以在其中填充属性。

## <a name="lock-values"></a>锁定值
 可以对存储、分区或单个 ModelElement 设置锁。 锁是 `Flags` 枚举：可以使用“&#124;”合并其值。

- ModelElement 的锁始终包含其分区的锁。

- 分区的锁始终包含存储的锁。

  不能对分区或存储设置锁而同时禁用单个元素上的锁。

|值|这意味着如果 `IsLocked(Value)` 为 true|
|-|-|
|无|无限制。|
|属性|无法更改元素的域属性。 这不适用于由关系中的域类的角色生成的属性。|
|添加|不能在分区或存储中创建新的元素和链接。<br /><br /> 不适用于 `ModelElement`。|
|移动|如果 `element.IsLocked(Move)` 为 true，或 `targetPartition.IsLocked(Move)` 为 true，则不能在分区之间移动元素。|
|删除|如果此锁是在元素本身上设置的，或者是在删除操作将传播到的任何元素（如嵌入的元素和形状）上设置的，则不能删除元素。<br /><br /> 可以使用 `element.CanDelete()` 来发现是否可以删除某个元素。|
|重新排序|不能更改 roleplayer 处的链接排序。|
|RolePlayer|不能更改来源于此元素的链接集合。 例如，不能在此元素下嵌入新元素。 这不会影响以此元素作为目标的链接。<br /><br /> 如果此元素是链接，则其源和目标不受影响。|
|全部|其他值的按位或。|

## <a name="locking-policies"></a>锁定策略
 作为 DSL 的作者，你可以定义锁定策略。 锁定策略协调 SetLocks() 的操作，让你可以防止设置特定的锁或强制规定必须设置特定的锁。 通常，你会使用锁定策略来防止用户或开发人员意外违规使用 DSL，这与将变量声明为 `private` 的方式相同。

 你还可以使用锁定策略在依赖于该元素类型的所有元素上设置锁。 这是因为第一次从文件中创建或反序列化某个元素时，始终会调用 `SetLocks(Locks.None)`。

 但是，不能使用策略在某个元素的生存期内改变其上的锁。 若要实现这种效果，应使用对的 `SetLocks()` 调用。

 若要定义锁定策略，必须执行以下操作：

- 创建用于实现 <xref:Microsoft.VisualStudio.Modeling.Immutability.ILockingPolicy> 的类。

- 将此类添加到可通过 DSL 的 DocData 使用的服务。

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

 对存储、分区或 ModelElement 上的 `SetLocks()` 进行调用时，将调用这些方法。 每种方法中都提供一组建议的锁。 可以返回建议的一组锁，也可以加减锁。

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

 若要确保用户始终可以删除元素，即使其他代码调用 `SetLocks(Lock.Delete):`

 `return proposedLocks & (Locks.All ^ Locks.Delete);`

 禁止在 MyClass 的每个元素的所有属性中进行更改：

 `return element is MyClass ? (proposedLocks | Locks.Property) : proposedLocks;`

### <a name="to-make-your-policy-available-as-a-service"></a>将策略作为服务提供
 在 `DslPackage` 项目中，添加包含类似于以下示例的代码的新文件：

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

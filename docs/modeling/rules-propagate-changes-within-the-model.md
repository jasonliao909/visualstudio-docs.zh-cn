---
title: 规则在模型内部传播更改
description: 了解如何创建存储规则，以在可视化和建模 SDK (VMSDK) 中的元素之间传播更改。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, programming domain models
- Domain-Specific Language, rules
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: f6434d4427371a0e2bd39da7c9979b6c29d521e6
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126663904"
---
# <a name="rules-propagate-changes-within-the-model"></a>规则在模型内部传播更改
可以创建存储规则，以在可视化和建模 SDK (VMSDK) 中的元素之间传播更改。 当存储区中任何元素发生更改时，通常会计划在提交最外层的事务时执行规则。 不同类型的事件（例如添加元素或删除元素）有不同类型的规则。 可以将规则附加到特定类型的元素、形状或关系图。 许多内置功能由规则定义：例如，规则可确保在模型发生更改时更新关系图。 可以通过添加自己的规则来自定义特定于域的语言。

 存储规则特别适用于在存储内部传播更改，即模型元素、关系、形状或连接符及其域属性的更改。 当用户调用 Undo 或 Redo 命令时，规则不会运行。 相反，事务管理器确保存储内容还原到正确的状态。 如果要将更改传播到存储外部的资源，请使用“存储事件”。 有关详细信息，请参阅[事件处理程序在模型外部传播更改](../modeling/event-handlers-propagate-changes-outside-the-model.md)。

 例如，假设要指定每当用户（或代码）创建类型为 ExampleDomainClass 的新元素时，在模型的另一部分创建另一种类型的其他元素。 可以编写 AddRule 并将其与 ExampleDomainClass 关联。 你将在规则中编写代码以创建额外元素。

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using Microsoft.VisualStudio.Modeling;

namespace ExampleNamespace
{
 // Attribute associates the rule with a domain class:
 [RuleOn(typeof(ExampleDomainClass), FireTime=TimeToFire.TopLevelCommit)]
 // The rule is a class derived from one of the abstract rules:
 class MyAddRule : AddRule
 {
  // Override the abstract method:
  public override void ElementAdded(ElementAddedEventArgs e)
  {
    base.ElementAdded(e);
    ExampleDomainClass element = e.ModelElement;
    Store store = element.Store;
    // Ignore this call if we're currently loading a model:
    if (store.TransactionManager.CurrentTransaction.IsSerializing)
       return;

    // Code here propagates change as required - for example:
      AnotherDomainClass echo = new AnotherDomainClass(element.Partition);
      echo.Name = element.Name;
      echo.Parent = element.Parent;
    }
  }
 // The rule must be registered:
 public partial class ExampleDomainModel
 {
   protected override Type[] GetCustomDomainModelTypes()
   {
     List<Type> types = new List<Type>(base.GetCustomDomainModelTypes());
     types.Add(typeof(MyAddRule));
     // If you add more rules, list them here.
     return types.ToArray();
   }
 }
}
```

> [!NOTE]
> 规则的代码仅应更改存储中元素的状态；即，规则应仅更改模型元素、关系、形状、连接符、关系图或属性。 如果要将更改传播到存储外部的资源，请定义“存储事件”。 有关详细信息，请参阅[事件处理程序在模型外部传播更改](../modeling/event-handlers-propagate-changes-outside-the-model.md)。

### <a name="to-define-a-rule"></a>定义规则

1. 将规则定义为以 `RuleOn` 属性为前缀的类。 该属性将规则与域类、关系或关系图元素之一关联。 规则将应用于此类的每一个实例，其中实例可能是抽象的。

2. 通过将规则添加到域模型类中的 `GetCustomDomainModelTypes()` 返回的集来注册规则。

3. 从抽象规则类之一派生规则类，并编写执行方法的代码。

   以下各部分更详细地说明了这些步骤。

### <a name="to-define-a-rule-on-a-domain-class"></a>在域类上定义规则

- 在自定义代码文件中，定义一个类，并添加 <xref:Microsoft.VisualStudio.Modeling.RuleOnAttribute> 属性作为其前缀：

    ```csharp
    [RuleOn(typeof(ExampleElement),
         // Usual value - but required, because it is not the default:
         FireTime = TimeToFire.TopLevelCommit)]
    class MyRule ...

    ```

- 第一个参数中的使用者类型可以是域类、域关系、形状、连接符或关系图。 通常，将规则应用于域类和关系。

     `FireTime` 通常为 `TopLevelCommit`。 这可确保仅在对事务进行所有主要更改后再执行规则。 替代项为“内联”（其将在更改后立即执行规则）和 LocalCommit（其在当前事务（可能不在最外层）处理结束时执行规则）。 还可以设置规则的优先级，以影响规则在队列中的顺序，但这是实现你所需结果的不可靠方法。

- 可以将抽象类指定为使用者类型。

- 该规则适用于使用者类的所有实例。

- `FireTime` 的默认值为 TimeToFire.TopLevelCommit。 这将导致在提交最外层的事务时执行规则。 另一种替代方法是 TimeToFire.Inline。 这会导致规则在触发事件后立即执行。

### <a name="to-register-the-rule"></a>注册规则

- 将规则类添加到域模型中的 `GetCustomDomainModelTypes` 返回的类型列表：

    ```csharp
    public partial class ExampleDomainModel
     {
       protected override Type[] GetCustomDomainModelTypes()
       {
         List<Type> types = new List<Type>(base.GetCustomDomainModelTypes());
         types.Add(typeof(MyAddRule));
         // If you add more rules, list them here.
         return types.ToArray();
       }
     }

    ```

- 如果不确定域模型类的名称，请查看文件 Dsl\GeneratedCode\DomainModel.cs

- 在 DSL 项目中的自定义代码文件中编写此代码。

### <a name="to-write-the-code-of-the-rule"></a>编写规则的代码

- 从以下基类之一派生规则类：

  | 基类 | 触发器 |
  |-|-|
  | <xref:Microsoft.VisualStudio.Modeling.AddRule> | 添加了元素、链接或形状。<br /><br /> 使用它来检测新关系以及新元素。 |
  | <xref:Microsoft.VisualStudio.Modeling.ChangeRule> | 域属性值已更改。 方法参数提供新、旧值。<br /><br /> 对于形状，如果移动了形状，则当内置 `AbsoluteBounds` 属性更改时，将触发此规则。<br /><br /> 在许多情况下，在属性处理程序中替代 `OnValueChanged` 或 `OnValueChanging` 是更方便的方法。 这些方法在更改之前和之后立即调用。 相比之下，规则通常在事务结束时运行。 有关详细信息，请参阅[域属性值更改处理程序](../modeling/domain-property-value-change-handlers.md)。 **注意：** 创建或删除链接时不会触发此规则。 而是为域关系编写 `AddRule` 和 `DeleteRule`。 |
  | <xref:Microsoft.VisualStudio.Modeling.DeletingRule> | 在即将删除元素或链接时触发。 在事务结束之前，属性 ModelElement.IsDeleting 为 true。 |
  | <xref:Microsoft.VisualStudio.Modeling.DeleteRule> | 删除元素或链接时执行。 此规则将在执行所有其他规则（包括 DeletingRules）后执行。 ModelElement.IsDeleting 为 false，ModelElement.IsDeleted 为 true。 为了允许后续的撤消操作，实际上不会从内存中删除元素，而是从 Store.ElementDirectory 中删除该元素。 |
  | <xref:Microsoft.VisualStudio.Modeling.MoveRule> | 元素从一个存储分区移到另一个存储分区。<br /><br /> （请注意，此操作与形状的图形位置不相关。） |
  | <xref:Microsoft.VisualStudio.Modeling.RolePlayerChangeRule> | 此规则仅适用于域关系。 如果将模型元素显式分配给链接的任一端，则触发此规则。 |
  | <xref:Microsoft.VisualStudio.Modeling.RolePlayerPositionChangeRule> | 在链接上使用 MoveBefore 或 MoveToIndex 方法更改元素的链接排序时触发。 |
  | <xref:Microsoft.VisualStudio.Modeling.TransactionBeginningRule> | 创建事务时执行。 |
  | <xref:Microsoft.VisualStudio.Modeling.TransactionCommittingRule> | 事务即将提交时执行。 |
  | <xref:Microsoft.VisualStudio.Modeling.TransactionRollingBackRule> | 事务即将回滚时执行。 |

- 每个类都有一个替代的方法。 在类中键入 `override` 以发现它。 此方法的参数标识要更改的元素。

  请注意有关规则的以下几点：

1. 事务中的一组更改可能会触发许多规则。 通常，在提交最外层的事务时执行规则。 它们以未指定的顺序执行。

2. 规则始终在事务内执行。 因此，不需要创建新事务来进行更改。

3. 回滚事务或执行撤消或重做操作时，不会执行规则。 这些操作将存储的所有内容重置为以前的状态。 因此，如果规则更改存储外部任何内容的状态，则可能不会与存储内容保持同步。 若要更新存储外部的状态，最好使用事件。 有关详细信息，请参阅[事件处理程序在模型外部传播更改](../modeling/event-handlers-propagate-changes-outside-the-model.md)。

4. 从文件加载模型时，将执行某些规则。 若要确定加载或保存是否正在进行，请使用 `store.TransactionManager.CurrentTransaction.IsSerializing`。

5. 如果规则的代码创建了更多规则触发器，这些触发器将添加到触发列表的末尾，并且将在事务完成之前执行。 DeletedRules 在所有其他规则之后执行。 一个规则可以在事务中运行多次，每个更改一次。

6. 若要向/从规则传递信息，可以在 `TransactionContext` 中存储信息。 这只是在事务期间维护的字典。 事务结束时，将释放该事务。 每个规则中的事件参数都提供对它的访问。 请记住，规则不按可预测的顺序执行。

7. 在考虑其他替代方法后，使用规则。 例如，如果要在值更改时更新属性，请考虑使用计算属性。 如果要约束形状的大小或位置，请使用 `BoundsRule`。 如果要响应属性值中的更改，请向属性添加 `OnValueChanged` 处理程序。 有关详细信息，请参阅[响应和传播更改](../modeling/responding-to-and-propagating-changes.md)。

## <a name="example"></a>示例
 以下示例在实例化域关系以链接两个元素时更新属性。 此规则不仅将在用户在关系图上创建链接时触发，而且当程序代码创建链接时也会触发。

 若要测试此示例，请使用任务流解决方案模板创建 DSL，并将以下代码插入 Dsl 项目中的文件中。 生成并运行解决方案，并打开调试项目中的示例文件。 在注释形状和流元素之间绘制注释链接。 注释中的文本将更改，以报告已连接到的最新元素。

 在实践中，通常会为每个 AddRule 编写一个 DeleteRule。

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.VisualStudio.Modeling;

namespace Company.TaskRuleExample
{

  [RuleOn(typeof(CommentReferencesSubjects))]
  public class RoleRule : AddRule
  {

    public override void ElementAdded(ElementAddedEventArgs e)
    {
      base.ElementAdded(e);
      CommentReferencesSubjects link = e.ModelElement as CommentReferencesSubjects;
      Comment comment = link.Comment;
      FlowElement subject = link.Subject;
      Transaction current = link.Store.TransactionManager.CurrentTransaction;
      // Don't want to run when we're just loading from file:
      if (current.IsSerializing) return;
      comment.Text = "Flow has " + subject.FlowTo.Count + " outgoing connections";
    }

  }

  public partial class TaskRuleExampleDomainModel
  {
    protected override Type[] GetCustomDomainModelTypes()
    {
      List<Type> types = new List<Type>(base.GetCustomDomainModelTypes());
      types.Add(typeof(RoleRule));
      return types.ToArray();
    }
  }

}
```

## <a name="see-also"></a>另请参阅

- [事件处理程序在模型外部传播更改](../modeling/event-handlers-propagate-changes-outside-the-model.md)
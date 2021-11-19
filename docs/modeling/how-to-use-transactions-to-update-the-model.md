---
title: 如何：使用事务更新模型
description: 了解事务确保对存储所做的更改被视为组，以及如何使用事务来更新模型。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 8b1d0914c83a8cc36a389006560401619fab1ef7
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665992"
---
# <a name="how-to-use-transactions-to-update-the-model"></a>如何：使用事务更新模型
事务确保对存储区所做的更改被视为组。 分组的更改可以作为单个单元提交或回滚。

 每当程序代码在可视化和建模 SDK Visual Studio Store 中修改、添加或删除任何元素时，都必须在事务内这样做。 发生更改时，必须有一个 <xref:Microsoft.VisualStudio.Modeling.Transaction> 与 Store 关联的活动实例。 这适用于所有模型元素、关系、形状、关系图及其属性。

 事务机制可帮助你避免不一致状态。 如果在事务期间发生错误，则回滚所有更改。 如果用户执行 Undo 命令，则每个最近的事务都被视为单个步骤。 用户无法撤消最近更改的某些部分，除非将它们显式放在单独的事务中。

## <a name="opening-a-transaction"></a>打开事务
 管理事务的最方便方法是使用 语句括在 `using` 语句 `try...catch` 中：

```csharp
Store store; ...
try
{
  using (Transaction transaction =
    store.TransactionManager.BeginTransaction("update model"))
    // Outermost transaction must always have a name.
  {
    // Make several changes in Store:
    Person p = new Person(store);
    p.FamilyTreeModel = familyTree;
    p.Name = "Edward VI";
    // end of changes to Store

    transaction.Commit(); // Don't forget this!
  } // transaction disposed here
}
catch (Exception ex)
{
  // If an exception occurs, the Store will be
  // rolled back to its previous state.
}
```

 如果在更改期间发生阻止最终的异常 `Commit()` ，存储将重置为以前的状态。 这有助于确保错误不会使模型保持不一致状态。

 可以在一个事务内进行任意数目的更改。 可以在活动事务中打开新事务。 嵌套事务必须在包含事务结束之前提交或回滚。 有关详细信息，请参阅 属性 <xref:Microsoft.VisualStudio.Modeling.Transaction.TransactionDepth%2A> 的示例。

 若要使更改永久化，应在释放 `Commit` 事务之前处理事务。 如果发生未在事务内捕获的异常，则存储将在更改之前重置为其状态。

## <a name="rolling-back-a-transaction"></a>回滚事务
 若要确保存储在事务之前保持或恢复其状态，可以使用以下策略之一：

1. 引发未在事务范围内捕获的异常。

2. 显式回滚事务：

    ```csharp
    this.Store.TransactionManager.CurrentTransaction.Rollback();
    ```

## <a name="transactions-do-not-affect-non-store-objects"></a>事务不影响非存储对象
 事务仅控制存储的状态。 它们无法撤消对外部项（如文件、数据库或已在 DSL 定义外部使用普通类型声明的对象）进行的部分更改。

 如果异常可能导致此类更改与 Store 不一致，应在异常处理程序中处理这种可能性。 确保外部资源与 Store 对象保持同步的一种方式是使用事件处理程序将每个外部对象耦合到存储内元素。 有关详细信息，请参阅事件 [处理程序在模型 外部传播更改](../modeling/event-handlers-propagate-changes-outside-the-model.md)。

## <a name="rules-fire-at-the-end-of-a-transaction"></a>规则在事务结束时执行
 在事务结束时，在释放事务之前，将触发附加到存储区中的元素的规则。 每个规则都是应用于已更改的模型元素的方法。 例如，存在"修复"规则，这些规则在形状的模型元素发生更改时更新形状的状态，并创建模型元素时创建形状。 没有指定的激发顺序。 规则做出更改可以再发一个规则。

 可以定义自己的规则。 有关规则详细信息，请参阅响应和 [传播更改](../modeling/responding-to-and-propagating-changes.md)。

 在撤消、重做或回滚命令后，不会执行规则。

## <a name="transaction-context"></a>事务上下文
 每个事务都有一个字典，可在其中存储任何需要的信息：

 `store.TransactionManager`

 `.CurrentTransaction.TopLevelTransaction`

 `.Context.Add(aKey, aValue);`

 这尤其适用于在规则之间传输信息。

## <a name="transaction-state"></a>事务状态
 在某些情况下，如果更改是由撤消或重做事务导致的，则需要避免传播更改。 例如，如果编写可更新 Store 中的另一个值的属性值处理程序，则可能会发生这种情况。 由于撤消操作将 Store 中所有值重置为以前的状态，因此不需要计算更新的值。 使用以下代码：

```csharp
if (!this.Store.InUndoRedoOrRollback) {...}
```

 最初从文件加载存储时，可能会启动规则。 若要避免响应这些更改，请使用：

```csharp
if (!this.Store.InSerializationTransaction) {...}
```

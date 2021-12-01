---
title: 简化 LINQ 表达式
description: 此重构用于删除对 Where 的 Enumerable 方法的不必要调用。
ms.date: 07/05/2021
ms.topic: reference
author: m-redding
ms.author: midumont
manager: jmartens
ms.technology: vs-ide-general
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 4d97f56dbf3e8c4e3b198de413f6f4700ea4eb16
ms.sourcegitcommit: 8e74969ff61b609c89b3139434dff5a742c18ff4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2021
ms.locfileid: "128426295"
---
# <a name="simplify-linq-expression"></a>简化 LINQ 表达式

此重构适用于：

- C#

**功能：** 用于 `Enumerable.Single()` 的 `SomeEnumerable.Single(<LambdaExpression>)` 的 `SomeEnumerableType.Where(<LambdaExpression>).Single()` 重构实例，以及以下 Enumerable 方法：`SingleOrDefault()`、`Last()`、`LastOrDefault()`、`Any()`、`Count()`、`First()` 和 `FirstOrDefault()`。

**使用时机：** 方法调用 `Single()`、`SingleOrDefault()` 等的所有实例都不具有任何参数，并且前面有一个 `Where()` 表达式。 `Where()` 表达式的输入不能构造为表达式树。

原因：删除对 `.Where()` 方法的 Enumerable 的不必要的调用可提高可读性，在某些情况下还可提高性能，请参阅“备注”。

## <a name="how-to"></a>操作说明

1. 将光标置于 Visual Basic 的 `SomeEnumerableType.Where(<LambdaExpression>).Single()` 实例中。
2. 按“Ctrl”+ **。** 触发“快速操作和重构”菜单。
3. 选择“简化 LINQ 表达式”

   ![将 typeof 转换为 nameof](media/simplify-linq-expression.png)
   
## <a name="remarks"></a>注解

在某些情况下，此重构可能会降低性能。 在这种情况下，对 `List<T>` 和 `T[]` 执行的 LINQ 操作不会优化，从而导致性能下降。

## <a name="see-also"></a>另请参阅

- [重构](../refactoring-in-visual-studio.md)

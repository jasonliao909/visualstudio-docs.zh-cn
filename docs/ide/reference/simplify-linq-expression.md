---
title: 简化 LINQ 表达式
description: 此重构用于删除对 Where 的 Enumerable 方法的不必要调用。
ms.date: 08/12/2020
ms.topic: reference
author: m-redding
ms.author: midumont
manager: jmartens
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 20a3524d786b1f03fc3e221d1b257892d9439a0b
ms.sourcegitcommit: 8590cf6b3351e82827fd21159beefef0c02bf162
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2021
ms.locfileid: "102466162"
---
# <a name="simplify-linq-expression"></a>简化 LINQ 表达式

此重构适用于：

- C#

**功能：** 用于 `Enumerable.Single()` 的 `SomeEnumerable.Single(<LambdaExpression>)` 的 `SomeEnumerableType.Where(<LambdaExpression>).Single()` 重构实例，以及以下 Enumerable 方法：`SingleOrDefault()`、`Last()`、`LastOrDefault()`、`Any()`、`Count()`、`First()` 和 `FirstOrDefault()`。

**使用时机：** 方法调用 `Single()`、`SingleOrDefault()` 等的所有实例都不具有任何参数，并且前面有一个 `Where()` 表达式。 `Where()` 表达式的输入不能构造为表达式树。

操作原因：删除对 `.Where()` 方法的 Enumerable 的不必要的调用可提高性能和可读性。

## <a name="how-to"></a>操作说明

1. 将光标置于 Visual Basic 的 `SomeEnumerableType.Where(<LambdaExpression>).Single()` 实例中。
2. 按“Ctrl”+ **。** 触发“快速操作和重构”菜单。
3. 选择“简化 LINQ 表达式”

   ![将 typeof 转换为 nameof](media/simplify-linq-expression.png)

## <a name="see-also"></a>请参阅

- [重构](../refactoring-in-visual-studio.md)

---
title: 简化条件表达式
description: 了解如何使用“快速操作和重构”菜单来简化条件表达式。
ms.custom: SEO-VS-2020
ms.date: 06/08/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jmartens
ms.technology: vs-ide-general
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 3784e6ac94440c433220432cd0b14c45254e8f14
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126641769"
---
# <a name="simplify-conditional-expression-refactoring"></a>简化条件表达式重构

此重构适用于：

- C#

**功能：** 允许简化 [条件表达式](/dotnet/csharp/language-reference/operators/conditional-operator)。

**使用时机：** 需要删除不必要的代码以提高清晰度。

操作原因：简化条件表达式可以提供更清晰和简洁的语法。 此重构工具可自动执行此任务，而无需手动执行该任务。

## <a name="how-to"></a>操作说明

1. 将插入符号置于条件表达式上：

2. 按“Ctrl”+ **。** 触发“快速操作和重构”菜单。

3. 选择“简化条件表达式”

    ![简化条件表达式](media/simplify-conditional-expression.png)

## <a name="see-also"></a>请参阅

- [重构](../refactoring-in-visual-studio.md)
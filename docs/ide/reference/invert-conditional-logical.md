---
title: 反转条件表达式和逻辑运算
description: 了解如何使用“快速操作和重构”菜单来反转条件表达式或条件 AND/OR 运算符。
ms.custom: SEO-VS-2020
ms.date: 02/19/2019
ms.topic: reference
author: kendrahavens
ms.author: kehavens
manager: jmartens
ms.technology: vs-ide-general
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 6d42cbd379550d8abb739aafacca5698f164048f
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126641185"
---
# <a name="invert-conditional-expressions-and-conditional-andor-operators"></a>反转条件表达式和条件 AND/OR 运算符

此重构适用于：

- C#
- Visual Basic

**功能：** 可以反转条件表达式或条件 AND/OR 运算符。

**使用时机：** 如果进行反转，条件表达式或条件 AND/OR 运算符将更好被理解。

操作原因：手动反转表达式或条件 AND/OR 运算符可能需要更长的时间并可能引入错误。 此代码修补程序可帮助你自动执行此重构。

## <a name="invert-conditional-expressions-and-conditional-andor-operators-refactoring"></a>反转条件表达式和条件 AND/OR 重构

1. 请将光标置于条件表达式或条件 AND/OR 运算符。
2. 按“Ctrl”+ **。** 触发“快速操作和重构”  菜单。
3. 选择“反转条件”或“将 '&&' 替换为 '||'”

    ![反转条件选项的屏幕截图。](media/invert-conditional.png)

    ![使用“||”替换“&&”选项的屏幕截图。](media/invert-logical-operator.png)

## <a name="see-also"></a>另请参阅

- [重构](../refactoring-in-visual-studio.md)
- [针对 .NET 开发人员的提示](../csharp-developer-productivity.md)

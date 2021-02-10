---
title: 反转 if 语句
description: 了解如何使用“快速操作和重构”菜单来反转 if 或 else 语句，且无需更改代码的含义。
ms.custom: SEO-VS-2020
ms.date: 02/19/2019
ms.topic: reference
author: kendrahavens
ms.author: kehavens
manager: jmartens
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: cf4ad7c25030e4a331ee67f4957ddac59afdd966
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99852227"
---
# <a name="invert-if-statement"></a>反转 if 语句

此重构适用于：

- C#
- Visual Basic

**功能：** 无需更改代码的含义，即可反转 `if` 或 `if else` 语句。

**使用时机：** 如果进行反转，`if` 或 `if else` 语句会更好理解。

操作原因：手动反转 `if` 或 `if else` 语句可能需要更长时间并可能引入错误。 此代码修补程序可帮助你自动执行此重构。

## <a name="invert-if-statement-refactoring"></a>反转 if 语句重构

1. 请将光标置于 `if` 或 `if else` 语句中。

    ![反转 if else](media/invert-if.png)

2. 按“Ctrl”+ **。** 触发“快速操作和重构”  菜单。

    ![反转 if else 代码修补程序](media/invert-if-codefix.png)

3. 选择“反转 if”。

    ![反转 if else 结果](media/invert-if-codefix-result.png)

## <a name="see-also"></a>另请参阅

- [重构](../refactoring-in-visual-studio.md)
- [针对 .NET 开发人员的提示](../csharp-developer-productivity.md)

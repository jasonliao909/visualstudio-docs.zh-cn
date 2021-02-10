---
title: 简化字符串内插
description: 了解如何使用“快速操作和重构”菜单来简化字符串内插。
ms.custom: SEO-VS-2020
ms.date: 03/10/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jmartens
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: ee23429980accbbedaa2cf14aaf8a673864179a9
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99897788"
---
# <a name="simplify-string-interpolation-refactoring"></a>简化字符串内插重构

此重构适用于：

- C#

- Visual Basic

**功能：** 让你可以 [简化字符串内插](/dotnet/csharp/tutorials/string-interpolation)。

**使用时机：** 当你有可简化的字符串内插时。

操作原因：简化字符串内插可以提供更清晰和简洁的语法。 此重构工具可自动执行此任务，而无需手动执行该任务。

## <a name="how-to"></a>操作说明

1. 将插入光标置于字符串内插上：

2. 按“Ctrl”  + **。** 触发“快速操作和重构”  菜单。

3. 选择“简化内插”

    ![简化字符串内插](media/simplify-string-interpolation.png)

## <a name="see-also"></a>请参阅

- [重构](../refactoring-in-visual-studio.md)
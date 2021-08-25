---
title: 添加显式强制转换
description: 了解如何根据代码的上下文自动向表达式添加显式强制转换。
ms.custom: SEO-VS-2020
ms.date: 03/26/2020
ms.topic: reference
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- dotnet
ms.openlocfilehash: 02227e6f57761aa08ed0110442e58d31b1d06fd8
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122034391"
---
# <a name="add-explicit-cast"></a>添加显式强制转换

此代码生成适用于：

- C#

**功能：** 允许根据使用情况，自动向表达式添加显式强制转换。

**使用时机：** 需要向表达式添加显式强制转换，并希望正确地自动分配它。

操作原因：  可以手动向表达式添加显式强制转换，但此功能会根据代码上下文自动添加它。

## <a name="how-to-use-it"></a>使用方法

1. 将脱字号放置在错误上。
2. 按“Ctrl”  + **。** 触发“快速操作和重构”  菜单。
3. 选择“添加显式强制转换”  。

   ![在 Visual Studio 中添加显式强制转换快速操作](media/add-explicit-cast.png)

## <a name="see-also"></a>请参阅

- [代码生成](../code-generation-in-visual-studio.md)
- [重构](../refactoring-in-visual-studio.md)

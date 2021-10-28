---
title: 提取本地函数
description: 通过选择代码并按 Ctrl+R、Ctrl+M，将代码片段转换为自己的函数。
ms.date: 02/19/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jmartens
ms.technology: vs-ide-general
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 8b1f05e564f5d26c3c470917dbdf9bb9045a689a
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126644419"
---
# <a name="extract-local-function-refactoring"></a>提取本地函数重构

此重构适用于：

- C#

**功能：** 将代码片段从现有方法转换为本地函数。

**使用时机：** 需要从本地函数调用某些方法中现有的代码片段时。

操作原因：  可以复制/粘贴该代码，但这样会导致重复。 更好的解决方案是将此片段重构为其自己的本地函数。

## <a name="how-to"></a>操作说明

1. 突出显示要提取的代码。

2. 按“Ctrl”  + **。** 触发“快速操作和重构”  菜单。 

3. 选择“提取本地函数”  。

    ![Visual Studio 代码窗口的屏幕截图，其中突出显示一个代码行。 “快速操作和重构”菜单处于打开状态，并且选中了“提取本地函数”。](media/extract-local-function.png)

## <a name="see-also"></a>请参阅

- [重构](../refactoring-in-visual-studio.md)
- [预览更改](../../ide/preview-changes.md)

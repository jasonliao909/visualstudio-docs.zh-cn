---
title: Office Excel键盘、设置"选项"对话框
description: 了解如何在文档具有焦点Microsoft Excel选择"动态键盘方案"，使用户能够接收快捷键命令。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VST.ExcelOptions.KeyboardMappingScheme
- VS.ToolsOptionsPages.Microsoft_Office_Keyboard_Settings.Microsoft_Office_Excel_Keyboard
- VS.ToolsOptionsPages.Microsoft_Office_Tools.Microsoft_Office_Excel.Keyboard
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- keyboard shortcuts, Office development in Visual Studio
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: d33811c8b5fc38359e59a1ff2708ba05d2f2f1d5
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664949"
---
# <a name="microsoft-office-excel-keyboard-settings-options-dialog-box"></a>Microsoft Office Excel键盘设置"选项"对话框
  Microsoft Office Excel和Visual Studio都处理快捷键。 同一个快捷键组合可以代表 Excel 和 Visual Studio 中的不同命令。 在 Excel 文档级项目中打开Visual Studio，一次只有一个应用程序接收快捷键命令。 默认情况下，Visual Studio接收所有快捷键命令，但当文档Excel时，可以通过选择"动态键盘方案"来接收 **它们**。

 如果使用的快捷键未分配给当前正在处理快捷键的应用程序中的命令，则快捷键将传递给另一个应用程序。

 你选择的选项将保持对项目Excel生效，直到更改它。 选择不会影响 Word Microsoft Office项目;必须使用 Word 键盘选项对 Word Microsoft Office任何更改。

## <a name="uielement-list"></a>UIElement 列表
 **Visual Studio键盘Visual Studio** 接收所有快捷键命令，即使Excel焦点。 例如，如果在焦点具有焦点时按函数键 **F5** Excel，Visual Studio开始调试解决方案。

 **动态键盘Visual Studio** 仅在具有焦点时接收快捷键命令。 当Excel焦点时，Excel接收所有快捷键命令。 例如，如果在焦点为 Excel按函数键 **F5，Excel** 打开"转到"对话框。  如果在焦点Visual Studio按 **F5，Visual Studio** 开始调试解决方案。

## <a name="see-also"></a>另请参阅
- [Microsoft OfficeWord 键盘，Microsoft Office键盘设置，"选项"对话框](../vsto/microsoft-office-word-keyboard-microsoft-office-keyboard-settings-options-dialog-box.md)

---
title: Office Excel 键盘，设置，"选项" 对话框
description: 了解如何通过选择动态键盘方案，在文档具有焦点时，使 Microsoft Excel 接收快捷方式键命令。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122115078"
---
# <a name="microsoft-office-excel-keyboard-settings-options-dialog-box"></a>Microsoft Office Excel 键盘，设置，"选项" 对话框
  Microsoft Office Excel 和 Visual Studio 都处理快捷键。 同一快捷键组合可用于 Excel 和 Visual Studio 中的不同命令。 如果 Excel 在 Visual Studio 的文档级项目中打开，则一次只能有一个应用程序收到快捷键命令。 默认情况下，Visual Studio 接收所有快捷键命令，但你可以通过选择 "**动态键盘方案**"，使 Excel 在文档具有焦点时接收它们。

 如果使用未分配给当前正在处理快捷键的应用程序中的命令的快捷键，则快捷键会传递到其他应用程序。

 选择的选项将对 Excel 项目保持有效，直到您更改它。 选择不会影响 Word 项目 Microsoft Office;您必须使用 Microsoft Office word 键盘选项对 word 进行任何更改。

## <a name="uielement-list"></a>UIElement 列表
 **Visual Studio 键盘方案** Visual Studio 接收所有快捷键命令，即使 Excel 具有焦点。 例如，如果在 Excel 具有焦点时按下函数键 **F5** ，Visual Studio 将开始调试解决方案。

 **动态键盘方案** Visual Studio 仅在其具有焦点时才接收快捷键命令。 当 Excel 有焦点时，Excel 接收所有快捷键命令。 例如，如果在 Excel 具有焦点时按下函数键 **F5** ，Excel 将打开 "**转到**" 对话框。 如果在 Visual Studio 有焦点时按 **F5** ，Visual Studio 将开始调试解决方案。

## <a name="see-also"></a>请参阅
- [Microsoft OfficeWord 键盘，Microsoft Office 键盘设置，"选项" 对话框](../vsto/microsoft-office-word-keyboard-microsoft-office-keyboard-settings-options-dialog-box.md)

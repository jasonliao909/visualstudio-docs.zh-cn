---
title: OfficeWord 键盘、设置、"选项" 对话框
description: 了解如何通过选择动态键盘方案，在文档具有焦点时，使 Microsoft Word 接收快捷方式键命令。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Microsoft_Office_Tools.Microsoft_Office_Word.Keyboard
- VS.ToolsOptionsPages.Microsoft_Office_Keyboard_Settings.Microsoft_Office_Word_Keyboard
- VST.WordOptions.KeyboardMappingScheme
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
ms.openlocfilehash: ec9df6fb069994144503f89808d2b6cf64a14883
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122025935"
---
# <a name="microsoft-office-word-keyboard-settings-options-dialog-box"></a>Microsoft OfficeWord 键盘、设置、"选项" 对话框
  Microsoft OfficeWord 和 Visual Studio 都处理快捷键。 在 Word 和 Visual Studio 中，同一快捷键组合可用于不同的命令。 在 Visual Studio 中的文档级项目中打开 Word 时，一次只能有一个应用程序收到快捷键命令。 默认情况下，Visual Studio 接收所有快捷键命令，但你可以通过选择 "**动态键盘方案**" 使 Word 在文档具有焦点时接收这些命令。

 如果使用未分配给当前正在处理快捷键的应用程序中的命令的快捷键，则快捷键会传递到其他应用程序。

 你选择的选项将对 Word 项目保持有效，直到你进行更改。 选择不会影响 Excel 项目 Microsoft Office;您必须使用 Microsoft Office Excel 键盘选项对 Excel 进行任何更改。

## <a name="uielement-list"></a>UIElement 列表
 **Visual Studio 键盘方案** Visual Studio 接收所有快捷键命令，即使 Word 文档具有焦点也是如此。 例如，如果在文档具有焦点时按 "函数键 **F5** "，Visual Studio 将开始调试解决方案。

 **动态键盘方案** Visual Studio 仅在其具有焦点时才接收快捷键命令。 当 Word 文档有焦点时，Word 会接收所有快捷键命令。 例如，如果在 Word 文档具有焦点时按 "函数键 **F5** "，word 将打开 " **查找和替换** " 对话框，并选中 " **转到** " 选项卡。 如果在 Visual Studio 有焦点时按 **F5** ，Visual Studio 将开始调试解决方案。

## <a name="see-also"></a>请参阅
- [Microsoft Office Excel 键盘，Microsoft Office 键盘设置，"选项" 对话框](../vsto/microsoft-office-excel-keyboard-microsoft-office-keyboard-settings-options-dialog-box.md)

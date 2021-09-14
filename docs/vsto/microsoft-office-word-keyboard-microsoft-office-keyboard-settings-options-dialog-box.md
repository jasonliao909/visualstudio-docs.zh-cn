---
title: OfficeWord 键盘，设置，"选项"对话框
description: 了解如何在文档具有焦点Microsoft Word通过选择动态键盘方案来接收快捷键命令。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664948"
---
# <a name="microsoft-office-word-keyboard-settings-options-dialog-box"></a>Microsoft OfficeWord 键盘，设置，"选项"对话框
  Microsoft OfficeWord 和 Visual Studio都处理快捷键。 相同的快捷键组合可以代表 Word 和 Visual Studio 中的不同命令。 当 Word 在 Visual Studio 文档级项目中打开时，一次只有一个应用程序接收快捷键命令。 默认情况下，Visual Studio接收所有快捷键命令，但当文档具有焦点时，可以通过选择"动态键盘方案"使 Word **接收它们**。

 如果使用的快捷键未分配给当前正在处理快捷键的应用程序中的命令，则快捷键将传递给另一个应用程序。

 在更改 Word 项目之前，你选择的选项将一直有效。 选择不会影响Microsoft Office Excel项目;必须使用"键盘"选项Excel对Microsoft Office Excel更改。

## <a name="uielement-list"></a>UIElement 列表
 **Visual Studio键盘Visual Studio** 接收所有快捷键命令，即使 Word 文档具有焦点。 例如，如果在文档具有焦点时按函数键 **F5，Visual Studio** 开始调试解决方案。

 **动态键盘Visual Studio** 仅在具有焦点时接收快捷键命令。 当 Word 文档具有焦点时，Word 将接收所有快捷键命令。 例如，如果在 Word 文档具有焦点时按函数键 **F5，Word** 将打开"查找和 **替换** "对话框，并选中" **转到"** 选项卡。 如果在焦点Visual Studio按 **F5，Visual Studio** 开始调试解决方案。

## <a name="see-also"></a>另请参阅
- [Microsoft Office Excel键盘，Microsoft Office键盘设置"选项"对话框](../vsto/microsoft-office-excel-keyboard-microsoft-office-keyboard-settings-options-dialog-box.md)

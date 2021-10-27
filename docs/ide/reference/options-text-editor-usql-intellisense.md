---
title: “选项”>“文本编辑器”>“U-SQL”>“IntelliSense”
description: 了解如何使用 U-SQL 部分中的“IntelliSense”页面来修改 U-SQL 的文本编辑器 IntelliSense 设置。
ms.custom: SEO-VS-2020
ms.date: 01/17/2019
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.U-SQL.IntelliSense
- VS.ToolsOptionsPages.Text_Editor.HQL.IntelliSense
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: 0455aa2420e260af0239100513cd7a042a8bcaf6
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126641145"
---
# <a name="options-text-editor-u-sql-intellisense"></a>“选项”>“文本编辑器”>“U-SQL”>“IntelliSense”

使用“IntelliSense”选项页，可以修改一些与 U-SQL 相关的文本编辑器设置。 若要访问此选项页，请先依次选择“工具” > “选项”，再依次选择“文本编辑器” > “U-SQL” > “IntelliSense”。

## <a name="intellisense-settings"></a>IntelliSense 设置

选中复选框即可启用“快速信息”或“Intellisense”。 如果你将鼠标光标悬停在变量之上，快速信息就会显示完成声明。

## <a name="completion-lists"></a>完成列表

- **键入字符后显示完成列表**

   选择此选项后，IntelliSense 在你开始键入时会自动显示完成列表。 如果取消选中此选项，仍可通过“IntelliSense”菜单或按 Ctrl + 空格键使用 IntelliSense 完成功能。

- **将关键字放入完成列表**

   如果你选中此选项，IntelliSense 就会在完成列表中添加关键字。

- **将代码片段放入完成列表**

   如果你选中此选项，IntelliSense 就会在完成列表中添加代码片段。

## <a name="selection-in-completion-list"></a>完成列表中的选定内容

- **通过键入以下字符提交**

   此字段显示导致编辑器提交当前突出显示的完成列表建议的字符。 可以在此列表中添加或删除字符。

- **通过按空格键提交**

   如果选中此选项，可以通过按空格键提交突出显示的完成列表建议。

- **按 Enter 在完整键入的字词末尾添加新行**

   如果你选中此选项，编辑器就会在你键入完成列表建议的所有字符时自动添加新行，并将光标移到新行。

## <a name="see-also"></a>请参阅

- [“选项”对话框 ->“环境”->“常规”](../../ide/reference/general-environment-options-dialog-box.md)
- [使用 IntelliSense](../../ide/using-intellisense.md)
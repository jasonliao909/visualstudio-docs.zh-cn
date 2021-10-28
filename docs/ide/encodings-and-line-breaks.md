---
title: 编码和换行符字符
description: 了解 Visual Studio 解释为换行符的字符并了解维护原始编码和换行符的方式。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.Encoding
helpviewer_keywords:
- line breaks
- encoding
- Visual Studio, encoding
- editors, line breaks
- line break characters
- Visual Studio, line break characters
ms.assetid: 8f9b3ffc-7b8d-44f4-87cb-dc29105be12d
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: db0efa149538d91c5123f6a973d5e8a455ff2e62
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126642193"
---
# <a name="encodings-and-line-endings"></a>编码和行尾

在 Visual Studio 中，以下字符将解释为换行符：

- CR LF:回车符 + 换行符，Unicode 字符 000D + 000A

- LF：换行符，Unicode 字符 000A

- NEL：下一行，Unicode 字符 0085

- LS：行分隔符，Unicode 字符 2028

- PS：段落分隔符，Unicode 字符 2029

从其他应用程序复制的文本将保留原始编码和换行符。 例如，当从记事本复制文本并将其粘贴到 Visual Studio 中的文本文件时，此文本的设置仍与在记事本中的设置相同。

当打开包含不同换行符的文件时，可能会看到一个对话框，询问是否应规范化不一致的换行符以及要选择哪一种换行类型。

## <a name="advanced-save-options"></a>高级保存选项

可以使用“文件” > “高级保存选项”对话框来确定所需的换行符类型   。 还可使用相同的设置更改文件的编码。

![“高级保存选项”对话框](media/line_endings.png)

> [!NOTE]
> 如果在“文件”  菜单上看不到“高级保存选项”  ，则可以添加它。 
> 1. 依次选择“工具”和“自定义”。 
> 1. 依次选择“命令”选项卡和“菜单栏”单选按钮，然后从相应的下拉列表中选择“文件”。 选择“添加命令”按钮。 
> 1. 在“添加命令”对话框中的“类别”，选择“文件”，然后在“命令”列表中，选择“高级保存选项”      。 选择“确定”按钮。
> 1. 使用“上移”和“下移”按钮，以将命令移动到菜单中的任意位置。 选择“关闭”  以关闭“自定义”  对话框。 
> 有关详细信息，请参阅[自定义菜单和工具栏](../ide/how-to-customize-menus-and-toolbars-in-visual-studio.md#customizing_menu)。
>
> 或者，可以通过选择“文件” > “将 \<file\> 另存为”来访问“高级保存选项”对话框  。 在“将文件另存为”对话框中，选择“保存”按钮旁边的下拉三角形，然后选择“以编码方式保持”。

## <a name="see-also"></a>请参阅

- [代码编辑器功能](../ide/writing-code-in-the-code-and-text-editor.md)

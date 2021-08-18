---
title: Visual Studio 命令的 GUID |Microsoft Docs
description: 了解如何在 IDE Visual Studio 集成开发环境中查找 (GUID 和 ID) 。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- commands
- id
- command placement
- visual studio command
- guid
ms.assetid: 2ea4bee2-0259-4675-8e65-2023b312b516
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: bcc20cea8db7aa72c1c13ed5cae095ea4c6944298c47f62fcb2d042df9dfb593
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121337924"
---
# <a name="guids-and-ids-of-visual-studio-commands"></a>命令的 GUID Visual Studio的 ID
Visual Studio 集成开发环境 (IDE) 中包含的命令的 GUID 和 ID 值在作为 Visual Studio SDK 的一部分安装的 .vsct 文件中定义。 有关详细信息，请参阅 [IDE 定义的命令、菜单和组](../../extensibility/internals/ide-defined-commands-menus-and-groups.md)。

 若要详细了解如何使用 *.vsct* 文件中定义的 IDE 对象，请参阅 [扩展菜单和命令](../../extensibility/extending-menus-and-commands.md)。

## <a name="find-a-command-definition"></a>查找命令定义
 由于Visual Studio定义了 1000 多个命令，因此在此处列出所有这些命令不切实际。 请改为按照以下步骤查找命令的定义。

### <a name="to-locate-a-command-definition"></a>查找命令定义

1. 在 Visual Studio 中，打开<Visual Studio SDK 安装路径 *\> \VisualStudioIntegration\Common\Inc \\* 文件夹中的以下文件：SharedCmdDef.vsct、ShellCmdDef.vsct、VsDbgCmdUsed.vsct、*则使用 Visualmenu.vsct*。   

    大多数Visual Studio命令在 *SharedCmdDef.vsct* 和 *ShellCmdDef.vsct 中定义*。 *VsDbgCmdUsed.vsct* 定义与调试器相关的命令， *而Menmenu.vsct* 定义特定于 Web 开发的命令。

2. 如果命令是菜单项，请记下菜单项的确切文本。 如果命令是工具栏上的按钮，请记下在工具栏上暂停时显示的工具提示文本。

3. 按 **Ctrl** + **F** 打开"**查找"** 对话框。

4. 在" **查找内容** "框中，键入在步骤 2 中说明的文本。

5. 验证 **"查找方式"** 框中是否显示"所有 **打开的文档** "。

6. 单击" **查找下一** 步"按钮，直到在 Button 元素 的 `<Strings>` 部分中 [选择了文本](../../extensibility/button-element.md)。

    `<Button>`命令显示的元素是命令定义。

   找到命令定义后，可以通过创建与命令具有相同的 和 值的 [CommandPlacement](../../extensibility/commandplacement-element.md) 元素，将命令的副本放在另一 `guid` `id` 个菜单或工具栏上。 有关详细信息，请参阅 [创建可重用的按钮组](../../extensibility/creating-reusable-groups-of-buttons.md)。

### <a name="special-cases"></a>特殊情况
 在下列情况下，菜单文本或工具提示文本可能与命令定义中的内容不完全匹配。

- 包含带下划线字符的菜单项，例如"文件"菜单上的 **"** 打印"命令，*其中 P* 带有下划线。

     菜单项名称中前面带有 (&) 字符的字符显示为带下划线。 但是 *，.vsct* 文件是用 XML 编写的，XML 使用 ampersand (&) 字符来指示特殊字符，并且要求要显示的和必须拼写为 *&amp; amp;*。 因此，在 *.vsct* 文件中 **，Print** 命令显示为 *&amp; amp;打印*。

- 具有动态文本的命令，例如 **"保存**"和动态生成的菜单项，例如"最近使用 \<Current Filename\> **的文件"列表中的** 项。

     没有可靠的方法可以搜索动态文本。 而是通过查阅 Visual Studio 菜单的[GUID](../../extensibility/internals/guids-and-ids-of-visual-studio-menus.md)或 Visual Studio 工具栏的[GUID](../../extensibility/internals/guids-and-ids-of-visual-studio-toolbars.md)和 ID 来查找托管所需命令的组，并搜索该组的 ID。 如果命令定义没有组作为其父元素，请 [](../../extensibility/parent-element.md)搜索 *SharedCmdPlace.vsct* 和 *ShellCmdPlace.vsct* (或 *VsDbgCmdPlace.vsct，* 查找调试器命令) 以查找设置命令父级的元素。 `<CommandPlacement>` *SharedCmdPlace.vsct、ShellCmdPlace.vsct* 和 *VsDbgCmdPlace.vsct* 在 *\<Visual Studio SDK installation path\> \VisualStudioIntegration\Common\Inc \\* 文件夹中。 

## <a name="see-also"></a>请参阅

- [Visual Studio命令表 (.vsct) 文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
- [VSCT XML 架构参考](../../extensibility/vsct-xml-schema-reference.md)

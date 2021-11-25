---
title: 自定义菜单和工具栏
description: 了解如何自定义 Visual Studio 菜单和工具栏，并了解如何自定义菜单和工具栏中包含的任意命令。
ms.custom: SEO-VS-2020
ms.date: 11/24/2021
ms.topic: how-to
f1_keywords:
- vs.renametoolbar
- vs.customize.toolbars
- vs.buttoneditor
- vs.customize.commands
- vs.newtoolbar
helpviewer_keywords:
- captions, customizing toolbar
- custom toolbars [Visual Studio]
- command buttons, customizing toolbar
- labels, customizing toolbar
- images [Visual Studio], toolbar buttons
- buttons [Visual Studio], custom toolbars
- toolbars [Visual Studio], creating in the IDE
- icons [Visual Studio], customizing toolbar
- commands [Visual Studio], customizing environment
- customizing toolbars
- toolbars [Visual Studio], customizing
- toolbars [Visual Studio], customizing in the IDE
ms.assetid: b570ae2f-5302-45dc-9cc9-8d4d1ad50603
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: 6a93698d1bbc2f7240ff43f3e81a8fcb074b96af
ms.sourcegitcommit: 5af130d3ff64b71d415819e42f4f2efb2ae36a6a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/25/2021
ms.locfileid: "133117466"
---
# <a name="how-to-customize-menus-and-toolbars-in-visual-studio"></a>如何：在 Visual Studio 中自定义菜单和工具栏

在自定义 Visual Studio 时，不仅可以添加和删除工具栏及菜单栏上的菜单，还可以添加和删除任何给定工具栏或菜单上的命令。

> [!TIP]
> 若要详细了解如何个性化设置工具栏，来使其具有你的风格，请参阅我们的最新博客文章：[针对工作流优化工具栏](https://devblogs.microsoft.com/visualstudio/optimizing-toolbars-for-your-workflow/)。

## <a name="add-remove-or-move-a-menu-on-the-menu-bar"></a>添加、删除或移动菜单栏上的菜单

1. 在菜单栏上，依次选择“工具” > “自定义” 。

     此时将打开“自定义”对话框。

2. 在“命令”选项卡上，继续选中“菜单栏”选项按钮，继续在该选项旁的列表中选中“菜单栏”，然后执行下列一组步骤：

    - 若要添加菜单，请选择“添加新菜单”按钮，选择“修改所选内容”按钮，然后命名要添加的菜单。

        ::: moniker range="vs-2017"
        ![显示如何添加菜单的“自定义”对话框](../ide/media/addmenu.png)
        ::: moniker-end

    - 若要删除菜单，请在“控件”列表中选择该菜单，然后选择“删除”按钮。

    - 若要移动菜单栏内的菜单，请在“控件”列表中选择该菜单，然后选择“上移”或“下移”按钮。

## <a name="add-remove-or-move-a-toolbar"></a>添加、删除或移动工具栏

1. 在菜单栏上，依次选择“工具” > “自定义” 。

     此时将打开“自定义”对话框。

2. 在“工具栏”选项卡上，执行下面一组步骤：

    - 若要添加工具栏，请选择“新建”按钮，指定要添加的工具栏的名称，然后选择“确定”按钮。

        ::: moniker range="vs-2017"
        ![显示如何添加工具栏的“自定义”对话框](../ide/media/addtoolbar.png)
        ::: moniker-end

    - 若要删除自定义工具栏，请在“工具栏”列表中选择该工具栏，然后选择“删除”按钮。

        > [!IMPORTANT]
        > 你可以删除自己创建的工具栏，但无法删除默认的工具栏。

    - 若要将工具栏移动到其他停靠位置，请在“工具栏”列表中选择该工具栏，选择“修改所选内容”按钮，然后在随后显示的列表中选择一个位置。

        你也可以拖动工具栏的左边缘，将其移动到主停靠区域内的任何位置。

        > [!NOTE]
        > 有关如何改进工具栏的可用性和辅助功能的详细信息，请参阅[如何：设置 IDE 辅助功能选项](../ide/reference/how-to-set-ide-accessibility-options.md)。

## <a name=""></a><a name="customizing_menu">自定义菜单或工具栏</a>

> [!WARNING]
> 自定义工具栏或菜单后，请确保在“自定义”对话框中继续选中其复选框。 否则，在关闭并重新打开 Visual Studio 之后，你所做的更改将不会保留。

1. 在菜单栏上，依次选择“工具” > “自定义” 。

    此时将打开“自定义”对话框。

2. 在“命令”选项卡上，选择要自定义的元素类型的选项按钮。

3. 在该类型元素的列表中，选择要自定义的菜单或工具栏，然后执行下面一组步骤：

    - 若要添加命令，请选择“添加命令”按钮。

        在“添加命令”对话框中，依次选择“类别”列表中的项和“命令”列表中的项，然后选择“确定”按钮。

        ::: moniker range="vs-2017"
        ![Visual Studio 中的“添加命令”对话框](../ide/media/addcommand.png)
        ::: moniker-end

    - 若要删除命令，请在“控件”列表中选择该命令，然后选择“删除”按钮。

    - 若要重新排序命令，请在“控件”列表中选择一个命令，然后选择“上移”或“下移”按钮。

    - 若要将命令分组到一条水平线下，请在“控件”列表中选择第一个命令，选择“修改所选内容”按钮，然后在显示的菜单中选择“开始一组”。

## <a name="reset-a-menu-or-a-toolbar"></a>重置菜单或工具栏

1. 在菜单栏上，依次选择“工具” > “自定义” 。

    此时将打开“自定义”对话框。

2. 在“命令”选项卡上，选择要重置的元素类型的选项按钮。

3. 在该元素类型的列表中，选择要重置的菜单或工具栏。

4. 选择“修改所选内容”按钮，然后在显示的菜单中选择“重置”。

    还可以选择“全部重置”按钮，从而重置所有菜单和工具栏。

## <a name="see-also"></a>请参阅

- [个性化 IDE](../ide/personalizing-the-visual-studio-ide.md)
- [自定义编辑器](../ide/how-to-change-text-case-in-the-editor.md)

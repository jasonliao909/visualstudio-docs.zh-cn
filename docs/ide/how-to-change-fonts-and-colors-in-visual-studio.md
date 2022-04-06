---
title: 更改主题、字体、文本和对比度以提供辅助功能
description: 了解如何更改Visual Studio颜色主题、字体颜色、文本大小、额外对比度颜色等，以便轻松使用和辅助功能问题。
titleSuffix: ''
ms.date: 04/04/2022
ms.topic: how-to
ms.custom: contperf-fy22q3
helpviewer_keywords:
- Visual Studio, color themes
- color themes, Visual Studio
ms.assetid: 60d91ba1-244b-4c43-847f-60b744f1352a
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: 86089af5cdb35c674c6de1a59dd33a9182c06348
ms.sourcegitcommit: d9cab667735450e735622f8b93266f07b8046f3e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2022
ms.locfileid: "141402267"
---
# <a name="how-to-change-fonts-colors-and-themes-in-visual-studio"></a>如何：在 Visual Studio 中更改字体、颜色和主题

::: moniker range=">=vs-2022"

可以通过多种方式在 Visual Studio 中更改字体和颜色。 例如，你可以将默认的深色主题（也称为“深色模式”）更改为浅色主题、蓝色主题、额外对比度主题或与系统设置相匹配的主题。 另外，还可以在 IDE 和代码编辑器中更改默认字体和文本大小。

> [!TIP]
> 请参阅 [**2022 年 Visual Studio 博客文章中的"我们升级了 UI**](https://devblogs.microsoft.com/visualstudio/weve-upgraded-the-ui-in-visual-studio-2022/)"，详细了解微妙的颜色对比度调整以及我们添加的新 [Cascadia Code](#use-the-cascadia-code-font) 字体，以便Visual Studio每个人都更易于访问。

::: moniker-end

::: moniker range="<=vs-2019"

可以通过多种方式在 Visual Studio 中更改字体和颜色。 例如，可以将默认的蓝色主题更改为深色主题（也称为“深色模式”）。 还可以选择一个额外的对比度主题（如果它最适合你的需求）。 另外，还可以在 IDE 和代码编辑器中更改默认字体和文本大小。

::: moniker-end

## <a name="change-the-color-theme"></a>更改颜色主题

下面介绍如何在 Visual Studio 中更改 IDE 框架和工具窗口的颜色主题。

::: moniker range=">=vs-2022"

1. 在菜单栏上，依次选择“工具”>“选项”。

1. 在选项列表中，选择“环境”>“常规” 。

1. 在“颜色主题”列表中，选择默认的“深色”主题、“浅色”主题、“蓝色”主题或“蓝色(额外对比度)”主题    。

   还可以通过选择“使用系统设置”，选择使用 Windows 使用的主题。

   :::image type="content" source="media/vs-2022/fonts-colors-theme.png" alt-text="可在其中更改颜色主题的“选项”对话框的屏幕截图。":::

   > [!NOTE]
   > 当你更改颜色主题时，IDE 中的文本将恢复为默认值，或恢复为之前为该主题自定义的字体和大小。

    > [!TIP]
    > 想要更多的主题选项？ 在 [Visual Studio Marketplace](https://marketplace.visualstudio.com/search?target=VS&category=Tools&vsVersion=&subCategory=Themes&sortBy=Installs) 上查看各种自定义主题。 若要查看基于 VS Code 的新的 Visual Studio 2022 自定义主题的示例，请参阅[新的 Visual Studio 主题集合简介](https://devblogs.microsoft.com/visualstudio/custom-themes/)博客文章。

::: moniker-end

::: moniker range="<=vs-2019"

1. 在菜单栏上，依次选择“工具”>“选项”。

1. 在选项列表中，选择“环境”>“常规” 。

1. 在“颜色主题”列表中，选择默认的“蓝色”主题、“浅色”主题、“深色”主题或“蓝色(额外对比度)”主题。

   ![用于更改颜色主题的“选项”对话框的屏幕截图](media/fonts-colors-theme.png "可用于更改颜色主题的“选项”对话框的屏幕截图。")

   > [!NOTE]
   > 当你更改颜色主题时，IDE 中的文本将恢复为默认值，或恢复为之前为该主题自定义的字体和大小。

    > [!TIP]
    > 可以使用扩展创建和编辑自己的 Visual Studio 主题。 根据所使用 Visual Studio 的版本，从以下两个选项中选择一个：
    > - [Visual Studio 2019 的颜色主题设计器](https://marketplace.visualstudio.com/items?itemName=ms-madsk.ColorThemeDesigner)。
    > - [Visual Studio 2017 的颜色主题编辑器](https://marketplace.visualstudio.com/items?itemName=VisualStudioPlatformTeam.VisualStudio2017ColorThemeEditor)

::: moniker-end

## <a name="change-fonts-and-text-size"></a>更改字体和文本大小

可以更改所有 IDE 框架和工具窗口的字体和文本大小，也可以仅为某些窗口或文本元素更改字体和文本大小。 还可以更改编辑器中的字体和文本大小。

### <a name="to-change-the-font-and-text-size-in-the-ide"></a>更改 IDE 中的字体和文本大小

::: moniker range=">=vs-2022"

1. 在菜单栏上，依次选择“工具”>“选项”。

1. 在选项列表中，选择“环境”>“字体和颜色” 。

1. 在“显示以下对象的设置”列表中，选择“环境”。

   ![“选项”对话框的屏幕截图，你可以在其中更改 IDE 中的字体和文本大小](media/vs-2022/fonts-colors-text-environment.png "“选项”对话框的屏幕截图，可在其中更改 IDE 中的字体和文本大小。")

    > [!NOTE]
    > 如果仅更改工具窗口的字体，则在“显示以下对象的设置”列表中，选择“所有文本工具窗口” 。

1. 修改“字体”和“大小”选项，以更改 IDE 的字体和文本大小。

1. 在“显示项”中选择合适的项，然后修改“项前景”和“项背景”选项。

::: moniker-end

::: moniker range="<=vs-2019"

1. 在菜单栏上，依次选择“工具”>“选项”。

1. 在选项列表中，选择“环境”>“字体和颜色” 。

1. 在“显示以下对象的设置”列表中，选择“环境”。

   ![用于在 IDE 中更改字体和颜色的“选项”对话框的屏幕截图](media/fonts-colors-environment.png "用于在 IDE 中更改字体和颜色的“选项”对话框的屏幕截图。")

    > [!NOTE]
    > 如果仅更改工具窗口的字体，则在“显示以下对象的设置”列表中，选择“所有文本工具窗口” 。

1. 修改“字体”和“大小”选项，以更改 IDE 的字体和文本大小。

1. 在“显示项”中选择合适的项，然后修改“项前景”和“项背景”选项。

::: moniker-end

### <a name="to-change-the-font-and-text-size-in-the-editor"></a>更改编辑器中的字体和文本大小

::: moniker range=">=vs-2022"

1. 在菜单栏上，依次选择“工具”>“选项”。

1. 在选项列表中，选择“环境”>“字体和颜色” 。

1. 在“显示以下对象的设置”列表中，选择“文本编辑器”。

   ![“选项”对话框的屏幕截图，你可以在其中更改编辑器中的字体和文本大小](media/vs-2022/fonts-colors-text-editor.png "“选项”对话框的屏幕截图，可在其中更改编辑器中的字体和文本大小。")

1. 修改“字体”和“大小”选项，以更改编辑器的字体和文本大小。

1. 在“显示项”中选择合适的项，然后修改“项前景”和“项背景”选项。

::: moniker-end

::: moniker range="<=vs-2019"

1. 在菜单栏上，依次选择“工具”>“选项”。

1. 在选项列表中，选择“环境”>“字体和颜色” 。

1. 在“显示以下对象的设置”列表中，选择“文本编辑器”。

   ![用于在编辑器中更改字体和颜色的“选项”对话框的屏幕截图](media/fonts-colors-text-editor.png "用于更改编辑器中字体和颜色的“选项”对话框的屏幕截图。")

1. 修改“字体”和“大小”选项，以更改编辑器的字体和文本大小。

1. 在“显示项”中选择合适的项，然后修改“项前景”和“项背景”选项。

::: moniker-end

有关如何更改辅助功能字体和颜色的详细信息，请参阅此页面的 ["设置辅助功能选项](#set-accessibility-options) "部分。 有关所有用户界面的详细信息， (UI) 元素，可在其中更改字体和配色方案，请参阅 ["字体和颜色"、"环境、选项"对话框](../ide/reference/fonts-and-colors-environment-options-dialog-box.md) 页。

## <a name="set-accessibility-options"></a>设置辅助功能选项

::: moniker range="vs-2022"

在神经多元性的世界中，我们希望通过提供以下字体选项和颜色主题来为不同学习者与低视力用户提供支持：

- 可使用 [Cascadia Code](#use-the-cascadia-code-font) 字体，它向字母、数字和字符的大小添加了更多权重，帮助用户区分这三者。 Cascadia Code 还包括编码连字。
- 可选择对计算机上的所有应用和 UI 使用[高对比度](#use-windows-high-contrast)颜色主题，也可仅对 Visual Studio 使用[额外对比度](#use-visual-studio-extra-contrast)颜色主题。

### <a name="use-the-cascadia-code-font"></a>使用 Cascadia Code 字体

新的 [Cascadia Code](https://github.com/microsoft/cascadia-code#welcome) 字体包括 Cascade Mono，后者是 Visual Studio 2022 中的默认字体 。 这些字体不仅更容易阅读，而且 Cascadia Code 字体还包含编码连字，它可将字符序列转换为字形。 通过编码连字（也称为字形），用户可更容易在认知上关联其背后的含义。

下面的屏幕截图显示了默认 Cascadia Mono 字体的示例，并列出了你在编码时可能发现自己在使用的一系列字符（包含数学符号）。

:::image type="content" source="media/vs-2022/cascadia-mono-font.png" alt-text="编辑器中 Cascadia Mono 字体示例的屏幕截图。":::

下面的屏幕截图显示了 Cascadia Code 字体的示例，其中前面所示的同一系列字符转换为编码连字（也称为字形）。

:::image type="content" source="media/vs-2022/cascadia-code-font.png" alt-text="编辑器中 Cascadia Code 字体示例的屏幕截图。":::

请注意，Cascadia Code 屏幕截图中的最后一行文本显示了重复字符之间的空格是如何缩短的，这也使得它们更易于阅读。

下面介绍如何切换使用不同的 Cascadia 字体：

1. 转到“工具”>“选项”>“环境”>“字体和颜色”   。

1. 从“字体”下拉列表中，选择所需的 Cascadia Code 字体或 Cascadia Mono 字体，然后选择“确定”   。

    :::image type="content" source="media/vs-2022/cascadia-font-options.png" alt-text="“选项”对话框中提供的 Cascadia 字体的屏幕截图。":::

::: moniker-end

::: moniker range="<=vs-2019"

如果视力不好，可以选择颜色主题选项。 可以为计算机上的所有应用和 UI 使用高对比度选项，或使用仅适用于 Visual Studio 的额外对比度选项。

::: moniker-end

### <a name="use-windows-high-contrast"></a>使用 Windows 高对比度

使用以下任一过程来切换 Windows 高对比度选项：

- 在 Windows 或任何 Microsoft 应用程序中，按左 Alt+左 Shift+PrtScn 键。

- 在 Windows 中，选择“开始” > “设置” > “轻松访问”  。 然后，在 Windows 10 和更高版本的“视觉”部分下，选择“高对比度” 。

    > [!WARNING]
    > Windows 高对比度设置会影响计算机上的所有应用程序和 UI。

### <a name="use-visual-studio-extra-contrast"></a>使用 Visual Studio 额外对比度

使用以下过程来切换 Visual Studio 额外对比度选项：

1. 在 Visual Studio 的菜单栏上，选择“工具” > “选项”，然后在“选项”列表中，选择“环境” > “常规”。

1. 在“颜色主题”下拉列表中，选择“蓝色(额外对比度)”主题，然后选择“确定”。

> [!TIP]
> 如果有你认为可能有用但当前在 Visual Studio 中不可用的颜色或字体辅助功能选项，请通过选择 [Visual Studio 开发者社区](https://aka.ms/feedback/suggest?space=8)中的“建议功能”来告知我们。 有关此论坛及其工作原理的详细信息，请参阅[建议功能](../ide/suggest-a-feature.md)页。

### <a name="more-accessibility-features-in-visual-studio"></a>Visual Studio中的更多辅助功能

Visual Studio还包括帮助具有有限敏捷性的人员编写的功能。 例如，Visual Studio支持 Dvorak 键盘布局，这使得最常键入的字符更易于访问。

还可以自定义 Visual Studio 可用的默认键盘快捷键。 有关详细信息，请参阅以下页面：

- [标识并自定义键盘快捷方式](identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md)
- [如何以独占方式使用键盘](reference/how-to-use-the-keyboard-exclusively.md)
- [Visual Studio 中的键盘快捷方式](default-keyboard-shortcuts-in-visual-studio.md)

Visual Studio还包括方法和参数的自动完成;有关详细信息，请参阅 [Visual Studio 中的 IntelliSense](using-intellisense.md)。

::: moniker range="vs-2017"

> [!TIP]
> 若要详细了解最新的辅助功能更新，请参阅博文 [Visual Studio 2017 版本 15.3 中的辅助功能改进](https://devblogs.microsoft.com/visualstudio/accessibility-improvements-in-visual-studio-2017-version-15-3/)。

::: moniker-end

可以通过更多方法自定义Visual Studio，使你更易于访问。 例如，可以更改弹出窗口、基于文本的工具窗口、工具栏按钮、边距指示器等的行为。

> [!NOTE]
> 显示的对话框和菜单命令可能与此处的描述不同，具体取决于你的当前设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[重置设置](environment-settings.md#reset-settings)。

#### <a name="change-the-behavior-of-pop-up-windows"></a>更改弹出窗口的行为

Visual Studio在编辑器中显示弹出窗口。 这些弹出窗口包括使编码更容易的信息，例如用于完成函数或语句的参数。 如果键入困难，弹出窗口也很有用。 但是，某些用户可能会发现它们干扰代码编辑器中的焦点，这可能会造成问题。

下面介绍如何关闭弹出窗口：

1. 从“工具”菜单中选择“选项”。

1. 依次选择“文本编辑器” > “所有语言” > “常规”  。

1. 清除“自动列出成员”和“参数信息”复选框。

可以在集成开发环境 (IDE) 中重新排列窗口，以最适合的方式开展工作。 可以停靠、浮动、隐藏或自动隐藏每个工具窗口。 有关如何更改窗口布局的详细信息，请参阅[自定义窗口布局](customizing-window-layouts-in-visual-studio.md)。

#### <a name="change-the-settings-of-text-based-tool-windows"></a>更改基于文本的工具窗口的设置

可以更改基于文本的工具窗口的设置，例如“命令”窗口、“即时”窗口和“输出”窗口，方法是使用“工具” > “选项” > “环境” > “字体和颜色”。

在“显示以下内容的设置”下拉列表中选中“[全部文本工具窗口]”时，默认设置会在“项前景”和“项背景”下拉列表中作为“默认值”列出。 选择“自定义”按钮可以更改这些设置。

还可以更改编辑器中文本显示方式的设置。 操作方法如下。

1. 从“工具”菜单中选择“选项”。

1. 选择“环境” > “字体和颜色” 。

1. 在“显示其设置”下拉菜单中选择一个选项。

    若要更改编辑器中文本的字号，请选择“文本编辑器”。

    若要更改基于文本的工具窗口中文本的字号，请选择“[全部文本工具窗口]”。

    若要更改编辑器中工具提示文本的字号，请选择“编辑器工具提示”。

    若要更改语句完成弹出消息中文本的字号，请选择“语句完成”。

1. 从“显示项”中选择“纯文本”。

1. 在“字体”中选择一个新的字体类型。

1. 在“大小”中选择一个新的字号。

    > [!TIP]
    > 若要重置基于文本的工具窗口和编辑器的文本大小，请选择“使用默认值”。

7. 选择 **“确定”** 。

#### <a name="change-the-colors-for-text-margin-indicators-white-space-and-code-elements"></a>更改文本、边距指示器、空格和代码元素的颜色

可以选择更改编辑器中文本、边距指示器、空格和码位元素的默认颜色。 操作方法如下。

1. 从“工具”菜单中选择“选项”。

1. 在“环境”文件夹中选择“字体和颜色”。

1. 在“显示其设置”中选择“文本编辑器”。

1. 从“显示项”中选择要更改其显示方式的项，例如“纯文本”、“指示器边距”、“可见空白”、“HTML 特性名”或“XML 特性”。

1. 从下列选项中选择显示设置：“项前景”、“项背景”和“粗体”。

1. 选择 **“确定”** 。

> [!TIP]
> 若要对操作系统上的所有应用程序窗口使用高对比度的颜色，请按左 Alt + 左 Shift + PrtScn  。 如果 Visual Studio 处于打开状态，请关闭并重新打开它以完全实现高对比度的颜色。

#### <a name="add-text-to-toolbar-buttons-or-modify-the-text"></a>向工具栏按钮添加文本或修改文本

为了提高工具栏的可用性和易用性，可以向工具栏按钮添加文本。

###### <a name="to-assign-text-to-toolbar-buttons"></a>为工具栏按钮指定文本

1. 在“工具”菜单中选择“自定义”。

1. 在“自定义”对话框中选择“命令”选项卡。

1. 选择“工具栏”，然后选择包含要显示其文本的按钮的工具栏名称。

1. 在列表中，选择要更改的命令。

1. 选择“修改所选内容”。

1. 选择“图像和文本”。

###### <a name="to-modify-the-displayed-text-in-a-button"></a>修改按钮中的显示文本

1. 重新选择“修改所选内容”。

1. 在“名称”旁边为选定的按钮插入一个新标题。

### <a name="accessibility-support"></a>辅助功能支持

有关使残障人士Windows更易于访问的功能、产品和服务的详细信息，请参阅 [Microsoft 提供的辅助功能产品和服务](reference/accessibility-products-and-services-from-microsoft.md)。 有关如何获取 Microsoft 产品的更易于访问的文档格式的详细信息，请参阅 [Microsoft 页面辅助功能产品和服务](reference/accessibility-products-and-services-from-microsoft.md)的["替代格式](reference/accessibility-products-and-services-from-microsoft.md#documentation-in-alternative-formats)"部分的文档。

此页面中包含的辅助功能信息可能仅适用于在美国中许可 Microsoft 产品的用户。 如果你在美国之外获得本产品，请访问 [Microsoft 辅助功能](https://www.microsoft.com/accessibility/)网站，以获取 Microsoft 支持服务电话号码和地址的列表。 你可以与当地的分公司联系，了解你所在的地区是否供应本页所描述的产品和服务类型。 有关辅助功能的信息还有其他语言版本。

## <a name="see-also"></a>另请参阅

- [Visual Studio 代码编辑器的功能](../ide/writing-code-in-the-code-and-text-editor.md)
- [个性化设置 Visual Studio IDE 和编辑器](../ide/quickstart-personalize-the-ide.md)

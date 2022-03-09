---
title: 更改主题、字体、文本和对比度以提供辅助功能
description: 了解如何更改 Visual Studio 颜色主题、字体颜色、文本大小和额外的对比度颜色，以提供辅助功能。
ms.date: 02/28/2022
ms.topic: how-to
ms.custom: contperf-fy21q1
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
ms.openlocfilehash: a810d7cea8665e94c5d1bc6a91fb922b89c473a2
ms.sourcegitcommit: edf8137cd90c67b6078a02c93094f7e1c3bf8930
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2022
ms.locfileid: "139551204"
---
# <a name="how-to-change-fonts-colors-and-themes-in-visual-studio"></a>如何：在 Visual Studio 中更改字体、颜色和主题

::: moniker range=">=vs-2022"

可以通过多种方式在 Visual Studio 中更改字体和颜色。 例如，你可以将默认的深色主题（也称为“深色模式”）更改为浅色主题、蓝色主题、额外对比度主题或与系统设置相匹配的主题。 另外，还可以在 IDE 和代码编辑器中更改默认字体和文本大小。

> [!TIP]
> 请参阅[我们在 Visual Studio 2022 中升级了 UI](https://devblogs.microsoft.com/visualstudio/weve-upgraded-the-ui-in-visual-studio-2022/) 博客文章，详细了解我们对颜色对比度作出的细微调整和添加的新 Cascadia Code 字体，以便每个人都能更轻松地使用 Visual Studio。

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

若要详细了解如何在代码编辑器中更改字体和颜色，请参阅更改编辑器 [的字体和颜色](../ide/reference/how-to-change-fonts-and-colors-in-the-editor.md) 页。 有关 UI 的所有用户界面的详细信息 (用户界面) 更改字体和配色方案的元素，请参阅"字体和颜色，环境，选项" [对话框](../ide/reference/fonts-and-colors-environment-options-dialog-box.md) 页。

## <a name="accessibility-options"></a>辅助功能选项

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

### <a name="more-accessibility-features-in-visual-studio"></a>更多辅助功能Visual Studio

除了字体和颜色辅助功能之外，下面还有一些使残障人士Visual Studio辅助功能的功能：

- 键盘快捷方式控件和自定义项;请参阅[如何以独占方式使用键盘](reference/how-to-use-the-keyboard-exclusively.md)[和键盘](default-keyboard-shortcuts-in-visual-studio.md)Visual Studio。

- 方法和参数的自动完成;请参阅[中的 IntelliSense](using-intellisense.md) Visual Studio。

有关使残障人士更容易Windows功能、产品和服务的信息，请参阅 Microsoft 的辅助功能[产品和服务](reference/accessibility-products-and-services-from-microsoft.md)。 此外，若要详细了解如何获取 Microsoft 产品的更易于访问的文档格式，请参阅 Microsoft 中辅助功能产品和服务的备用[格式文档部分](reference/accessibility-products-and-services-from-microsoft.md)页。[](reference/accessibility-products-and-services-from-microsoft.md#documentation-in-alternative-formats)

### <a name="accessibility-support"></a>辅助功能支持

此页上包含的辅助功能信息可能仅适用于在 美国 中许可 Microsoft 产品的用户。 如果你在美国之外获得本产品，请访问 [Microsoft 辅助功能](https://www.microsoft.com/accessibility/)网站，以获取 Microsoft 支持服务电话号码和地址的列表。 你可以与当地的分公司联系，了解你所在的地区是否供应本页所描述的产品和服务类型。 有关辅助功能的信息还有其他语言版本。

## <a name="see-also"></a>另请参阅

- [Visual Studio 代码编辑器的功能](../ide/writing-code-in-the-code-and-text-editor.md)
- [个性化设置 Visual Studio IDE 和编辑器](../ide/quickstart-personalize-the-ide.md)
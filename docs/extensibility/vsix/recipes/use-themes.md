---
title: 主题设置
description: 了解如何使用 WPF 控件来主题窗口和其他 XAML 控件来匹配Visual Studio的颜色主题。
ms.date: 12/01/2021
ms.topic: conceptual
author: madskristensen
ms.author: madsk
manager: pchapman
ms.prod: visual-studio-windows
ms.technology: vs-ide-sdk
ms.custom: cookbook, kr2b-contr-experiment
ms.openlocfilehash: a19dc64e6bf8e27ee14d59e7b90f13b5ab4d3026
ms.sourcegitcommit: fec993dbfc5cbe94ca5c5845cb6c1b17b46160fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/25/2022
ms.locfileid: "145859248"
---
# <a name="matching-visual-studio-themes-in-visual-studio-extensions"></a>在Visual Studio扩展中匹配Visual Studio主题

 [!INCLUDE [Visual Studio](~/includes/applies-to-version/vs-windows-only.md)]

每当使用 WPF 生成任何自定义 UI 时，都需要确保它与Visual Studio主题匹配。 这样，UI 就会看起来是本机的，感觉更像是Visual Studio的自然部分。 否则，工具窗口和对话框最终可能会在浅色主题中如下所示：

:::image type="content" source="../media/theming-light-none.png" alt-text="显示不使用 W P F 控件的浅色主题的窗口的屏幕截图。":::

请注意文本框和按钮的填充看起来不正确？ 深色主题中的情况会变得更糟：

:::image type="content" source="../media/theming-dark-none.png" alt-text="显示不使用 W P F 控件的深色主题的窗口的屏幕截图。":::

现在，文本和背景色几乎无法阅读。 不好。

有一种简单的方法可以确保 UI 的背景色、按钮样式等与Visual Studio的背景色、按钮样式等匹配。 这样，同一 UI 就可以在浅色主题中如下所示：

:::image type="content" source="../media/theming-light.png" alt-text="显示正确使用控件和浅色主题的窗口的屏幕截图。":::

或在深色主题中：

:::image type="content" source="../media/theming-dark.png" alt-text="显示正确使用控件和深色主题的窗口的屏幕截图。":::

这看起来好多了。 让我们看看如何对 UI 进行主题化。

## <a name="wpf-usercontrol"></a>WPF UserControl
下面是一个 WPF 示例，该 WPF `<UserControl>` 可以直接在工具窗口中使用。

```xml
<UserControl x:Class="TestExtension.RunnerWindowControl"
             xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
             xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
             xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
             xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
             xmlns:toolkit="clr-namespace:Community.VisualStudio.Toolkit;assembly=Community.VisualStudio.Toolkit"
             toolkit:Themes.UseVsTheme="True">
```

请注意导入的 `xmlns:toolkit` 命名空间和 `toolkit:Themes.UseVsTheme="True"` 属性。 它们将自动为Visual Studio使用的 WPF 控件应用官方样式。 我们不必执行任何其他操作才能将样式应用于整个 `<UserControl>`样式。 简单！

另一个好处是，当用户将颜色主题从浅色更改为深色时，UI 也会立即切换，而无需重新加载。

## <a name="dialogwindow-control"></a>DialogWindow 控件
Visual Studio附带了可用于自定义窗口（即控件）的`DialogWindow`控件。 建议将它用于任何对话框窗口，但它也可以在工具窗口中使用。

它与其他 XAML 窗口类型非常相似。

```xml
<platform:DialogWindow 
    x:Class="TestExtension.ThemeWindowDialog"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:platform="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.15.0"
    xmlns:toolkit="clr-namespace:Community.VisualStudio.Toolkit;assembly=Community.VisualStudio.Toolkit"
    toolkit:Themes.UseVsTheme="True">
```

请注意工具包和平台和属性 `toolkit:Themes.UseVsTheme="True"`的导入命名空间。

以上是其中包含的全部内容。 对话窗口现在使用Visual Studio颜色和样式主题。

## <a name="get-the-source-code"></a>获取源代码
可以在[Community Toolkit测试项目中](https://github.com/VsixCommunity/Community.VisualStudio.Toolkit/tree/master/demo/VSSDK.TestExtension)找到此扩展的源代码。

## <a name="additional-resources"></a>其他资源
详细了解这些资源中的Visual Studio颜色。

* [Visual Studio的颜色和样式](../../ux-guidelines/colors-and-styling-for-visual-studio.md)
* [Visual Studio的共享颜色](../../ux-guidelines/shared-colors-for-visual-studio.md)
* [颜色值参考](../../ux-guidelines/color-value-reference-for-visual-studio.md)

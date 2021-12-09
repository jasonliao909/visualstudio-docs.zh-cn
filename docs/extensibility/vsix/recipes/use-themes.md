---
title: 主题设置
description: 如何正确主题工具窗口和其他 XAML 控件，Visual Studio的颜色主题。
ms.date: 12/01/2021
ms.topic: conceptual
author: madskristensen
ms.author: madsk
manager: pchapman
ms.prod: visual-studio-windows
ms.technology: vs-ide-sdk
ms.custom: cookbook
ms.openlocfilehash: 1a99d49615a51f4bbbf7372ef15795b178dd6a88
ms.sourcegitcommit: ba40c6208b2cb27d047fec4fa2c83c6be4f9ee5a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/09/2021
ms.locfileid: "134463497"
---
# <a name="matching-visual-studio-themes-in-visual-studio-extensions"></a>匹配Visual Studio扩展Visual Studio主题

每当使用 WPF 生成任何自定义 UI 时，都需要确保它与 WPF 的Visual Studio。 这样一来，UI 将看起来本机，并感觉更像一个自然Visual Studio。 如果没有，工具窗口和对话框最终可能在浅色主题中如下所示：

:::image type="content" source="../media/theming-light-none.png" alt-text="浅色主题中的非主题 UI。":::

请注意文本框和按钮周围的填充看起来如何不对？ 在"深色"主题中，情况更差：

:::image type="content" source="../media/theming-dark-none.png" alt-text="深色主题中的非主题 UI。":::

现在，文本和背景色几乎无法读取。 不好。

有一种简单的方法，确保 UI 的背景色、按钮样式等与Visual Studio一点小技巧匹配。 这样，相同的 UI 在浅色主题中可能如下所示：

:::image type="content" source="../media/theming-light.png" alt-text="浅色主题中正确主题的 UI。":::

或在深色主题中：

:::image type="content" source="../media/theming-dark.png" alt-text="深色主题中正确主题的 UI。":::

这看起来要更好。 让我们看看如何为 UI 设置主题。

## <a name="wpf-usercontrol"></a>WPF UserControl
下面是可直接在工具窗口中使用的 WPF `<UserControl>` 示例。

```xml
<UserControl x:Class="TestExtension.RunnerWindowControl"
             xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
             xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
             xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
             xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
             xmlns:toolkit="clr-namespace:Community.VisualStudio.Toolkit;assembly=Community.VisualStudio.Toolkit"
             toolkit:Themes.UseVsTheme="True">
```

请注意 `xmlns:toolkit` 导入的命名空间和 `toolkit:Themes.UseVsTheme="True"` 属性。 它们会自动为自己使用的 WPF 控件Visual Studio样式。 我们不必执行任何其他操作来将样式应用于整个 `<UserControl>` 。 简单！

另一个好处是，当用户将颜色主题从浅色更改到深色时，UI 也会立即切换，而无需重新加载。

## <a name="dialogwindow-control"></a>DialogWindow 控件
Visual Studio附带一个控件，我们可用于自定义窗口，即 `DialogWindow` 控件。 建议对任意对话框窗口使用该窗口，但也可在工具窗口内使用它。

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

请注意工具包和平台以及 属性 的导入命名空间 `toolkit:Themes.UseVsTheme="True"` 。

就这么简单。 现在，对话框窗口使用颜色Visual Studio样式进行主题设置。

## <a name="get-the-source-code"></a>获取源代码
可以在测试项目 中查找此扩展[Community Toolkit源代码](https://github.com/VsixCommunity/Community.VisualStudio.Toolkit/tree/master/demo/VSSDK.TestExtension)。

## <a name="additional-resources"></a>其他资源
详细了解这些资源Visual Studio颜色。

* [样式的颜色和Visual Studio](../../ux-guidelines/colors-and-styling-for-visual-studio.md)
* [共享颜色Visual Studio](../../ux-guidelines/shared-colors-for-visual-studio.md)
* [颜色值参考](../../ux-guidelines/color-value-reference-for-visual-studio.md)

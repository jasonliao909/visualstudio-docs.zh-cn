---
title: Visual Studio for Mac IDE 和 macOS 中的辅助功能选项
description: 介绍 Visual Studio for Mac 中的辅助功能及其启用方法。 此外，还了解如何在 Visual Studio for Mac 中使用 macOS 辅助功能选项和功能，例如高对比度、键盘导航和 VoiceOver
author: jmatthiesen
ms.author: jomatthi
manager: dominicn
ms.date: 02/23/2022
ms.assetid: 2C4AAC2E-3B4A-4496-8BE0-1F5A7F81D1CA
ms.topic: overview
ms.openlocfilehash: 872d1f24a89c29f8599b410350fb97d9bfda4c54
ms.sourcegitcommit: fcf47a9c356df7e9636bcab92186923e5c9b8892
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/30/2022
ms.locfileid: "144516305"
---
# <a name="accessibility"></a>可访问性

 [!INCLUDE [Visual Studio for Mac](~/includes/applies-to-version/vs-mac-only.md)]

macOS 中内置了许多可在你使用 Visual Studio for Mac 时提供帮助的辅助工具和功能。 这些功能包括高对比度模式、键盘导航和 VoiceOver（macOS 屏幕读取器）。

除此之外，Visual Studio for Mac 还提供了以下功能，使用户能够更轻松地访问各种功能：

* 编辑器文本放大
* 工具窗口文本放大
* 代码编辑器颜色主题自定义
* 键盘快捷方式自定义
* 键盘导航

本文介绍如何使用 macOS 辅助功能，以及如何在 Visual Studio for Mac IDE 中设置辅助功能选项。

> [!NOTE]
> 本指南适用于 Visual Studio for Mac。 有关 Windows 上的 Visual Studio，请参阅 [Visual Studio 的辅助功能](/visualstudio/ide/reference/accessibility-features-of-visual-studio)。

::: moniker range="vsmac-2019"
## <a name="enable-macos-accessibility-features-in-visual-studio-for-mac"></a>在 Visual Studio for Mac 中启用 macOS 辅助功能

默认情况下，Visual Studio for Mac 对辅助技术的支持处于禁用状态。 启用辅助功能支持：

1. 转到 **Visual Studio (菜单)** > **首选项** > **“其他**”，然后选择“**辅助功能**”。

1. 选择“启用辅助功能”  复选框。

   ![辅助功能首选项的屏幕截图，其中选择了“启用辅助功能”](media/accessibility-preferences.png)

1. 选择“重启 Visual Studio”  ，以启用对 Apple 辅助技术的支持。

也可以使用命令行启用辅助功能。 为此，请在终端中输入以下命令：

```bash
defaults write com.microsoft.visual-studio com.monodevelop.AccessibilityEnabled 1
```

通过命令行更改此设置后，需要重启 Visual Studio。

::: moniker-end

## <a name="increase-the-contrast-in-macos"></a>提高 macOS 中的对比度

Visual Studio for Mac 支持 macOS 中提高的对比度，可提高 UI 元素的对比度并使轮廓更明确。 启用此项：

1. 打开“系统首选项”。

1. 转到“辅助功能”，然后选择“显示”。

1. 选择“增加对比度”复选框。

## <a name="resize-tool-windows-and-editor-content"></a>对工具窗口和编辑器内容重设大小

1. 选择要对其内容重设大小的工具窗口或编辑器窗口。

1. 选择“视图(菜单)”  ，然后选择“放大(&#8984;+)”  或“缩小(&#8984;-)”  。

> [!TIP]
> 若要将内容重置为默认大小，可以选择“视图(菜单)”   > “常规大小(&#8984;0)”  。

## <a name="change-the-content-font-and-size"></a>更改内容的字体和大小

在 Visual Studio for Mac 中，可以自定义大多数工具窗口内容的字体和大小。 以下是操作方法：

1. 转到“Visual Studio (菜单)”   > “首选项... (&#8984;,)”  。

1. 在“首选项”  中，转到“环境”   > “字体”  。

1. 对于“文本编辑器”、“常规工具窗口文本”或“输出窗口内容”，选择“字体和大小”按钮。

1. 选择所需的字体、样式和大小，然后选择“确定”  。

> [!TIP]
> 若要返回到每个设置的默认字体和样式，请选择“设置为默认值”  。

## <a name="change-the-editor-syntax-highlighting"></a>更改编辑器语法突出显示

某些用户可能会发现默认配色方案不符合其对比度或颜色要求。 Visual Studio for Mac 具有多个用户可以选择的替代主题，其中包括两个高对比度主题。

1. 转到“Visual Studio (菜单)”   > “首选项... (&#8984;,)”  。

1. 在“首选项”  中，转到“文本编辑器”   > “颜色主题”  。

1. 选择所需的主题。

> [!TIP]
> 主题将实时在编辑器中进行更新，因此你可以预览并选择你的首选主题。

有关详细信息，请参阅以下主题：

* [使用键盘导航](accessibility-keyboard.md)
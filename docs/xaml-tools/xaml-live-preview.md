---
title: 通过 XAML 实时预览捕获和编辑桌面应用 UI
description: 将 xaml 实时预览与 xaml 热重载配对，以捕获桌面应用 UI，在 Visual Studio 中对其进行迭代更改，然后实时查看这些更改。
ms.date: 11/08/2021
ms.topic: conceptual
helpviewer_keywords:
- xaml edit
- xaml live preview
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-xaml-tools
ms.workload:
- multiple
monikerRange: vs-2022
ms.openlocfilehash: 0f5839bc7f05afb4f4e91db4608a9b30687aca8d
ms.sourcegitcommit: 67dc39e93c86ba50eb5ca877b0471fb8ab8475ac
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/08/2021
ms.locfileid: "132002129"
---
# <a name="xaml-live-preview-capture-and-edit-desktop-app-ui"></a>XAML 实时预览：捕获和编辑桌面应用程序 UI

使用 xaml 实时预览，你可以)  (UI 捕获桌面应用的用户界面，并将其引入到 Visual Studio 内的停靠窗口中，这样可以更轻松地使用[XAML 热重载](xaml-hot-reload.md)来更改应用，然后在你进行更改时实时查看这些更改。

:::image type="content" source="media/vs-2022/xaml-live-preview.gif" alt-text="显示 XAML 实时预览的操作的动画。":::

## <a name="xaml-live-preview-window"></a>XAML 实时预览窗口

XAML 实时预览窗口在调试过程中可用。 若要打开它，请参阅 **调试**  >  **Windows**  >  **XAML 实时预览**。

:::image type="content" source="media/vs-2022/xaml-live-preview-menu.png" alt-text="&quot;调试&quot; 菜单栏中的 &quot;XAML 实时预览&quot; 选项的屏幕截图。":::

或者，在 "应用程序" 工具栏中选择 " **在 XAML 实时预览中显示** " 按钮。

:::image type="content" source="media/vs-2022/xaml-live-preview-toolbar.png" alt-text="应用程序工具栏上的 XAML 实时预览选项的屏幕截图。":::

### <a name="scrolling-and-zooming"></a>滚动和缩放

除滚动条外，还可以使用下列交互：

- 如果鼠标支持) ，则为垂直和水平滚动 (条。
- 触摸板双指垂直和水平滚动。
- 按下 **Ctrl** 键的同时按下了鼠标拖动操作。

对于缩放，还可以使用下列交互：

- 左下角的 "放大/缩小" 按钮。
-  + 如果喜欢使用键盘，请按 ctrl **+ sign** (+) 或 **ctrl** + **减号** (-) 键盘快捷方式。
- 按下 **Ctrl** 键与鼠标滚轮操作配对，或使用触摸板缩放操作。 使用鼠标的额外优点是维护着一个控件区域。

:::image type="content" source="media/vs-2022/xaml-live-preview-scroll-zoom.gif" alt-text="XAML 实时预览中滚动和缩放操作的动画。":::

### <a name="element-selection"></a>元素选择

XAML 实时预览中的元素选择类似于正在运行的应用程序中的选择。 它允许您在实时可视化树或源 XAML 中查找元素。

:::image type="content" source="media/vs-2022/xaml-live-preview-element-selection.gif" alt-text="XAML 实时预览中元素选择操作的动画。":::

元素选择由 (从左到右) 的前四个工具栏按钮控制。

:::image type="content" source="media/vs-2022/xaml-live-preview-toolbar-selection.png" alt-text="用于元素选择的 XAML 实时预览工具栏按钮的屏幕截图。":::

工具栏按钮将生成以下操作：

- **元素选择** 启动元素选择操作;换句话说，当你将鼠标移到 XAML 实时预览中的应用程序内容上时，它将突出显示元素。 单击某个元素时，它会在 "实时可视化树" 中被选中。 如果启用了 **预览选定元素** ，则它还会导航到源，并且源 XAML 可用。 此行为与在 "实时可视化树" 中的行为相同。
- 在 **选择过程中显示元素信息** 是一个切换按钮，用于控制鼠标下元素的大小、颜色和字体信息的显示。
- **"仅我的 XAML"** 是一个切换按钮，用于控制要突出显示的元素：全部，或仅用于解决方案中可用的源 XAML 的元素。 此行为与在 "实时可视化树" 中的行为相同。
- **预览选定项** 是一个切换按钮，用于控制在选择元素时导航到源 XAML。 默认情况下，此功能处于关闭状态。 此行为与在 "实时可视化树" 中的行为相同。

### <a name="rulers"></a>标尺

标尺有助于在应用程序中对齐元素。 它们在应用程序单位中显示与上一个标尺之间的距离。 通过这种方式，它们有助于验证应用程序的不同部分之间的距离。

:::image type="content" source="media/vs-2022/xaml-live-preview-rulers.gif" alt-text="操作中标尺的动画。":::

第二组工具栏按钮控制标尺，如下 (从左到右) ：

:::image type="content" source="media/vs-2022/xaml-live-preview-toolbar-rulers.png" alt-text="XAML 实时预览中第二组标尺工具栏按钮的屏幕截图。":::

- **添加垂直标尺**。 添加单个垂直标尺。 如果在一行中多次单击此按钮，则它将放置新标尺，使其不会与现有标尺重叠。
- **添加水平标尺**。 添加单个水平标尺，类似于垂直标尺。
- **删除所有标尺**。 删除所有标尺。
- **选择 "标尺颜色**"。 更改标尺的颜色。
- **切换标尺可见性**。 只单击一次即可隐藏或显示所有标尺。

标尺适合键盘。 您可以按 tab。 您可以使用箭头键，一次一个像素地移动标尺，或按 **Ctrl** 与箭头键配对，一次移动10个应用单元。 **Del** 键删除当前所选标尺。 还可以通过选择标签附近的 " **删除标尺** " 按钮，使用鼠标删除标尺。

使用元素选择时，还可以在元素周围添加标尺。 右键单击会添加垂直标尺。 若要添加水平标尺，请在右键单击时选择并按住 **Shift** 键。

:::image type="content" source="media/vs-2022/xaml-live-preview-outline-rulers.gif" alt-text="以及如何在 XAML 实时预览中将标尺添加到图像的轮廓的动画。":::

### <a name="multi-window-applications"></a>多窗口应用程序

如果你的应用程序具有多个窗口，则可以使用 "窗口" 组合框选择要显示的窗口。 或者，使用你要预览的窗口中的应用程序工具栏上的 " **在 XAML 中显示" 实时预览** 按钮。

:::image type="content" source="media/vs-2022/xaml-live-preview-change-window.gif" alt-text="XAML 实时预览中多窗口应用程序功能的动画。":::

## <a name="supported-platforms"></a>受支持的平台

Visual Studio 2022 的初始版本支持以下平台和调试方案。

|平台  |元素选择 & 信息提示  |标尺  |
|---------|---------|---------|
|WPF      |是         |是         |
|UWP      |是         |是         |
|WinUI3 桌面     |否         |是         |
|MAUI (Android Emulator)      |否         |是 (px * )          |
|Xamarin 5.0 + (Android Emulator)      |否          |是 (px * )          |

> [!NOTE]
> 在上表中， ( * * px * * * ) 指示以像素为单位显示的标尺;所有其他平台都显示平台单元中的信息，它们依赖于监视器的 DPI。

## <a name="limitations"></a>限制

XAML 实时预览的工作原理是，每秒捕获一次应用程序屏幕截图，并使用可用的 Api （如 [PrintWindow](/windows/win32/api/winuser/nf-winuser-printwindow)）。 这会受到以下限制：

- 如果应用窗口的某个部分处于关闭屏幕，则该部分不可能显示 XAML 热重载更改。
- &mdash; &mdash; 使用带有 DWMWA_CLOAK WDA_EXCLUDEFROMCAPTURE 或[DwmSetWindowAttribute](/windows/win32/api/dwmapi/nf-dwmapi-dwmsetwindowattribute)的[SetWindowDisplayAffinity](/windows/win32/api/winuser/nf-winuser-setwindowdisplayaffinity) ，窗口可以选择退出截图捕获并使其变得不可用。

## <a name="next-steps"></a>后续步骤

详细了解 [Xaml 热重载](xaml-hot-reload.md)，它们与 Xaml 实时预览非常类似。

## <a name="see-also"></a>请参阅

[Visual Studio 2022 发行说明](/visualstudio/releases/2022/release-notes-preview)

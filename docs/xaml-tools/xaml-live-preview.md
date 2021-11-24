---
title: 使用 XAML 实时预览捕获和编辑桌面应用 UI
description: 结合使用 XAML 实时预览与 XAML 热重载以捕获桌面应用 UI，以便在 Visual Studio 中对其进行迭代更改并实时查看这些更改。
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
ms.openlocfilehash: ba6d69f631c89d933633a7b1262cd3081002b54b
ms.sourcegitcommit: 932cf0f653c6258b73f42102d134cbaf50b8f20c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2021
ms.locfileid: "132879748"
---
# <a name="xaml-live-preview-capture-and-edit-desktop-app-ui"></a>XAML 实时预览：捕获和编辑桌面应用 UI

借助 XAML 实时预览功能，可以捕获桌面应用的用户界面 (UI) 并将其引入到 Visual Studio 内的停靠窗口中，从而可以更轻松地使用 [XAML 热重载](xaml-hot-reload.md)来更改应用，然后在进行更改时实时查看这些更改。

:::image type="content" source="media/vs-2022/xaml-live-preview.gif" alt-text="显示正在使用 XAML 实时预览的动画。":::

## <a name="xaml-live-preview-window"></a>“XAML 实时预览”窗口

“XAML 实时预览”窗口在调试期间可用。 若要打开该窗口，请转到“调试” > “Windows” > “XAML 实时预览”  。

:::image type="content" source="media/vs-2022/xaml-live-preview-menu.png" alt-text="“调试”菜单栏中的“XAML 实时预览”选项的屏幕截图。":::

也可选择应用程序工具栏中的“在 XAML 实时预览中显示”按钮。

:::image type="content" source="media/vs-2022/xaml-live-preview-toolbar.png" alt-text="应用程序工具栏中的“XAML 实时预览”选项的屏幕截图。":::

### <a name="scrolling-and-zooming"></a>滚动和缩放

除了使用滚动条滚动外，也可使用以下交互工具：

- 鼠标滚轮，可垂直和水平滚动（如果鼠标支持）。
- 触摸板双指滚动，可垂直和水平滚动。
- 按住 Ctrl 键的同时进行鼠标拖动操作。

至于缩放，也可使用以下交互工具：

- 左下角的“放大”/“缩小”按钮。
- 按 Ctrl+加号 (+) 或 Ctrl+减号 (-) 键盘快捷键（如果更喜欢使用键盘）   。
- 按住 Ctrl 键的同时进行鼠标滚轮操作，或使用触摸板进行双指缩放操作。 使用鼠标的额外好处是可以保持控制区域。

:::image type="content" source="media/vs-2022/xaml-live-preview-scroll-zoom.gif" alt-text="XAML 实时预览中滚动和缩放操作的动画。":::

### <a name="element-selection"></a>元素选择

XAML 实时预览中的元素选择类似于正在运行的应用程序中的选择。 借助该功能，可在实时可视化树或源 XAML 中查找元素。

:::image type="content" source="media/vs-2022/xaml-live-preview-element-selection.gif" alt-text="XAML 实时预览中元素选择操作的动画。":::

元素选择由前四个工具栏按钮（从左到右）控制。

:::image type="content" source="media/vs-2022/xaml-live-preview-toolbar-selection.png" alt-text="用于元素选择的 XAML 实时预览工具栏按钮的屏幕截图。":::

工具栏按钮将执行以下操作：

- “元素选择”启动元素选择操作，也就是说，它在将鼠标移到 XAML 实时预览中的应用程序内容上时突出显示元素。 当你单击某个元素时，将在实时可视化树中选中该元素。 如果启用了“预览选定元素”且源 XAML 可用，它还会导航到源。 此行为与实时可视化树中的行为相同。
- “在选择过程中显示元素信息”是一个切换按钮，用于控制有关鼠标下方元素的大小、颜色和字体信息的显示。
- “仅我的 XAML”是一个切换按钮，用于控制要突出显示的元素：全部元素或仅具有解决方案中可用的源 XAML 的那些元素。 此行为与实时可视化树中的行为相同。
- “预览选定项”是一个切换按钮，用于在选择元素时控制到源 XAML 的导航。 此功能默认处于关闭状态。 此行为与实时可视化树中的行为相同。

### <a name="rulers"></a>标尺

标尺可帮助对齐应用程序中的元素。 它们显示与前一个标尺的距离（以应用程序为单位）。 通过这种方式，它们可用于验证应用程序不同部分之间的距离。

:::image type="content" source="media/vs-2022/xaml-live-preview-rulers.gif" alt-text="操作中标尺的动画。":::

第二组工具栏按钮控制标尺，如下所示（从左到右）：

:::image type="content" source="media/vs-2022/xaml-live-preview-toolbar-rulers.png" alt-text="XAML 实时预览中第二组标尺工具栏按钮的屏幕截图。":::

- 添加垂直标尺。 添加一个垂直标尺。 如果连续多次单击该按钮，它将放置新标尺，这样就不会与现有标尺重叠。
- 添加水平标尺。 添加一个水平标尺，它类似于垂直标尺。
- 删除所有标尺。 一次性删除所有标尺。
- 选择标尺颜色。 更改标尺的颜色。
- 切换标尺可见性。 单击即可隐藏或显示所有标尺。

标尺适用于键盘操作。 可以按 Tab 键绘制标尺。 可以使用箭头键将标尺一次移动一个像素，或者同时按住 Ctrl 和箭头键将其一次移动 10 个应用单位。 Del 键用于删除当前选定的标尺。 也可通过选择标签旁边的“删除标尺”按钮，使用鼠标删除标尺。

也可以在使用“元素选择”时在元素周围添加标尺。 右键单击将添加垂直标尺。 若要添加水平标尺，请在右键单击时选择并按住 Shift 键。

:::image type="content" source="media/vs-2022/xaml-live-preview-outline-rulers.gif" alt-text="如何在 XAML 实时预览中向图像轮廓添加标尺的动画。":::

### <a name="multi-window-applications"></a>多窗口应用程序

如果应用程序有多个窗口，则可以使用 Window 组合框选择要显示的窗口。 也可使用要预览的窗口上的应用程序工具栏中的“在 XAML 实时预览中显示”按钮。

:::image type="content" source="media/vs-2022/xaml-live-preview-change-window.gif" alt-text="XAML 实时预览中多窗口应用程序功能的动画。":::

## <a name="supported-platforms"></a>受支持的平台

Visual Studio 2022 的初始版本支持以下平台和调试方案。

|平台  |元素选择和信息提示  |标尺  |
|---------|---------|---------|
|WPF      |是         |是         |
|UWP      |是         |是         |
|WinUI3 桌面     |否         |是         |
|MAUI (Android Emulator)     |否         |是 (px*)         |
|Xamarin 5.0 + (Android Emulator)     |否          |是 (px*)         |

> [!NOTE]
> 上表中的 (px*****) 表示以像素为单位显示的标尺；所有其他平台以平台为单位显示信息，这取决于监视器的 DPI。

## <a name="limitations"></a>限制

XAML 实时预览的工作原理是每秒多次捕获应用程序屏幕截图，并使用 [PrintWindow](/windows/win32/api/winuser/nf-winuser-printwindow) 等可用 API。 该功能具有以下局限性：

- 如果应用窗口的某个部分不在屏幕上，则该部分将不会显示 XAML 热重载更改。
- 通过使用带有 WDA_EXCLUDEFROMCAPTURE 的 [SetWindowDisplayAffinity](/windows/win32/api/winuser/nf-winuser-setwindowdisplayaffinity) 或带有 DWMWA_CLOAK 的 [DwmSetWindowAttribute](/windows/win32/api/dwmapi/nf-dwmapi-dwmsetwindowattribute)，窗口可以选择退出屏幕截图捕获并且对于 XAML 实时预览变得不可用。

## <a name="next-steps"></a>后续步骤

详细了解 [XAML 热重载](xaml-hot-reload.md)，它可与 XAML 实时预览结合使用。

## <a name="see-also"></a>另请参阅

[Visual Studio 2022 发行说明](/visualstudio/releases/2022/release-notes)

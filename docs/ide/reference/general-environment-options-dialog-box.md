---
title: “选项”对话框 ->“环境”->“常规”
description: 了解如何通过“环境”部分的“常规”页来更改 IDE 的颜色主题、状态栏设置、文件扩展名关联等内容。
ms.custom: SEO-VS-2020
ms.date: 11/29/2021
ms.topic: reference
f1_keywords:
- VS.Environment.General
- VS.Message.0x800a002e
- VS.OptionsDialog.Environment
- VS.ToolsOptionsPages.Environment
- VS.ToolsOptionsPages.Environment.General
helpviewer_keywords:
- recently used file lists
- Windows menu, customizing
- status bar, displaying
- Options dialog box, General Environment
- General Environment Options dialog box
- Environment Options dialog box
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: 19c96e580a55c6b6a5deaf307fbe9e0653c7b0da
ms.sourcegitcommit: 28168514c0c9472e852de35cceb4f95837669da6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/30/2021
ms.locfileid: "133256966"
---
# <a name="options-dialog-box-environment--general"></a>“选项”对话框：环境 \> 常规

使用此页更改集成开发环境 (IDE) 的颜色主题、状态栏设置和文件扩展名关联以及其他选项。 可以通过打开“工具”菜单，选择“选项”，打开“环境”文件夹然后选择“常规”页来访问“选项”对话框。

## <a name="visual-experience"></a>视觉体验

颜色主题

为 IDE 选择“蓝色”、“浅色”、“深色”，或者“蓝色(额外对比度)”颜色主题。

::: moniker range="vs-2022"

还可以通过选择“使用系统设置”，选择使用 Windows 使用的主题。

::: moniker-end

可以通过下载并安装当前使用的版本的 Visual Studio 颜色主题设计器来安装其他预定义主题并创建自定义主题，如下所示：

- [2022 年Visual Studio主题设计器](https://marketplace.visualstudio.com/items?itemName=idex.colorthemedesigner2022)
- [Visual Studio 2019 的颜色主题设计器](https://marketplace.visualstudio.com/items?itemName=ms-madsk.ColorThemeDesigner)。
- [Visual Studio 2017 的颜色主题编辑器](https://marketplace.visualstudio.com/items?itemName=VisualStudioPlatformTeam.VisualStudio2017ColorThemeEditor)

安装此工具后，其他颜色主题将显示在“颜色主题”列表框中。

::: moniker range="vs-2022"

> [!NOTE]
> 想要更多的主题选项？ 在 [Visual Studio Marketplace](https://marketplace.visualstudio.com/search?target=VS&category=Tools&vsVersion=&subCategory=Themes&sortBy=Installs) 上查看各种自定义主题。 若要查看基于 VS Code 的新的 Visual Studio 2022 自定义主题的示例，请参阅[新的 Visual Studio 主题集合简介](https://devblogs.microsoft.com/visualstudio/custom-themes/)博客文章。

::: moniker-end

将词首字母大写样式应用到菜单栏

默认情况下，菜单使用词首字母大写样式。 取消选中此选项以改为使用所有大写样式。

::: moniker range=">=vs-2019"

使用不同像素密度优化屏幕呈现(需要重启)

此选项启用或禁用每监视器每英寸点数 (DPI) 识别功能（或 PMA）。 启用 PMA 后，Visual Studio 用户界面在任何监视器显示比例因子和 DPI 配置（包括跨多个监视器）中都清晰显示。 若要启用 PMA，需要 Windows 10 2018 年 4 月更新或更高版本以及 .NET Framework 4.8 或更高版本。 （如果不满足这两个系统必备项，此选项将显示为灰色。）

> [!TIP]
> - Windows 10 包含设置，指示“让 Windows 尝试修复应用，以便它们不再模糊”。 如果选中了“使用不同像素密度优化屏幕呈现”选项，则启用该 Windows 设置的效果可以忽略不计。
> - Windows 10 还包括“程序兼容性疑难解答”。 不建议尝试使用该疑难解答修复 Visual Studio 外观。

::: moniker-end

基于客户端性能自动调整视觉体验

指定由 Visual Studio 自动设置视觉体验调整，还是由你明确地设置调整。 这种调整可能会将颜色的显示从渐变更改为纯色，也可能会限制菜单或弹出窗口中动画的使用。

::: moniker range="vs-2017"

> [!TIP]
> Windows 10 包含设置，指示“让 Windows 尝试修复应用，以便它们不再模糊”。 如果 Visual Studio 在显示器上模糊显示，建议启用该设置。 请考虑升级到 [Visual Studio 2019](https://visualstudio.microsoft.com/downloads)，该版本大大提高了显示清晰度，因为它是每显示器每英寸点数感知应用程序。

::: moniker-end

启用丰富客户端体验

启用 Visual Studio 的完整视觉体验，包括渐变和动画。 使用远程桌面连接或较旧的图形适配器时，请清除此选项，因为在这些情况下这些功能可能会使性能变差。 只有在清除了“基于客户端自动调整视觉体验”选项时，此选项才可用。

使用硬件图形加速（如果可用）

如果可用，请使用硬件图形加速，而不是软件加速。

## <a name="other"></a>其他

要在窗口菜单中显示的项

自定义“窗口”菜单的“窗口”列表中显示的窗口数。 请输入一个介于 1 和 24 之间的数字。 默认值为 10。

“最近使用的文件”列表中显示的项

自定义出现在“文件”菜单上的最近使用过的项目和文件数。 请输入一个介于 1 和 24 之间的数字。 默认值为 10。 这可以轻松地检索最近使用的项目和文件。

显示状态栏

显示状态栏。 状态栏位于 IDE 窗口的底部并显示关于正在进行的操作的进度信息。

**“关闭”按钮只影响活动工具窗口**

指定在单击“关闭”按钮时，只关闭具有焦点的工具窗口，而不是停靠集中的所有工具窗口。 默认情况下选择此选项。

**“自动隐藏”按钮只影响活动工具窗口**

指定在单击“自动隐藏”按钮时，只自动隐藏具有焦点的工具窗口，而不是停靠集中的所有工具窗口。 默认情况下，不选择该选项。

## <a name="see-also"></a>另请参阅

- [自定义窗口布局](../../ide/customizing-window-layouts-in-visual-studio.md)

---
title: 适用于 WPF 热重载 UWP 应用的 XAML 应用
description: XAML 热重载（或 XAML 编辑并继续）允许你在运行应用时对 XAML 代码进行更改
ms.date: 02/25/2022
ms.topic: conceptual
helpviewer_keywords:
- xaml edit and continue
- xaml hot reload
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.custom: contperf-fy22q1
ms.technology: vs-xaml-tools
ms.workload:
- multiple
monikerRange: '>=vs-2019'
ms.openlocfilehash: 4c93455957322a0c5abe6d35a0d4dfb71e2594b1
ms.sourcegitcommit: 4e0efca10b152418a4c924dbf2462e3da6094597
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2022
ms.locfileid: "141252483"
---
# <a name="what-is-xaml-hot-reload-for-wpf-and-uwp-apps-visual-studio"></a>什么是 WPF 热重载 UWP 应用的 XAML 应用？  (Visual Studio) 

使用 XAML 热重载，可以增量生成和测试 WPF 和 UWP 应用的 XAML 代码。 为此，可以受益于正在运行的应用的数据上下文、身份验证状态和其他在设计时难以模拟的实际复杂性。

> [!TIP]
> 如果你是通过 XAML 热重载用户界面 (UI) 来到这里的，欢迎你的到来！ 你来对了地方，这里非常适合详细了解 XAML 热重载。
>
> 但是，如果你在此处寻求排查 XAML 热重载的相关帮助，请改为参阅 [XAML 热重载故障排除](xaml-hot-reload-troubleshooting.md)。

## <a name="where-to-get-xaml-hot-reload"></a>在何处获取 XAML 热重载

Visual Studio XAML 热重载当前仅在 **Visual Studio - 或** **- Blend for Visual Studio** 中运行应用程序，但调试器已连接到  **(F5** 或启动调试) 。

[除非手动设置环境变量](xaml-hot-reload-troubleshooting.md#verify-that-you-use-start-debugging-rather-than-attach-to-process)，否则无法通过使用[附加到进程](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)来启用此体验。

## <a name="applications-for-xaml-hot-reload"></a>XAML 应用程序热重载

XAML 热重载在以下情况中尤其有用：

* 修复在调试模式下启动应用后在 XAML 代码中发现的 UI 问题。

* 为开发中的应用生成新的 UI 组件，同时利用应用的运行时上下文。

## <a name="supported-os"></a>支持的 OS

|支持的应用程序类型|操作系统和工具|
|-|-|-|
|Windows Presentation Foundation (WPF) |.NET Framework 4.6 及更高版本和 .NET Core</br>Windows 7 及更高版本 |
|通用 Windows 应用 (UWP)|Windows 10 及更高版本，以及  [Windows 10 SDK](https://developer.microsoft.com/windows/downloads/windows-10-sdk) 14393 及更高版本|

如果使用的是 **Xamarin.Forms**，请参阅 [XAML 热重载 Xamarin.Forms](/xamarin/xamarin-forms/xaml/hot-reload)。

## <a name="example"></a>示例

以下动画实例演示了如何使用实时可视化树打开一些源代码，然后使用 XAML 热重载更改按钮的文本和颜色。

:::image type="content" source="media/vs-2022/xaml-hot-reload-live-visual-tree.gif" alt-text="打开源代码并使用 XAML 热重载更改 UI 元素的实时可视化树的动画。":::

## <a name="see-also"></a>另请参阅

* [排查 XAML 热重载问题](xaml-hot-reload-troubleshooting.md)
* [适用于 Xamarin.Forms 的 XAML 热重载](/xamarin/xamarin-forms/xaml/hot-reload)
* [编辑并继续 (Visual C#)](../debugger/edit-and-continue-visual-csharp.md)
* [XAML 数据绑定诊断](xaml-data-binding-diagnostics.md)

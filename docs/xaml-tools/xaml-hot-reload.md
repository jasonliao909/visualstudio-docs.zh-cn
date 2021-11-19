---
title: 使用代码编写和调试 XAML XAML 热重载
description: XAML 热重载或 XAML 编辑并继续，允许在运行应用时更改 XAML 代码
ms.date: 10/26/2021
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
ms.openlocfilehash: 5bd1b7c07d4a467c886b2846b8504d8c47f87684
ms.sourcegitcommit: 7a820b7698a8dcf076eb36e3d766fb0751f56bb1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2021
ms.locfileid: "131128009"
---
# <a name="xaml-hot-reload-write-and-debug-your-wpf-and-uwp-apps-while-theyre-running"></a>XAML 热重载：在 WPF 和 UWP 应用运行时编写和调试它们

借助 XAML 热重载，可以增量生成和测试 XAML 代码，其优势是正在运行的应用的数据上下文、身份验证状态和其他实际复杂性在设计时难以模拟。

> [!TIP]
> 如果已通过 UI XAML 热重载用户界面 (到达) 欢迎！ 你适合详细了解XAML 热重载。 但是，如果需要帮助排查问题XAML 热重载，请参阅 [故障排除XAML 热重载](xaml-hot-reload-troubleshooting.md) 故障排除。

在 Visual Studio 和 Blend for Visual Studio 中XAML 热重载，XAML 热重载在这些方案中尤其有用：

* 修复在调试模式下启动应用后在 XAML 代码中发现的 UI 问题。

* 为开发中的应用生成新的 UI 组件，同时利用应用的运行时上下文。

|支持的应用程序类型|操作系统和工具|
|-|-|-|
|Windows Presentation Foundation (WPF) |.NET Framework 4.6+ 和 .NET Core</br>Windows 7 及更高版本 |
|UWP Windows通用 (应用) |Windows 10及更高版本，Windows 10 [SDK](https://developer.microsoft.com/windows/downloads/windows-10-sdk) 14393 及更高版本|

> [!NOTE]
> 如果使用 Xamarin.Forms，请参阅[XAML 热重载 Xamarin.Forms 。](/xamarin/xamarin-forms/xaml/hot-reload)

以下动画演示使用实时可视化树打开一些源代码，然后使用 XAML 热重载更改按钮的文本和颜色的实例。

:::image type="content" source="../debugger/media/xaml-hot-reload-using.gif" alt-text="实时可视化树的动画，它打开源代码，XAML 热重载更改 UI 元素。":::

> [!NOTE]
> Visual StudioXAML 热重载在 Visual Studio 或 Blend for Visual Studio 中运行应用程序，但调试器已连接到 F5 或启动调试 **(，) 。**  除非手动设置环境变量 ，否则无法通过使用 ["](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md) 附加到进程" [来启用此体验](xaml-hot-reload-troubleshooting.md#verify-that-you-use-start-debugging-rather-than-attach-to-process)。

## <a name="known-limitations"></a>已知的限制

以下是上述方法的已知XAML 热重载。 若要处理你遇到的任何限制，只需停止调试器，然后完成操作。

|限制|WPF|UWP|备注|
|-|-|-|-|
|应用运行时将事件与控件连接|不支持|不支持|请参阅错误： *确保事件失败*。 请注意，在 WPF 中，可以引用现有的事件处理程序。 在 UWP 应用中，不支持引用现有事件处理程序。|
|在资源字典（如应用页面/窗口或 *App.xaml* 中的资源字典）中创建资源对象|从 2019 Visual Studio [16.2](/visualstudio/releases/2019/release-notes-v16.2)及更高版本开始支持|支持|示例： <br>- 将 `SolidColorBrush` 添加到资源字典中，以用作 `StaticResource` 。</br>注意：使用资源字典时，可以应用/使用静态资源、样式转换器和其他XAML 热重载。 不支持仅创建资源。</br> - 更改资源字典 `Source` 属性。|
|在应用运行时向项目添加新控件、类、窗口或其他文件|不支持|不支持|无|
|管理NuGet包 (添加/删除/更新包) |不支持|不支持|无|
|更改使用 {x：Bind} 标记扩展的数据绑定|空值|从 2019 Visual Studio开始支持|这需要Windows 10版本 1809 (版本 10.0.17763) 及更高版本。 在 2017 Visual Studio版本中不受支持。|
|不支持更改 x：Uid 指令|N/A|不支持|无|
|使用多个进程 | 支持 | 支持 | 在 2019 Visual Studio [16.6](/visualstudio/releases/2019/release-notes-v16.6)及更高版本中受支持。 |

## <a name="error-messages"></a>错误消息

使用 XAML 热重载 时，可能会遇到以下XAML 热重载。

|错误消息|说明|
|-|-|
|确保事件失败|错误指示你正在尝试将事件连接到其中一个控件，而应用程序运行时不支持该事件。|
|此更改不受 XAML 热重载，并且不会在调试会话期间应用。|错误指示用户不支持你尝试XAML 热重载。 停止调试会话，进行更改，然后重启调试会话。  |

如果发现不受支持的方案，请通过"建议功能"选项 [告知](../ide/suggest-a-feature.md) 我们。

## <a name="see-also"></a>另请参阅

* [排查 XAML 热重载问题](xaml-hot-reload-troubleshooting.md)
* [适用于 Xamarin.Forms 的 XAML 热重载](/xamarin/xamarin-forms/xaml/hot-reload)
* [编辑并继续 (Visual C#)](../debugger/edit-and-continue-visual-csharp.md)

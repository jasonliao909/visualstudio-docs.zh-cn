---
title: 使用 XAML 热重载编写和调试 XAML 代码
description: XAML 热重载（或 XAML 编辑并继续）允许你在运行应用时对 XAML 代码进行更改
ms.date: 11/08/2021
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
ms.openlocfilehash: b85d91752f666bf540f6d74e899c5eb4093144f8
ms.sourcegitcommit: 67dc39e93c86ba50eb5ca877b0471fb8ab8475ac
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/08/2021
ms.locfileid: "132001771"
---
# <a name="xaml-hot-reload-write-and-debug-your-wpf-and-uwp-apps-while-theyre-running"></a>XAML 热重载：在 WPF 和 UWP 应用运行时编写和调试它们

借助 XAML 热重载，可以利用正在运行的应用的数据上下文、身份验证状态和其他在设计时难以模拟的实际复杂性以增量方式生成和测试 XAML 代码。

> [!TIP]
> 如果你是通过 XAML 热重载用户界面 (UI) 来到这里的，欢迎你的到来！ 你来对了地方，这里非常适合详细了解 XAML 热重载。
>
> 但是，如果你在此处寻求排查 XAML 热重载的相关帮助，请改为参阅 [XAML 热重载故障排除](xaml-hot-reload-troubleshooting.md)。

XAML 热重载在 Visual Studio 和 Blend for Visual Studio 中可用，在遇到以下情况时尤其有帮助：

* 修复在调试模式下启动应用后在 XAML 代码中发现的 UI 问题。

* 为开发中的应用生成新的 UI 组件，同时利用应用的运行时上下文。

|支持的应用程序类型|操作系统和工具|
|-|-|-|
|Windows Presentation Foundation (WPF) |.NET Framework 4.6 及更高版本和 .NET Core</br>Windows 7 及更高版本 |
|通用 Windows 应用 (UWP)|Windows 10 及更高版本，以及  [Windows 10 SDK](https://developer.microsoft.com/windows/downloads/windows-10-sdk) 14393 及更高版本|

> [!NOTE]
> 如果你使用的是 Xamarin.Forms，请参阅[适用于 Xamarin.Forms 的 XAML 热重载](/xamarin/xamarin-forms/xaml/hot-reload)。

以下动画实例演示了如何使用实时可视化树打开一些源代码，然后使用 XAML 热重载更改按钮的文本和颜色。

:::image type="content" source="media/vs-2022/xaml-hot-reload-live-visual-tree.gif" alt-text="打开源代码并使用 XAML 热重载更改 UI 元素的实时可视化树的动画。":::

> [!NOTE]
> 当前仅当在 Visual Studio 或 Blend for Visual Studio 中运行应用程序并连接调试程序（F5 或开始调试）时才支持 Visual Studio XAML 热重载。 [除非手动设置环境变量](xaml-hot-reload-troubleshooting.md#verify-that-you-use-start-debugging-rather-than-attach-to-process)，否则无法通过使用[附加到进程](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)来启用此体验。

## <a name="known-limitations"></a>已知的限制

以下是 XAML 热重载的已知限制。 若要处理你遇到的任何限制，只需停止调试程序，然后完成操作。

|限制|WPF|UWP|说明|
|-|-|-|-|
|在应用运行时将事件与控件连接|不支持|不支持|请参阅错误：确保事件失败。 在 WPF 中，可以引用现有的事件处理程序。 在 UWP 应用中，不支持引用现有的事件处理程序。|
|在资源字典（如应用页面/窗口或 App.xaml 中的资源字典）中创建资源对象|从 Visual Studio 2019 [版本 16.2](/visualstudio/releases/2019/release-notes-v16.2) 及更高版本开始受支持|支持|示例： <br>- 将 `SolidColorBrush` 添加到资源字典中，以用作 `StaticResource`。</br>注意：在使用 XAML 热重载时，可以应用/使用写入资源字典的静态资源、样式转换器和其他元素。 不支持仅创建资源。</br> - 更改资源字典的 `Source` 属性。|
|在应用运行时向项目添加新控件、类、窗口或其他文件|不支持|不支持|无|
|管理 NuGet 包（添加/删除/更新包）|不支持|不支持|无|
|更改使用 {x:Bind} 标记扩展的数据绑定|不可用|从 Visual Studio 2019 开始受支持|这需要 Windows 10 版本 1809（内部版本 10.0.17763）及更高版本。 在 Visual Studio 2017 或更低版本中不受支持。|
|不支持更改 x:Uid 指令|N/A|不支持|无|
|使用多个进程 | 支持 | 支持 | 在 Visual Studio 2019 [版本 16.6](/visualstudio/releases/2019/release-notes-v16.6) 以及更高版本中受支持。 |

## <a name="error-messages"></a>错误消息

使用 XAML 热重载时，可能会遇到以下错误。

|错误消息|说明|
|-|-|
|确保事件失败|错误指示你正在尝试将事件连接到其中一个控件，而应用程序运行时不支持该事件。|
|XAML 热重载不支持此更改，且调试会话期间将不应用此更改。|错误指示 XAML 热重载不支持你正在尝试的更改。 停止调试会话，进行更改，然后重启调试会话。  |

如果发现想要得到支持却不受支持的情况，请通过使用[建议功能](../ide/suggest-a-feature.md)选项告知我们。

## <a name="see-also"></a>请参阅

* [排查 XAML 热重载问题](xaml-hot-reload-troubleshooting.md)
* [适用于 Xamarin.Forms 的 XAML 热重载](/xamarin/xamarin-forms/xaml/hot-reload)
* [编辑并继续 (Visual C#)](../debugger/edit-and-continue-visual-csharp.md)

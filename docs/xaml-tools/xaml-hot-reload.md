---
title: 使用脚本编写和调试 XAML XAML 热重载
description: XAML 热重载或 XAML 编辑并继续，允许在运行应用时更改 XAML 代码
ms.date: 09/23/2020
ms.topic: conceptual
helpviewer_keywords:
- xaml edit and continue
- xaml hot reload
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-xaml-tools
ms.workload:
- multiple
ms.openlocfilehash: 4baea5effc0670a8366074187475c7c09c5b39ef
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122130268"
---
# <a name="write-and-debug-running-xaml-code-with-xaml-hot-reload-in-visual-studio"></a>在 Visual Studio 中使用 XAML 热重载编写和调试正在运行的 XAML 代码

XAML 热重载在应用运行时更改 XAML 代码， (UI) 生成 WPF 或 UWP 应用用户界面。 热重载在 Visual Studio 和 Blend for Visual Studio 中均可用。 借助此功能，可以增量生成和测试 XAML 代码，其优点包括正在运行的应用的数据上下文、身份验证状态和其他在设计时难以模拟的实际复杂性。 如果需要帮助排查问题XAML 热重载，请参阅 [疑难](xaml-hot-reload-troubleshooting.md) 解答XAML 热重载故障排除。

> [!NOTE]
> 如果使用的是 Xamarin.Forms，请参阅[XAML 热重载 Xamarin.Forms 。](/xamarin/xamarin-forms/xaml/hot-reload)

XAML 热重载以下情况中， 尤其有用：

* 修复在调试模式下启动应用后在 XAML 代码中发现的 UI 问题。

* 为开发中的应用生成新的 UI 组件，同时利用应用的运行时上下文。

|支持的应用程序类型|操作系统和工具|
|-|-|-|
|Windows Presentation Foundation (WPF) |.NET Framework 4.6+ 和 .NET Core</br>Windows 7 和更高版本 |
|UWP Windows通用 (应用) |Windows 10 SDK 14393+ Windows 10 [及](https://developer.microsoft.com/windows/downloads/windows-10-sdk)以上版本 |

下图显示了如何使用实时可视化树打开源代码，XAML 热重载更改按钮文本和按钮颜色。

![XAML 热重载](../debugger/media/xaml-hot-reload-using.gif)

> [!NOTE]
> Visual StudioXAML 热重载在已连接到 **F5** 的调试器Visual Studio或Blend for Visual Studio或"开始调试" (时，才支持) 。  除非手动设置环境变量 ，否则无法通过使用 ["](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md) 附加到进程" [来启用此体验](xaml-hot-reload-troubleshooting.md#verify-that-you-use-start-debugging-rather-than-attach-to-process)。

## <a name="known-limitations"></a>已知限制

以下是上述方法的已知XAML 热重载。 若要处理你遇到的任何限制，只需停止调试器，然后完成操作。

|限制|WPF|UWP|说明|
|-|-|-|-|
|应用运行时将事件与控件连接|不支持|不支持|请参阅错误： *确保事件失败*。 请注意，在 WPF 中，可以引用现有的事件处理程序。 在 UWP 应用中，不支持引用现有事件处理程序。|
|在资源字典（如应用页面/窗口或 *App.xaml* 中的资源字典）中创建资源对象|从 2019 Visual Studio 2 开始支持|支持|示例：将 `SolidColorBrush` 添加到资源字典中，以用作 `StaticResource` 。</br>注意：在使用资源字典时，可以应用/使用静态资源、样式转换器和其他XAML 热重载。 不支持仅创建资源。</br> 更改资源字典 `Source` 属性。|
|在应用运行时向项目添加新控件、类、窗口或其他文件|不支持|不支持|无|
|管理NuGet包 (添加/删除/更新包) |不支持|不支持|无|
|更改使用 {x：Bind} 标记扩展的数据绑定|不适用|从 2019 Visual Studio开始支持|这需要Windows 10版本 1809 (版本 10.0.17763) 。 在 2017 Visual Studio版本中不受支持。|
|不支持更改 x：Uid 指令|N/A|不支持|无|
|多个进程 | 支持 | 支持 | 在 2019 Visual Studio [16.6](/visualstudio/releases/2019/release-notes-v16.6)及更高版本中受支持 |

## <a name="error-messages"></a>错误消息

使用 XAML 热重载 时，可能会遇到以下XAML 热重载。

|错误消息|说明|
|-|-|
|确保事件失败|错误指示你正在尝试将事件连接到其中一个控件，而应用程序运行时不支持该事件。|
|此更改不受 XAML 热重载，并且不会在调试会话期间应用。|错误指示用户不支持你尝试XAML 热重载。 停止调试会话，进行更改，然后重启调试会话。 如果发现不受支持的方案，请使用开发人员指南中的新"建议功能[Visual Studio"Community。](https://aka.ms/feedback/suggest?space=8) |

## <a name="see-also"></a>请参阅

* [排查 XAML 热重载问题](xaml-hot-reload-troubleshooting.md)
* [适用于 Xamarin.Forms 的 XAML 热重载](/xamarin/xamarin-forms/xaml/hot-reload)
* [编辑并继续 (Visual C#)](../debugger/edit-and-continue-visual-csharp.md)

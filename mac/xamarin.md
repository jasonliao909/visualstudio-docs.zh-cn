---
title: Xamarin
description: '使用 Visual Studio for Mac 中的 Xamarin，可创建面向 iOS、Mac、Android、tvOS 和 watchOS 的跨平台应用程序 '
author: jmatthiesen
ms.author: jomatthi
manager: dominicn
ms.date: 06/18/2019
ms.assetid: 339F6051-5F90-48DC-8237-EBBC8A03A32B
ms.topic: how-to
ms.openlocfilehash: cbbcd2b7a94b76df4aa00b4955d2303513cf1e52
ms.sourcegitcommit: fcf47a9c356df7e9636bcab92186923e5c9b8892
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/30/2022
ms.locfileid: "144522759"
---
# <a name="xamarin-mobile-app-development"></a>Xamarin 移动应用开发

 [!INCLUDE [Visual Studio for Mac](~/includes/applies-to-version/vs-mac-only.md)]

通过对 [Xamarin](/xamarin) 的卓越支持，可以开发适用于 Android、macOS、iOS、tvOS 和 watchOS 的丰富本机体验。 使用 Xamarin.Forms 跨平台应用程序可以在 Android、iOS 和 macOS 之间共享基于 XAML 的 UI 代码，而不会限制对本机功能的访问。

## <a name="xamarinforms"></a>Xamarin.Forms

适用于 Xamarin.Forms 的 XAML 热重载内置于版本 8.3 及更高版本的 Visual Studio for Mac 中。 启用此功能后，每次保存文件时，所做更改会立即反映在正在运行的应用中。

若要启用 XAML 热重载，请在“Visual Studio”>“首选项”>“项目”>“Xamarin 热重载”中选中“启用 Xamarin 热重载”复选框 。

若要详细了解热重载，请参阅文档中的[适用于 Xamarin.Forms 的 XAML 热重载指南](/xamarin/xamarin-forms/xaml/hot-reload)。

## <a name="android"></a>Android

Visual Studio for Mac 有其自己的集成 Android SDK 管理器，允许访问希望应用面向的 SDK。

对于 Android 应用程序，Visual Studio for Mac 包含其自己的设计器，该设计器适用于 Android `.axml` 文件来直观地构造用户界面。 Visual Studio for Mac 将在 Android Designer 中打开这些文件，如下图所示：

![Android UI 设计器](media/intro-image31.png)

有关 Android Designer 的详细信息，请参阅 [Xamarin Android Designer 概述](/xamarin/android/user-interface/android-designer/index)指南。

## <a name="ios"></a>iOS

IOS 设计器与 Visual Studio for Mac 完全集成，可进行 .xib 的可视编辑，并使 Storyboard 文件创建 iOS、tvOS 和 WatchOS UI 并转换。 使用直观方法处理事件时，可使用工具箱和 Design Surface 之间的拖放功能生成整个用户界面。 iOS 设计器还支持具有额外的设计时呈现优势的[自定义控件](/xamarin/ios/user-interface/designer/ios-designable-controls-overview)。

![iOS Storyboard 设计器](media/intro-image30.png)

有关使用 iOS Designer 的详细信息，请参阅[设计器](/xamarin/ios/user-interface/designer/?tabs=macos)指南。

### <a name="mac"></a>Mac

Xamarin 提供本机 Mac API 绑定，让用户能够创建美观的 Mac 应用程序。

有关使用 Visual Studio for Mac 编写 Mac 应用程序的详细信息，请参阅 [Xamarin.Mac](/xamarin/mac/get-started/index) 指南。

## <a name="xamarin-enterprise-features"></a>Xamarin Enterprise 功能

> [!Note]
> 这些产品仅可用于 Visual Studio Enterprise 订阅。

### <a name="profiler"></a>探查器

Xamarin Profiler 有三个可用于分析的仪表。 [Xamarin Profiler 简介](/xamarin/tools/profiler/index?tabs=macos)指南介绍了这些仪表的度量值以及它们分析应用程序的方式，并阐明了每个屏幕上显示的数据的含义。

### <a name="inspector"></a>检查器

Xamarin Inspector 提供一个具有用户工具的交互式 C# 控制台。 它可在检查实时应用程序时用作调试或诊断辅助，还可用作教学工具、文档工具或实验工具。

![Xamarin Inspector](media/intro-inspector.png)

它包括一个独立应用程序，可提供面向各种编程平台（Android、iOS、Mac 和 Windows）并集成到 IDE 调试工作流的内容丰富的 C# 控制台。

有关详细信息，请参阅 [Xamarin Inspector](/xamarin/tools/inspector/release-notes/1.5) 指南。

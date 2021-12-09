---
title: 使用热重载编写和调试代码
description: 热重载（类似于“编辑并继续”）允许你在运行应用时对代码进行更改
ms.date: 11/05/2021
ms.topic: conceptual
helpviewer_keywords:
- Hot reload
- .NET Hot Reload
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: '>= vs-2022'
ms.workload:
- multiple
ms.openlocfilehash: fd616cb467d5367fd317601ecfdbacf5fc946b48
ms.sourcegitcommit: ba40c6208b2cb27d047fec4fa2c83c6be4f9ee5a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/09/2021
ms.locfileid: "134463505"
---
# <a name="write-and-debug-running-code-with-hot-reload-in-visual-studio-c-visual-basic-c"></a>在 Visual Studio (c #、Visual Basic、c + + 中，用热重载编写和调试正在运行的代码) 

从 Visual Studio 2022 开始，Visual Studio 中的热重载体验适用于托管 .NET 和本机 C++ 应用。 无论使用哪种类型的应用，热重载的目的都是尽可能节省编辑之间的应用重启次数，从而使你通过减少等待应用重新生成、重启、重新导航到你在应用中的上一个位置等操作的时间来提高工作效率。

为此，可以编辑应用程序的代码文件并将代码更改立即应用于正在运行的应用程序，也称为“热重载”。 应用更改后，通过在应用中执行操作（或通过某种计时器等）再次重新执行代码并立即查看更改；不需要通过断点暂停应用！

## <a name="update-running-code-with-hot-reload"></a>使用热重载更新正在运行的代码

1. 基于支持的应用程序类型打开项目。 有关 .NET 的详细信息，请参阅 [.NET 应用程序支持](#supported-net-app-frameworks-and-scenarios)。

1. 确保在调试器设置或调试启动配置文件中禁用“启用本机代码调试”。

1. 使用 F5 或 Ctrl+F5（如果[应用程序支持](#supported-net-app-frameworks-and-scenarios)）来启动附加了调试器的应用。

1. 打开包含一些代码的 C#、C++ 或 Visual Basic 代码文件，这些代码可以通过正在运行的应用程序用户界面（例如，按钮或视图模型命令的代码隐藏）重新执行或通过计时器每隔一段时间触发并更改代码。

1. 使用“热重载”按钮或按 ALT+F10 应用代码更改。

   ![“热重载”按钮的屏幕截图。](../debugger/media/vs-2022/dotnet-hot-reload.gif)

## <a name="supported-net-app-frameworks-and-scenarios"></a>支持的 .NET 应用框架和方案

* 使用 Visual Studio 2022 和启动具有调试器的应用时，基本热重载体验适用于大多数类型的 .NET 应用和框架版本。 此支持包括 .NET Framework、.NET Core 和 .NET 5+（适用于 C# 和 Visual Basic）。 支持的应用类型包括 Web（代码隐藏更改）、桌面、移动、云和其他项目类型。 此方案中的预期是，如果使用的是调试器，则假设热重载可用并进行尝试！
* 使用 Visual Studio 2022 但不使用调试器（例如，使用 CTRL-F5 启动应用）时，即使面向大多数类型的 .NET 6 应用，热重载也可用。 这意味着不面向 .NET 6（.NET 5 或更低版本）的应用将不支持“无调试器”方案，并且必须使用调试器来获得热重载支持。
* 将 Visual Studio 2022 与 .NET 6 应用一起使用时，支持大多数方案。 这不限于上述新的“无调试器”功能。 它还包括其他新功能，例如支持热重载 Blazor 项目，更一般地说，在任何 ASP.NET Core 应用中编辑 Razor 文件，以及 CSS 热重载。 将 Visual Studio 2022 与面向 .NET 6 的应用一起使用，可让你获得最强大的热重载体验。

下表显示了哪些应用程序类型在附加调试器 (F5) 和不附加调试器 (Ctrl+F5) 的情况下支持 .NET 热重载，以及是否需要 .NET 6 才能获得最低支持（即 F5）。 Ctrl+F5 支持始终需要 .NET 6。 还显示了支持该功能的 Visual Studio 的最低版本。

|应用程序类型|需要 .NET 6|F5|Ctrl+F5|
|-|-|-|-|
|ASP.NET 代码隐藏|否|16.11|17.0|
|ASP.NET Razor（Blazor Server 和 ASP.NET Core）|是|17.0|17.0|
|ASP.NET Razor (Blazor WASM)|是|17.1|17.0|
|WPF|否|16.11|17.0|
|WinUI3|否|16.11|--|
|WinForms|否|16.11|17.0|
|控制台|否|16.11|17.0|
|.NET MAUI (WinUI 3) |是|17.1|--|
|.NET MAUI (Android) |是|17.1|--|
|.NET MAUI (iOS) |是|17.1|--|
|.NET MAUI Blazor 混合 (WinUI 3) |是|17.1|--|
|.NET MAUI Blazor 混合 (Android) |是|17.1|--|
|.NET MAUI Blazor 混合 (iOS) |是|17.1|--|

可以使用热重载进行的编辑类型由运行时决定，而不是由用于启动应用程序的方法（F5 或 Ctrl+F5）决定。

在以下部分中，我们将对上述摘要进行扩展，并深入了解更多详细信息。

## <a name="support-for-c-apps"></a>对 C++ 应用的支持

使用 Visual Studio 2022 并启动具有调试器的应用时，可以使用“热重载”按钮热重载在调试器 (F5) 下运行的本机 C++ 应用。 使用 CMake 和 OpenFolder 项目生成的应用也支持热重载。

此体验由本机“编辑并继续”提供支持。 有关支持的编辑，请参阅[编辑并继续](../debugger/edit-and-continue-visual-cpp.md)。

## <a name="visual-studio-2022-with-a-net-app-when-using-the-debugger"></a>使用 .NET 应用同时使用调试器的 Visual Studio 2022

使用 Visual Studio 2022 并启动具有调试器的应用时，热重载适用于大多数应用框架，包括典型的应用类型，例如控制台、Windows 窗体 (WinForms)、WPF、UWP、WinUI 3（请参阅注释）和大多数类型的 ASP.NET Web 项目（用于代码隐藏编辑），包括 ASP.NET MVC、Web API，甚至较旧的 Web Forms 项目。 这些就是示例。 在你拥有 .NET 且使用 Visual Studio 托管调试器的任何地方，你都应获得基本的热重载支持。 这一事实意味着，即使是 Azure Functions 之类的项目在此方案中也非常成功。

> [!NOTE]
> WinUI 3 默认使用混合模式调试，不支持热重载。 可以通过启用托管的调试器在项目设置中修改此设置，从而使热重载正常工作。 若要在项目中启用此项，请修改 Launchsettings.json 并在 `"nativeDebugging": false` 属性后面添加 `commandName` 。

从 Visual Studio 2022 版本 17.1 预览版 1 开始支持 .NET MAUI 应用。

## <a name="visual-studio-2022-with-a-net-app-but-not-using-the-debugger"></a>使用 .NET 应用但不使用调试器的 Visual Studio 2022

当面向大多数类型的 .NET 6 应用（包括控制台、WPF、Windows 窗体 (WinForms)、ASP.NET Core MVC、Web API 和 Blazor 等项目类型）时，无需调试器即可使用热重载。

此功能专用于 .NET 6+。 这些不面向 .NET 6（.NET 5 或更低版本）的应用将不支持“无调试器”方案，并且必须使用调试器才能访问热重载功能。

另外，请注意，并非所有项目类型目前都支持“无调试器”方案。 具体而言：

* 在没有调试器的情况下，热重载不支持 UWP 应用。 这是设计使然，目前没有改善这一点的计划。
* 面向 iOS 和 Android 的 Xamarin.Forms 应用不支持 .NET 热重载（无论是在有还是没有调试器的情况下启动应用），但将继续支持 XAML 热重载。
* .NET MAUI调试器才支持这些应用。

## <a name="visual-studio-2022-with-a-net-6-app"></a>使用 .NET 6 应用的 Visual Studio 2022

如果同时使用 Visual Studio 2022 和面向 .NET 6 的应用，则可以获得最精美且功能强大的热重载体验。

在此方案中受支持：

* Blazor 应用（服务器和 WebAssembly（请参阅注释））
* 在 Blazor 和常规 ASP.NET Core 网站中编辑 Razor 文件
* CSS 热重载
* 在没有调试器的情况下运行应用程序时支持热重载（更多详情如前所述）

如果你面向的是 .NET 6，将继续在即将推出的 Visual Studio 2022 更新和 .NET 功能区段和主要版本中获得改进。

> [!NOTE]
> 在 Visual Studio 2022 (版本 17.0) 的第一个版本中，热重载 在使用 Visual Studio 调试器时对 Blazor WebAssembly 的支持当前未启用，但从 17.1 开始提供。 如果在没有调试热重载的情况下通过 Visual Studio或更新到 17.1 版本来启动应用，则仍可以继续运行。

## <a name="supported-aspnet-core-scenarios"></a>支持的 ASP.NET Core 方案

许多 ASP.NET 方案都支持基本的热重载体验。 最广泛可用的功能是能够为大多数类型的 Web 应用程序更改代码隐藏和其他 .NET 类文件。 此功能在使用 Visual Studio 调试器时有效，并且出现在以前可以使用“编辑并继续”的任何位置。

对于面向 .NET 6 的 ASP.NET Core 开发人员，还有一些其他功能不适用于较低版本的 .NET。 这些功能包括：

* CSHTML：编辑 Razor CSHTML 文件支持多种类型的编辑。
* **浏览器刷新**：编辑 razor 文件将在调试时自动在 Web 浏览器中刷新更改。 此功能以前仅在没有调试器的情况下启动应用时可用。
* **CSS 热重载**：可以在应用运行时更改 CSS 文件，键入的更改将立即应用到正在运行的应用。
* 无调试器：使用 Visual Studio 在没有调试器的情况下启动 Web 应用 (CTRL-F5) 时，可以获得热重载支持。

## <a name="supported-net-edits"></a>支持的 .NET 编辑

.NET 热重载体验通过[编辑并继续](../debugger/edit-and-continue-visual-csharp.md)机制提供支持。 改进包括对其他类型的编辑的支持，这些编辑超出了较旧版本的 Visual Studio 中最初可能存在的编辑。 改进包括：

* 添加、更新或删除自定义属性
* 添加或更新记录结构
* 添加或更新 #line 指令
* 编辑 Switch 表达式
* 用 #line 指令编辑文件，包括对指令本身的更改
* 编辑顶级语句
* 编辑使用任何 C# 10 新功能的代码，例如全局 using 指令、文件范围的命名空间、改进的 lambda 和无参数结构构造函数
* 重命名 Lambda 参数
* 重命名现有方法的参数

上述改进适用于热重载和“编辑并继续”体验。

## <a name="unsupported-net-scenarios"></a>不支持的 .NET 方案

不支持的方案：

* Xamarin.Forms 应用在 iOS 和 Android 方案中不支持 .NET 热重载。 面向 UWP 应用时，将获得对热重载的部分支持。 这是设计使然，我们不希望进行任何进一步的改进。 （注意：在最新的 SDK 上，XAML 热重载将继续可用，并支持 Xamarin.Forms 客户。）
* Visual Studio 2022 版本 17.1 预览版 1 之前不支持 .NET MAUI 应用。 从 17.1 预览版 1 开始，支持 .NET MAUI，但仅限于附加了调试器的情况。
* 使用 F# 生成的应用或面向 .NET Native 的应用不支持热重载。

如果在不使用调试器的情况下使用 Visual Studio。 NET 热重载仅适用于面向 .NET 6 的应用。

此外，热重载在某些项目配置中不可用：

* 如果使用 Visual Studio 调试器来运行应用，但在设置中禁用了 `Edit and Continue`，则不支持热重载。
* 不支持版本或自定义生成配置。 你的项目必须使用“调试”生成配置。
* .NET 热重载不支持某些启动或编译优化。 例如，如果项目的调试配置文件是通过以下方式配置的，则不支持 .NET 热重载：
  * 为你的项目启用了[修整](/dotnet/core/deploying/trimming/trimming-options)。 例如，如果在调试配置文件的项目文件中将 `PublishTrimmed` 设置为 True，则不支持热重载。
  * 为你的项目启用了 [ReadyToRun](/dotnet/core/deploying/ready-to-run)。 例如，如果在调试配置文件的项目文件中将 `PublishReadyToRun` 设置为 True，则不支持热重载。
* 对于 WinUI 3 应用程序，会默认启用本机代码调试（即使 LaunchSettings.json 中缺少设置也会默认启用），在按此方式执行混合模式调试时，不支持 .NET 热重载。 因此，必须将显式设置 `nativeDebugging: false` 添加到 LaunchSettings.json 中，以便 .NET 热重载正常工作。

## <a name="configure-hot-reload"></a>配置热重载

可以通过从“热重载”下拉按钮中选择“设置”来配置热重载。 

![配置热重载的屏幕截图](../debugger/media/vs-2022/dotnet-hot-reload-configure.png)

或者，打开“工具” > “选项” > “调试” > “.NET/C++ 热重载”。

热重载的设置包括：

* 调试时启用热重载和“编辑并继续”。 在附加调试器 (F5) 的情况下启动时启用热重载。

* 在不调试的情况下启动时启用热重载。 在没有附加调试器的情况下启动时启用热重载 (Ctrl+F5)。

* 保存文件时应用热重载。 保存文件时应用代码更改。

![.NET 热重载设置的屏幕截图](../debugger/media/vs-2022/dotnet-hot-reload-settings.png)

还可通过修改 .NET 6 项目 launchSetting.json，将 设置为 来控制 .NET 热重载是否在项目级别 `hotReloadEnabled` 可用 `false` 。

示例：

```xaml
{
  "profiles": {
    "Console": {
      "commandName": "Project",
      "hotReloadEnabled": false
    }
  }
}
```

## <a name="warning-message"></a>警告消息

如果看到以下对话框，则热重载无法在不重启的情况下应用当前编辑。 可以选择重新生成应用，并应用更改（重启），或者继续编辑。 如果重新生成，则所有应用程序状态都将丢失。 如果继续编辑，其他更改或更正可能导致热重载再次运行。

![“应用更改”对话框的屏幕截图](../debugger/media/vs-2022/dotnet-hot-reload-apply-changes.png)

如果在对话框中选择“始终重新生成”选项，则不会在当前 Visual Studio 会话中再次看到该对话框，并且 Visual Studio 将自动重新生成和重新加载，而不是显示对话框。

> [!NOTE]
> 在版本 17.0 Visual Studio (版本 17.0) 在调试器中使用 热重载时，仍将显示标准"编辑并继续"对话框。 这是一个 bug，从 17.1 预览版 2 版本开始已解决。

## <a name="see-also"></a>另请参阅

[编辑并继续 (Visual C#)](../debugger/edit-and-continue-visual-csharp.md)
[编辑并继续 (C++)](../debugger/edit-and-continue-visual-cpp.md)

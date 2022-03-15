---
title: .NET C# 调试配置的项目设置 | Microsoft Docs
description: 了解如何使用项目属性页面的“调试”选项卡和“生成”选项卡在 Visual Studio 中更改 C# .NET 5+ 或 .NET Core 调试配置的项目设置。
ms.date: 02/22/2022
ms.topic: reference
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debug configurations, C# .NET Core
- project settings [Visual Studio], debug configurations
- debug builds, project settings
- projects [Visual Studio], debug configurations
- project configurations, debug
- debugging [C#], debugger settings
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: '>= vs-2022'
ms.workload:
- dotnet
ms.openlocfilehash: 1eb007fed1d237aaa00c8bf9e040f57b7c8113bb
ms.sourcegitcommit: edf8137cd90c67b6078a02c93094f7e1c3bf8930
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2022
ms.locfileid: "139552364"
---
# <a name="project-settings-for-c-debug-configurations-net-core-net-5-and-aspnet-core"></a>C# 调试配置（.NET Core、.NET 5+ 和 ASP.NET Core）的项目设置

可在项目属性页的[“调试”选项卡](#debug-tab)和[“生成”选项卡](#build-tab)中更改 C# 项目调试设置。

若要打开属性页，在“解决方案资源管理器”中选择项目，然后选择“属性”图标，或右键单击项目并选择“属性”  。

有关详细信息，请参见[调试和发布配置](how-to-set-debug-and-release-configurations.md)。

>[!IMPORTANT]
>这些设置不适用于 .NET Framework 或 UWP 。 若要配置 .NET Framework 的调试设置，请参阅 [C# 调试配置的项目设置](../debugger/project-settings-for-csharp-debug-configurations.md)。

## <a name="debug-tab"></a>“调试”选项卡

从 Visual Studio 2022 开始，选择“调试”选项卡中的“打开调试启动配置文件 UI”可打开启动配置文件 UI 和更改调试设置。

## <a name="launch-profile-net-core-net-5"></a>启动配置文件（.NET Core、.NET 5+）

|设置|说明|
|-------------------------------------| - |
|**命令行参数** | 指定要调试的应用的命令行参数。 命令名称为“启动外部程序”中指定的应用名称。 |
|**工作目录** | 指定要调试的应用的工作目录。 在 C# 中，默认情况下，工作目录为 \bin\debug。 |
|**使用远程计算机**|对于远程调试，请选择此选项，然后输入远程调试目标的名称或 [Msvsmon 服务器名称](../debugger/remote-debugging.md)。 <br />应用在远程计算机上的位置由“生成”选项卡中的“输出路径”属性指定 。此位置必须是远程计算机上的共享目录。 |
|**环境变量**|在运行应用程序进程之前设置环境变量。 有关 ASP.NET Core 的信息，请参阅[环境](/aspnet/core/fundamentals/environments#environments-1)。|
|**启用非托管代码调试** | 从托管应用调试对本机（非托管）Win32 代码的调用。 |
|**启用 SQL Server 调试** | 调试 SQL Server 数据库对象。 |
|**启用 WebView2 调试**| 使用基于 Microsoft Edge (Chromium) 调试器调试 JavaScript。|

## <a name="launch-profile-aspnet-core"></a>启动配置文件 (ASP.NET Core)

除了 .NET 5+ 的属性之外，ASP.NET Core 启动配置文件还包括不同 ASP.NET Core 配置文件的若干其他属性。 这些设置为项目的 launchSettings.json 文件提供了一个简单的 UI。 有关此文件的详细信息，请参阅[在 ASP.NET Core 中使用多个环境](/aspnet/core/fundamentals/environments)中的“开发”和 launchSettings.json 部分。

启动配置文件 UI 中提供的设置包括以下内容。

|设置|说明|
|-------------------------------------| - |
|**启动浏览器**|选择在启动调试时是否启动默认浏览器（使用在“URL”设置中设置的 URL）。|
|**Url**|指定 .NET 或 .NET Core 的主机 URL 的位置。 对于根据项目命名的配置文件（即 launchSettings.json 中的 commandName 属性为 Project），Kestrel 服务器侦听指定的端口 。 对于 IIS 配置文件，此值通常与“应用 URL”相同。 有关详细信息，请参阅[配置项目](/aspnet/core/host-and-deploy/iis/development-time-iis-support#configure-the-project)下的 IIS 启动配置文件部分。|
|**应用 URL**|指定应用程序 URL。 对于根据项目命名的配置文件，此属性指定 Kestrel 服务器 URL，通常为 https://localhost:5001 和 http://localhost:5000|

Visual Studio 默认提供 IIS Express 配置文件，并且你可以创建其他配置文件，例如 IIS 配置文件。 这些设置还对应于 launchSettings.json 中的设置。 这两种配置文件类型提供了多种设置，例如托管模型。

|设置|说明|
|-------------------------------------| - |
|**托管模型**|指定“进程内”或“进程外”。 有关详细信息，请参阅 ASP.NET Core 中的[托管模型](/aspnet/core/host-and-deploy/aspnet-core-module#hosting-models)。|
|**应用 SSL URL**|对于 IIS Express，“应用 SSL URL”通常为 http://localhost:44334。|

## <a name="build-tab"></a>“生成”选项卡

|设置|描述|
|-------------|-----------------|
|**常规** > **条件编译符号**|定义 DEBUG 和 TRACE 常数（如果已选）。<br /><br /> 这些常数启用 [Debug](/dotnet/api/system.diagnostics.debug) 类和 [Trace](/dotnet/api/system.diagnostics.trace) 类的条件编译。 定义了这两个常数后，Debug 和 Trace 类方法将向[输出窗口](../ide/reference/output-window.md)生成输出。 如果没有这两个常数，则不编译 Debug 和 Trace 类方法，并且不生成任何输出。<br /><br />通常情况下，DEBUG 在生成的调试版本中定义，而不在发布版本中定义。 调试和发布版本中都定义了 TRACE。|
|**常规** > **优化代码**|除非 bug 仅在经过优化的代码中出现，否则对于“调试”生成，请取消选择此设置。 经过优化的代码更难调试，因为指令与源代码中的语句并不是直接对应关系。|
|**调试符号**|指定编译器生成的调试信息的类型。 请参阅[调试符号](#debug-symbols)。 有关如何配置应用程序的调试性能的信息，请参阅[令映像更易于调试](/dotnet/framework/debug-trace-profile/making-an-image-easier-to-debug)。|
|“输出” > “输出的基路径” |指定中间输出的基文件夹。 输出通常转到“bin\Debug”进行调试生成。|
|“输出” > “中间输出的基路径” |指定中间输出的基文件夹。 输出通常转到“obj\Debug”进行调试生成。|

## <a name="debug-symbols"></a>调试符号

可以选择以下调试符号选项。

- **未发出任何符号**

   指定不会生成任何调试信息。

- **PDB 文件，当前平台**

   生成 .PDB 文件，这是一种特定于平台的符号文件，可提供其他工具（尤其是调试器）、主可执行文件内容的相关信息及其生成方式。

- **PDB 文件，可移植**

   生成 .PDB 文件，这是一种未特定于任何平台的可移植符号文件，可提供其他工具（尤其是调试器）、主可执行文件内容的相关信息及其生成方式。 有关详细信息，请参阅 [Portable PDB](https://github.com/dotnet/core/blob/master/Documentation/diagnostics/portable_pdb.md)（可移植 PDB）。

- **嵌入到 DLL/EXE 中，可跨平台移植**

   将可移植符号信息嵌入程序集。 不会生成任何外部 .PDB 文件。

有关详细信息，请参阅 [/debug (C# 编译器选项)](/dotnet/csharp/language-reference/compiler-options/debug-compiler-option)。

## <a name="see-also"></a>请参阅

- [调试器设置和准备](../debugger/debugger-settings-and-preparation.md)
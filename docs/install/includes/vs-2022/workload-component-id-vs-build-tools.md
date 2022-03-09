---
title: Visual Studio 生成工具 2022 工作负荷和组件 ID
titleSuffix: ''
description: 使用 Visual Studio 工作负载和组件 ID 来构建基于 Windows 的经典应用程序
keywords: ''
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.date: 02/15/2022
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.topic: include
ms.openlocfilehash: 0f60284120c72fe1ac893a708e5bf4d9013c7c3b
ms.sourcegitcommit: edf8137cd90c67b6078a02c93094f7e1c3bf8930
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2022
ms.locfileid: "139550308"
---
## <a name="azure-development-build-tools"></a>Azure 开发生成工具

**ID：** Microsoft.VisualStudio.Workload.AzureBuildTools

**描述：** 用于生成 Azure 应用程序的 MSBuild 任务和目标。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | “属性” | Version | 依赖项类型
--- | --- | --- | ---
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 目标包 | 17.1.32112.364 | 必需
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 17.1.32112.364 | 必需
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 开发工具 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Azure.AuthoringTools | Azure 创作工具 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Azure.ClientLibs | .NET 的 Azure 库 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Azure.Waverton.BuildTools | Azure 云服务生成工具 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.DockerTools.BuildTools | 容器开发工具 - 生成工具 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.NuGet.BuildTools | NuGet 目标和生成任务 | 17.1.32112.364 | 必须
Microsoft.VisualStudio.Component.TypeScript.TSServer | TypeScript 服务器 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Wcf.BuildTools.ComponentGroup | Windows Communication Foundation 生成工具 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Web.BuildTools.ComponentGroup | Web 开发生成工具 | 17.1.32112.364 | 必须
Microsoft.Net.Component.4.8.TargetingPack | .NET Framework 4.8 目标包 | 17.1.32112.364 | 建议
Microsoft.Net.ComponentGroup.4.8.DeveloperTools | .NET Framework 4.8 开发工具 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.WebDeploy | Web Deploy | 17.1.32112.364 | 建议
Microsoft.Net.Component.3.5.DeveloperTools | .NET Framework 3.5 开发工具 | 17.1.32112.364 | 可选
Microsoft.Net.Component.4.6.2.TargetingPack | .NET Framework 4.6.2 目标包 | 17.1.32112.364 | 可选
Microsoft.Net.Component.4.7.1.TargetingPack | .NET Framework 4.7.1 目标包 | 17.1.32112.364 | 可选
Microsoft.Net.Component.4.7.TargetingPack | .NET Framework 4.7 目标包 | 17.1.32112.364 | 可选
Microsoft.Net.ComponentGroup.4.6.2-4.7.1.DeveloperTools | .NET Framework 4.6.2-4.7.1 开发工具 | 17.1.32112.364 | 可选
Microsoft.NetCore.Component.Runtime.6.0 | .NET 6.0 运行时 | 17.1.32210.238 | 可选
Microsoft.NetCore.Component.SDK | .NET SDK | 17.1.32210.238 | 可选
Microsoft.VisualStudio.Component.TypeScript.SDK.4.4 | TypeScript 4.4 SDK | 17.1.32112.364 | 可选

## <a name="data-storage-and-processing-build-tools"></a>数据存储和处理生成工具

**ID：** Microsoft.VisualStudio.Workload.DataBuildTools

**描述：** 生成 SQL Server 数据库项目

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | “属性” | Version | 依赖项类型
--- | --- | --- | ---
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 目标包 | 17.1.32112.364 | 建议
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 17.1.32112.364 | 建议
Microsoft.Net.Component.4.8.TargetingPack | .NET Framework 4.8 目标包 | 17.1.32112.364 | 建议
Microsoft.Net.ComponentGroup.TargetingPacks.Common | .NET Framework 4.8 开发工具 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# 和 Visual Basic | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.SQL.SSDTBuildSku | SQL Server Data Tools - 生成工具 | 17.1.32112.364 | 建议

## <a name="net-desktop-build-tools"></a>.NET 桌面生成工具

**ID：** Microsoft.VisualStudio.Workload.ManagedDesktopBuildTools

**描述：** 用于使用 C#、Visual Basic 和 F# 生成 WPF、Windows 窗体和控制台应用程序的工具。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | “属性” | Version | 依赖项类型
--- | --- | --- | ---
Microsoft.Component.MSBuild | MSBuild | 17.1.32112.364 | 必需
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 目标包 | 17.1.32112.364 | 必需
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 17.1.32112.364 | 必需
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 开发工具 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.NuGet.BuildTools | NuGet 目标和生成任务 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 17.1.32112.364 | 必需
Microsoft.Component.ClickOnce.MSBuild | ClickOnce 生成工具 | 17.1.32112.364 | 建议
Microsoft.Net.Component.4.8.TargetingPack | .NET Framework 4.8 目标包 | 17.1.32112.364 | 建议
Microsoft.Net.ComponentGroup.4.8.DeveloperTools | .NET Framework 4.8 开发工具 | 17.1.32112.364 | 建议
Microsoft.NetCore.Component.Runtime.6.0 | .NET 6.0 运行时 | 17.1.32210.238 | 建议
Microsoft.NetCore.Component.SDK | .NET SDK | 17.1.32210.238 | 建议
Microsoft.VisualStudio.Component.TestTools.BuildTools | 测试工具核心功能 - 生成工具 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Wcf.BuildTools.ComponentGroup | Windows Communication Foundation 生成工具 | 17.1.32112.364 | 建议
Microsoft.Net.Component.3.5.DeveloperTools | .NET Framework 3.5 开发工具 | 17.1.32112.364 | 可选
Microsoft.Net.Component.4.6.2.TargetingPack | .NET Framework 4.6.2 目标包 | 17.1.32112.364 | 可选
Microsoft.Net.Component.4.7.1.TargetingPack | .NET Framework 4.7.1 目标包 | 17.1.32112.364 | 可选
Microsoft.Net.Component.4.7.TargetingPack | .NET Framework 4.7 目标包 | 17.1.32112.364 | 可选
Microsoft.Net.ComponentGroup.4.6.2-4.7.1.DeveloperTools | .NET Framework 4.6.2-4.7.1 开发工具 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.FSharp.MSBuild | F# 编译器 | 17.1.32112.364 | 可选

## <a name="msbuild-tools"></a>MSBuild 工具

**ID：** Microsoft.VisualStudio.Workload.MSBuildTools

**描述：** 提供生成基于 MSBuild 的应用程序所需的工具。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | “属性” | Version | 依赖项类型
--- | --- | --- | ---
Microsoft.Component.MSBuild | MSBuild | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.CoreBuildTools | Visual Studio 生成工具核心 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 17.1.32112.364 | 必须

## <a name="nodejs-build-tools"></a>Node.js 生成工具

**ID：** Microsoft.VisualStudio.Workload.NodeBuildTools

**描述：** 用于使用异步事件驱动型 JavaScript 运行时 Node.js 生成可缩放网络应用程序的 MSBuild 任务和目标。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | “属性” | Version | 依赖项类型
--- | --- | --- | ---
Microsoft.VisualStudio.Component.Node.Build | Node.js MSBuild 支持 | 17.1.32112.364 | 必须
Microsoft.VisualStudio.Component.TypeScript.TSServer | TypeScript 服务器 | 17.1.32112.364 | 必须
Microsoft.VisualStudio.Component.TypeScript.SDK.4.4 | TypeScript 4.4 SDK | 17.1.32112.364 | 可选

## <a name="officesharepoint-build-tools"></a>Office/SharePoint 生成工具

**ID：** Microsoft.VisualStudio.Workload.OfficeBuildTools

**描述：** 生成 Office 和 SharePoint 加载项以及 VSTO 加载项。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | “属性” | Version | 依赖项类型
--- | --- | --- | ---
Microsoft.Component.ClickOnce.MSBuild | ClickOnce 生成工具 | 17.1.32112.364 | 必需
Microsoft.Component.MSBuild | MSBuild | 17.1.32112.364 | 必需
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 目标包 | 17.1.32112.364 | 必需
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 17.1.32112.364 | 必需
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 开发工具 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.NuGet | NuGet 程序包管理器 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.NuGet.BuildTools | NuGet 目标和生成任务 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Sharepoint.BuildTools | Office/SharePoint 开发生成工具 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Workflow.BuildTools | Windows Workflow Foundation 生成工具 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Wcf.BuildTools.ComponentGroup | Windows Communication Foundation 生成工具 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Web.BuildTools.ComponentGroup | Web 开发生成工具 | 17.1.32112.364 | 必须
Microsoft.Net.Component.4.8.TargetingPack | .NET Framework 4.8 目标包 | 17.1.32112.364 | 建议
Microsoft.Net.ComponentGroup.4.8.DeveloperTools | .NET Framework 4.8 开发工具 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.TeamOffice.BuildTools | Visual Studio Tools for Office (VSTO) 生成工具 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.WebDeploy | Web Deploy | 17.1.32112.364 | 建议
Microsoft.Net.Component.4.6.2.TargetingPack | .NET Framework 4.6.2 目标包 | 17.1.32112.364 | 可选
Microsoft.Net.Component.4.7.1.TargetingPack | .NET Framework 4.7.1 目标包 | 17.1.32112.364 | 可选
Microsoft.Net.Component.4.7.TargetingPack | .NET Framework 4.7 目标包 | 17.1.32112.364 | 可选
Microsoft.Net.ComponentGroup.4.6.2-4.7.1.DeveloperTools | .NET Framework 4.6.2-4.7.1 开发工具 | 17.1.32112.364 | 可选

## <a name="universal-windows-platform-build-tools"></a>通用 Windows 平台生成工具

**ID：** Microsoft.VisualStudio.Workload.UniversalBuildTools

**描述：** 提供生成通用 Windows 平台应用程序所需的工具。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | “属性” | Version | 依赖项类型
--- | --- | --- | ---
Microsoft.Component.MSBuild | MSBuild | 17.1.32112.364 | 必需
Microsoft.Component.NetFX.Native | .NET Native | 17.1.32112.364 | 必需
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 17.1.32112.364 | 必须
Microsoft.NetCore.Component.Runtime.6.0 | .NET 6.0 运行时 | 17.1.32210.238 | 必需
Microsoft.NetCore.Component.SDK | .NET SDK | 17.1.32210.238 | 必需
Microsoft.VisualStudio.Component.NuGet.BuildTools | NuGet 目标和生成任务 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.ComponentGroup.UWP.BuildTools | 通用 Windows 平台生成必备组件 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Windows10SDK.19041 | Windows 10 SDK (10.0.19041.0) | 17.1.32112.364 | 建议
Component.Microsoft。Windows。CppWinRT | C++/WinRT | 2.0.210806.1 | 可选
Microsoft.Net.Component.4.7.2.SDK | .NET Framework 4.7.2 SDK | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.UWP.VC.ARM64 | C++ 通用Windows平台对 ARM64 (v143 生成工具)  | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.UWP.VC.ARM64EC | C++ Universal Windows Platform 支持 v143 生成工具 (ARM64EC - 试验)  | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.14.29.16.11.ARM64 | MSVC v142 - VS 2019 C++ ARM64 生成工具 (v14.29-16.11)  | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.CoreBuildTools | C++ 生成工具核心功能 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.Tools.ARM | MSVC v143 - VS 2022 C++ ARM 生成工具 (最新)  | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.Tools.ARM64 | MSVC v143 - VS 2022 C++ ARM64 生成工具 (最新)  | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.Tools.ARM64EC | MSVC v143 - VS 2022 C++ ARM64EC 生成工具 (最新 - 试验)  | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | MSVC v143 - VS 2022 C++ x64/x86 生成工具 (最新)  | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.v141.ARM | MSVC v141 – VS 2017 C++ ARM 生成工具 (v14.16) | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.v141.ARM64 | MSVC v141 – VS 2017 C++ ARM64 生成工具 (v14.16) | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.v141.x86.x64 | MSVC v141 - VS 2017 C++ x64/x86 生成工具 (v14.16) | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.Windows10SDK | Windows 通用 C 运行时 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.Windows10SDK.18362 | Windows 10 SDK (10.0.18362.0) | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.Windows11SDK.22000 | Windows 11 SDK (10.0.22000.0)  | 17.1.32112.364 | 可选
Microsoft.VisualStudio.ComponentGroup.UWP.VC.BuildTools | C++ (v143) 通用 Windows 平台工具 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.ComponentGroup.UWP.VC.v141.BuildTools | C++ (v141) 通用 Windows 平台工具 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.ComponentGroup.UWP.VC.v142.BuildTools | C++ (v142) 通用 Windows 平台工具 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.ComponentGroup.VC.Tools.142.x86.x64 | MSVC v142 - VS 2019 C++ x64/x86 生成工具 (v14.29) | 17.1.32112.364 | 可选

## <a name="desktop-development-with-c"></a>使用 C++ 的桌面开发

**ID：** Microsoft.VisualStudio.Workload.VCTools

**描述：** 使用所选工具（包括 MSVC、Clang、CMake 或 MSBuild）生成适用于 Windows 的新式 C++ 应用。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | “属性” | Version | 依赖项类型
--- | --- | --- | ---
Microsoft.Component.MSBuild | MSBuild | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.TextTemplating | 文本模板转换 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.VC.CoreBuildTools | C++ 生成工具核心功能 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.VC.CoreIde | C++ 核心功能 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.VC.Redist.14.Latest | C++ 2022 可再发行组件更新 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Windows10SDK | Windows 通用 C 运行时 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.ComponentGroup.NativeDesktop.Core | C++ 核心桌面功能 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.TestTools.BuildTools | 测试工具核心功能 - 生成工具 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.VC.ASAN | C++ AddressSanitizer | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.VC.CMake.Project | 用于 Windows 的 C++ CMake 工具 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | MSVC v143-VS 2022 c + + x64/x86 生成工具 (最新)  | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.Windows10SDK.19041 | Windows 10 SDK (10.0.19041.0) | 17.1.32112.364 | 建议
Microsoft.Component.VC.Runtime.UCRTSDK | Windows 通用 CRT SDK | 17.1.32112.364 | 可选
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 目标包 | 17.1.32112.364 | 可选
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.140 | MSVC v140 - VS 2015 C++ 生成工具 (v14.00) | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.ATL | 适用于最新 v143 生成工具的 c + + ATL (x86 & x64)  | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.ATLMFC | 适用于最新 v143 生成工具的 C++ MFC（x86 和 x64） | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.CLI.Support | C + +/CLI 支持 v143 生成工具 (最新)  | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.Llvm.Clang | 用于 Windows (13.0.0 的 c + + Clang 编译器)  | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.Llvm.ClangToolset | C + + Clang-cl for v143 build tools (x64/x86)  | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.Modules.x86.x64 | 适用于 v143 生成工具的 C++ 模块（x64/x86 - 实验性） | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.v141.x86.x64 | MSVC v141 - VS 2017 C++ x64/x86 生成工具 (v14.16) | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.Windows10SDK.18362 | Windows 10 SDK (10.0.18362.0) | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.Windows10SDK.20348 | Windows 10 SDK (10.0.20348.0) | 17.1.32112.364 | 可选
VisualStudio. Windows11SDK. 22000 | Windows 11 SDK (10.0.22000.0)  | 17.1.32112.364 | 可选
Microsoft.VisualStudio.ComponentGroup.NativeDesktop.Llvm.Clang | c + + Clang tools for Windows (13.0.0-x64/x86)  | 17.1.32112.364 | 可选
VisualStudio. ComponentGroup.. c e x | MSVC v142 - VS 2019 C++ x64/x86 生成工具 (v14.29) | 17.1.32112.364 | 可选

## <a name="visual-studio-extension-development"></a>Visual Studio 扩展开发

**ID：** Microsoft.VisualStudio.Workload.VisualStudioExtensionBuildTools

**描述：** 用于生成 Visual Studio 加载项和扩展的工具，其中包括新命令、代码分析器和工具窗口。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | “属性” | Version | 依赖项类型
--- | --- | --- | ---
Microsoft.Component.MSBuild | MSBuild | 17.1.32112.364 | 必需
Microsoft.Net.Component.4.6.TargetingPack | .NET Framework 4.6 目标包 | 17.1.32112.364 | 必需
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 目标包 | 17.1.32112.364 | 必需
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 17.1.32112.364 | 必需
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 开发工具 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.NuGet.BuildTools | NuGet 目标和生成任务 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.VSSDKBuildTools | Visual Studio SDK 生成工具核心 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.ComponentGroup.VisualStudioExtensionBuildTools.Prerequisites | Visual Studio 扩展开发必备组件 | 17.1.32112.364 | 必需
Component.Dotfuscator | PreEmptive Protection - Dotfuscator | 17.1.32112.364 | 可选
Microsoft.Component.VC.Runtime.OSSupport | 用于 v142 生成工具的 C++ 通用 Windows 平台运行时 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.ATL | 适用于最新 v143 生成工具的 c + + ATL (x86 & x64)  | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.ATLMFC | 适用于最新 v143 生成工具的 C++ MFC（x86 和 x64） | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | MSVC v143-VS 2022 c + + x64/x86 生成工具 (最新)  | 17.1.32112.364 | 可选

## <a name="web-development-build-tools"></a>Web 开发生成工具

**ID：** Microsoft.VisualStudio.Workload.WebBuildTools

**描述：** 用于生成 Web 应用程序的 MSBuild 任务和目标。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | “属性” | Version | 依赖项类型
--- | --- | --- | ---
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 目标包 | 17.1.32112.364 | 必需
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 17.1.32112.364 | 必需
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 开发工具 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.NuGet.BuildTools | NuGet 目标和生成任务 | 17.1.32112.364 | 必须
VisualStudio. TSServer。 | TypeScript 服务器 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Web.BuildTools.ComponentGroup | Web 开发生成工具 | 17.1.32112.364 | 必需
Microsoft.Component.ClickOnce.MSBuild | ClickOnce 生成工具 | 17.1.32112.364 | 建议
Microsoft.Net.Component.4.8.TargetingPack | .NET Framework 4.8 目标包 | 17.1.32112.364 | 建议
Microsoft.Net.ComponentGroup.4.8.DeveloperTools | .NET Framework 4.8 开发工具 | 17.1.32112.364 | 建议
Microsoft.NetCore.Component.Runtime.6.0 | .NET 6.0 运行时 | 17.1.32210.238 | 建议
Microsoft.NetCore.Component.SDK | .NET SDK | 17.1.32210.238 | 建议
Microsoft.VisualStudio.Component.DockerTools.BuildTools | 容器开发工具 - 生成工具 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.TestTools.BuildTools | 测试工具核心功能 - 生成工具 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.WebDeploy | Web Deploy | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Wcf.BuildTools.ComponentGroup | Windows Communication Foundation 生成工具 | 17.1.32112.364 | 建议
Microsoft.Net.Component.3.5.DeveloperTools | .NET Framework 3.5 开发工具 | 17.1.32112.364 | 可选
Microsoft.Net.Component.4.6.2.TargetingPack | .NET Framework 4.6.2 目标包 | 17.1.32112.364 | 可选
Microsoft.Net.Component.4.7.1.TargetingPack | .NET Framework 4.7.1 目标包 | 17.1.32112.364 | 可选
Microsoft.Net.Component.4.7.TargetingPack | .NET Framework 4.7 目标包 | 17.1.32112.364 | 可选
Microsoft.Net.ComponentGroup.4.6.2-4.7.1.DeveloperTools | .NET Framework 4.6.2-4.7.1 开发工具 | 17.1.32112.364 | 可选
microsoft.net.runtime.mono.tooling | 用于存储的共享本机Mono 运行时 | 6.0.222.10215 | 可选
microsoft.net.sdk.emscripten | Emscripten SDK 编译器工具 | 6.0.6.10204 | 可选
Microsoft.VisualStudio.Component.TypeScript.SDK.4.4 | TypeScript 4.4 SDK | 17.1.32112.364 | 可选
wasm.tools | .NET WebAssembly 生成工具 | 6.0.222.10215 | 可选

## <a name="mobile-development-with-net"></a>使用 .NET 的移动开发

**ID：** Microsoft.VisualStudio.Workload.XamarinBuildTools

**描述：** 用于使用 C# 和 F# 生成 iOS、Android 和 Windows 版跨平台应用程序的工具。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | “属性” | Version | 依赖项类型
--- | --- | --- | ---
Microsoft.Component.MSBuild | MSBuild | 17.1.32112.364 | 必需
Microsoft.Net.Component.4.6.1.TargetingPack | .NET Framework 4.6.1 目标包 | 17.1.32112.364 | 必需
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.NuGet.BuildTools | NuGet 目标和生成任务 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 17.1.32112.364 | 必须
Component.Android.SDK.MAUI | Android SDK API (31 级别设置)  | 17.1.32112.364 | 可选

## <a name="unaffiliated-components"></a>独立组件

这些组件不随附于任何工作负载，但可选择作为单个组件。

组件 ID | “属性” | 版本
--- | --- | ---
Microsoft.Net.Core.Component.SDK.2.1 | .NET Core 2.1 运行时 (不支持)  | 17.1.32210.238
Microsoft.NetCore.Component.Runtime.3.1 | .NET Core 3.1 运行时 (LTS) | 17.1.32210.238
Microsoft.NetCore.Component.Runtime.5.0 | .NET 5.0 运行时 | 17.1.32210.238
Microsoft.VisualStudio.Component.VC.14.29.16.11.ARM | MSVC v142 - VS 2019 C++ ARM 生成工具 (v14.29-16.11)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.29.16.11.ARM.Spectre | MSVC v142 - VS 2019 C++ ARM Spectre 缓解库 (v14.29-16.11)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.29.16.11.ARM64.Spectre | MSVC v142 - VS 2019 C++ ARM64 Spectre 缓解库 (v14.29-16.11)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.29.16.11.ATL | 适用于 v142 生成工具的 C++ v14.29 (16.11) ATL (x86 & x64)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.29.16.11.ATL.ARM | 适用于 v142 生成工具的 C++ v14.29 (16.11) ATL (ARM)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.29.16.11.ATL.ARM.Spectre | 适用于 v142 生成工具的 C++ v14.29 (16.11) ATL 和 Spectre 缓解 (ARM)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.29.16.11.ATL.ARM64 | 适用于 v142 生成工具的 C++ v14.29 (16.11) ATL (ARM64)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.29.16.11.ATL.ARM64.Spectre | 适用于 v142 生成工具的 C++ v14.29 (16.11) ATL 和 Spectre 缓解 (ARM64)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.29.16.11.ATL.Spectre | C++ v14.29 (16.11) ATL for v142 生成工具，具有 Spectre 缓解 (x86 & x64)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.29.16.11.CLI.Support | 14.29-16.11 (v142 生成工具的 C++/CLI)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.29.16.11.MFC | 适用于 v142 生成工具的 C++ v14.29 (16.11) MFC (x86 & x64)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.29.16.11.MFC.ARM | 适用于 V142 生成工具的 C++ v14.29 (16.11) MFC (ARM)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.29.16.11.MFC.ARM.Spectre | C++ v14.29 (16.11) MFC for v142 生成工具，具有 Spectre 缓解 (ARM)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.29.16.11.MFC.ARM64 | 适用于 v142 生成工具的 C++ v14.29 (16.11) MFC (ARM64)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.29.16.11.MFC.ARM64.Spectre | C++ v14.29 (16.11) MFC for v142 生成工具，具有 Spectre 缓解 (ARM64)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.29.16.11.MFC.Spectre | C++ v14.29 (16.11) MFC for v142 生成工具，具有 Spectre 缓解 (x86 & x64)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.29.16.11.x86.x64 | MSVC v142 - VS 2019 C++ x64/x86 生成工具 (v14.29-16.11)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.29.16.11.x86.x64.Spectre | MSVC v142 - VS 2019 C++ x64/x86 Spectre 缓解库 (v14.29-16.11)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.30.17.0.ARM | MSVC v143 - VS 2022 C++ ARM 生成工具 (v14.30-17.0)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.30.17.0.ARM.Spectre | MSVC v143 - VS 2022 C++ ARM Spectre 缓解库 (v14.30-17.0)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.30.17.0.ARM64 | MSVC v143 - VS 2022 C++ ARM64 生成工具 (v14.30-17.0)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.30.17.0.ARM64.Spectre | MSVC v143 - VS 2022 C++ ARM64 Spectre 缓解库 (v14.30-17.0)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.30.17.0.ATL | 适用于 v143 生成工具的 C++ v14.30 (17.0) ATL (x86 & x64)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.30.17.0.ATL.ARM | 适用于 V143 生成工具的 C++ v14.30 (17.0) ATL (ARM)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.30.17.0.ATL.ARM.Spectre | 适用于 v143 生成工具的 C++ v14.30 (17.0) ATL 和 Spectre 缓解 (ARM)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.30.17.0.ATL.ARM64 | 适用于 ARM64 (v143 生成工具的 C++ v14.30 (17.0) ATL (ATL)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.30.17.0.ATL.ARM64.Spectre | 适用于 v143 生成工具的 C++ v14.30 (17.0) ATL 和 Spectre 缓解 (ARM64)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.30.17.0.ATL.Spectre | 适用于 v143 生成工具的 C++ v14.30 (17.0) ATL (x86 & x64)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.30.17.0.CLI.Support | 14.30-17.0 (v143 生成工具的 C++/CLI)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.30.17.0.MFC | 适用于 v143 生成工具的 C++ v14.30 (17.0) MFC (x86 & x64)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.30.17.0.MFC.ARM | 适用于 v143 生成工具的 C++ v14.30 (17.0) MFC (ARM)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.30.17.0.MFC.ARM.Spectre | C++ v14.30 (17.0) MFC for v143 生成工具，具有 Spectre 缓解 (ARM)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.30.17.0.MFC.ARM64 | 适用于 v143 生成工具的 C++ v14.30 (17.0) MFC (ARM64)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.30.17.0.MFC.ARM64.Spectre | C++ v14.30 (17.0) MFC for v143 生成工具，具有 SPECtre 缓解措施 (ARM64)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.30.17.0.MFC.Spectre | C++ v14.30 (17.0) MFC for v143 生成工具，具有 Spectre 缓解 (x86 & x64)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.30.17.0.x86.x64 | MSVC v143 - VS 2022 C++ x64/x86 生成工具 (v14.30-17.0)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.30.17.0.x86.x64.Spectre | MSVC v143 - VS 2022 C++ x64/x86 Spectre 缓解库 (v14.30-17.0)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.31.17.1.ARM | MSVC v143 - VS 2022 C++ ARM 生成工具 (v14.31-17.1)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.31.17.1.ARM.Spectre | MSVC v143 - VS 2022 C++ ARM Spectre 缓解库 (v14.31-17.1)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.31.17.1.ARM64 | MSVC v143 - VS 2022 C++ ARM64 生成工具 (v14.31-17.1)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.31.17.1.ARM64.Spectre | MSVC v143 - VS 2022 C++ ARM64 Spectre 缓解库 (v14.31-17.1)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.31.17.1.ATL | 适用于 v143 生成工具的 C++ v14.31 (17.1) ATL (x86 & x64)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.31.17.1.ATL.ARM | 适用于) ARM (的 v143 生成工具的 C++ v14.31 (17.1) ATL (ATL | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.31.17.1.ATL.ARM.Spectre | 适用于 v143 生成工具的 C++ v14.31 (17.1) ATL 和 Spectre 缓解措施 (ARM)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.31.17.1.ATL.ARM64 | 适用于 ARM64 (v143 生成工具的 C++ v14.31 (17.1) ATL (ATL)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.31.17.1.ATL.ARM64.Spectre | 适用于 v143 生成工具的 C++ v14.31 (17.1) ATL 和 Spectre 缓解 (ARM64)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.31.17.1.ATL.Spectre | C++ v14.31 (17.1) ATL，适用于具有 Spectre 缓解措施的 v143 生成工具 (x86 & x64)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.31.17.1.CLI.Support | 针对 v143 生成工具的 C++/CLI (14.31-17.1)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.31.17.1.MFC | 适用于 v143 生成工具的 C++ v14.31 (17.1) MFC (x86 & x64)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.31.17.1.MFC.ARM | 适用于 V143 生成工具的 C++ v14.31 (17.1) MFC (ARM)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.31.17.1.MFC.ARM.Spectre | C++ v14.31 (17.1) MFC for v143 生成工具，具有 Spectre 缓解措施 (ARM)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.31.17.1.MFC.ARM64 | 适用于 V143 生成工具的 C++ v14.31 (17.1) MFC (ARM64)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.31.17.1.MFC.ARM64.Spectre | C++ v14.31 (17.1) MFC for v143 生成工具，具有 Spectre 缓解 (ARM64)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.31.17.1.MFC.Spectre | C++ v14.31 (17.1) MFC，适用于具有 Spectre 缓解措施的 v143 生成工具 (x86 & x64)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.31.17.1.x86.x64 | MSVC v143 - VS 2022 C++ x64/x86 生成工具 (v14.31-17.1)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.31.17.1.x86.x64.Spectre | MSVC v143 - VS 2022 C++ x64/x86 Spectre 缓解库 (v14.31-17.1)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.ATL.ARM | 适用于 ARM (的最新 v143 生成工具的 C++ ATL)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.ATL.ARM.Spectre | 具有 Spectre 缓解措施的最新 v143 生成工具的 C++ ATL (ARM)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.ATL.ARM64 | 适用于最新 v143 生成工具的 C++ ATL (ARM64)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.ATL.ARM64.Spectre | 具有 Spectre 缓解措施的最新 v143 生成工具的 C++ ATL (ARM64)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.ATL.ARM64EC | 适用于最新 v143 生成工具的 C++ ATL (ARM64EC - 试验)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.ATL.ARM64EC.Spectre | 具有 Spectre 缓解措施的最新 v143 生成工具的 C++ ATL (ARM64EC - 试验)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.ATL.Spectre | 具有 Spectre 缓解措施的最新 v143 生成工具的 C++ ATL (x86 & x64)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.ATLMFC.Spectre | 具有 Spectre 缓解措施的最新 v143 生成工具的 C++ MFC (x86 & x64)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.MFC.ARM | 适用于最新 v143 生成工具的 c + + MFC (ARM)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.MFC.ARM.Spectre | C + + MFC，适用于最新的 v143 生成工具，Spectre 缓解 (ARM)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.MFC.ARM64 | C + + MFC for 最新的 v143 生成工具 (ARM64)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.MFC.ARM64.Spectre | C + + MFC，适用于带有 Spectre 缓解 (ARM64) 的最新 v143 生成工具 | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.MFC.ARM64EC | C + + MFC for 最新的 v143 生成工具 (ARM64EC-试验性)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.MFC.ARM64EC.Spectre | C + + MFC，适用于带有 Spectre 缓解 (ARM64EC 的最新 v143 生成工具-试验性)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.Redist.MSM | C + + 2022 可再发行 MSMs | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.Runtimes.ARM.Spectre | MSVC v143-2022 c + + ARM Spectre (最新)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.Runtimes.ARM64.Spectre |  (最新) MSVC v143-VS 2022 c + + ARM64 Spectre | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.Runtimes.ARM64EC.Spectre | MSVC v143-VS 2022 c + + ARM64EC Spectre)  ( | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.Runtimes.x86.x64.Spectre |  (最新) MSVC v143-VS 2022 c + + x64/x86 Spectre  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.v141.ARM.Spectre | MSVC v141 – VS 2017 C++ ARM Spectre 缓解库 (v14.16) | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.v141.ARM64.Spectre | MSVC v141 – VS 2017 C++ ARM64 Spectre 缓解库 (v14.16) | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.v141.ATL | C++ ATL for v141 生成工具 (x86 & x64) | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.v141.ATL.ARM | C++ ATL for v141 生成工具 (ARM) | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.v141.ATL.ARM.Spectre | 带有 Spectre 缓解措施的 C++ ATL for v141 生成工具 (ARM) | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.v141.ATL.ARM64 | C++ ATL for v141 生成工具 (ARM64) | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.v141.ATL.ARM64.Spectre | 带有 Spectre 缓解措施的 C++ ATL for v141 生成工具 (ARM64) | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.v141.ATL.Spectre | 带有 Spectre 缓解措施的 C++ ATL for v141 生成工具（x86 和 x64） | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.v141.CLI.Support | v141 生成工具的 C++/CLI 支持 (14.16) | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.v141.MFC | C++ MFC for v141 生成工具（x86 和 x64） | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.v141.MFC.ARM | C++ MFC for v141 生成工具 (ARM) | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.v141.MFC.ARM.Spectre | 带有 Spectre 缓解措施的 C++ MFC for v141 生成工具 (ARM) | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.v141.MFC.ARM64 | C++ MFC for v141 生成工具 (ARM64) | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.v141.MFC.ARM64.Spectre | 带有 Spectre 缓解措施的 C++ MFC for v141 生成工具 (ARM64) | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.v141.MFC.Spectre | 带有 Spectre 缓解措施的 C++ MFC for v141 生成工具 (x86 & x64) | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.v141.x86.x64.Spectre | MSVC v141 – VS 2017 C++ x64/x86 Spectre 缓解库 (v14.16) | 17.1.32112.364
Microsoft.VisualStudio.Component.WinXP | VS 2017 (v141) 工具的 C++ Windows XP 支持 [已弃用] | 17.1.32112.364

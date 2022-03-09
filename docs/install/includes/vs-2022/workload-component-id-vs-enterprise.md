---
title: Visual Studio Enterprise 2022 工作负荷和组件 id
titleSuffix: ''
description: 使用工作负载和组件 ID 通过命令行安装 Visual Studio 或指定为 VSIX 清单中的依赖项
keywords: ''
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.date: 02/15/2022
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.topic: include
ms.openlocfilehash: 9ded6245664255f64d187911a05de82f8fe75ca1
ms.sourcegitcommit: edf8137cd90c67b6078a02c93094f7e1c3bf8930
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2022
ms.locfileid: "139552339"
---
## <a name="visual-studio-core-editor-included-with-visual-studio-enterprise-2022"></a>Visual Studio 核心编辑器 (包含 Visual Studio Enterprise 2022) 

**ID：** Microsoft.VisualStudio.Workload.CoreEditor

**描述：** Visual Studio 核心 shell 体验，包括语法感知代码编辑、源代码管理和工作项管理。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | “属性” | Version | 依赖项类型
--- | --- | --- | ---
Microsoft.VisualStudio.Component.CoreEditor | Visual Studio 核心编辑器 | 17.1.32112.364 | 必须

## <a name="azure-development"></a>Azure 开发

**ID：** Microsoft.VisualStudio.Workload.Azure

**说明：** 使用 .NET 和 .NET Framework 开发云应用和创建资源的 Azure SDK、工具和项目。 还包括用于容器化应用程序的工具，包括 Docker 支持。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | “属性” | Version | 依赖项类型
--- | --- | --- | ---
Component.Microsoft.VisualStudio.RazorExtension | Razor 语言服务 | 17.1.32112.364 | 必需
Component.Microsoft.VisualStudio.Web.AzureFunctions | Azure WebJobs 工具 | 17.1.32112.364 | 必需
Component.Microsoft.Web.LibraryManager | 库管理器 | 17.1.32112.364 | 必选
Component.Microsoft.WebTools.BrowserLink.WebLivePreview | Web 直播预览 | 17.1.70.52095 | 必须
Microsoft.Component.ClickOnce | ClickOnce 发布 | 17.1.32112.364 | 必需
Microsoft.Component.MSBuild | MSBuild | 17.1.32112.364 | 必需
Microsoft.ComponentGroup.ClickOnce.Publish | 适用于 .NET 的 ClickOnce 发布  | 17.1.32112.364 | 必需
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 目标包 | 17.1.32112.364 | 必需
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 17.1.32112.364 | 必需
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 开发工具 | 17.1.32112.364 | 必需
Microsoft.NetCore.Component.DevelopmentTools | .NET 开发工具 | 17.1.32112.364 | 必须
NetCore。6.0 版 | .NET 6.0 运行时 | 17.1.32210.238 | 必需
Microsoft.NetCore.Component.SDK | .NET SDK | 17.1.32210.238 | 必需
Microsoft.NetCore.Component.Web | 适用于 .NET 的 Web 开发工具 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Azure.ClientLibs | .NET 的 Azure 库 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Common.Azure.Tools | 连接和发布工具 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.DockerTools | 容器开发工具 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.FSharp | F# 语言支持 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.FSharp.WebTemplates | 针对 Web 项目的 F# 语言支持 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 诊断 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript 和 TypeScript 语言支持 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.ManagedDesktop.Core | 托管桌面工作负载核心 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.MSODBC.SQL | SQL Server ODBC 驱动程序 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.MSSQL.CMDLnUtils | SQL Server 命令行实用工具 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.NuGet | NuGet 程序包管理器 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# 和 Visual Basic | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server 的 CLR 数据类型 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.SQL.DataSources | SQL Server 支持的数据源 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2019 LocalDB | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.TextTemplating | 文本模板转换 | 17.1.32112.364 | 必须
VisualStudio. TSServer。 | TypeScript 服务器 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Web | ASP.NET 和 web 开发先决条件 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.ComponentGroup.Azure.Prerequisites | Azure 开发必备组件 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.ComponentGroup.AzureFunctions | Azure WebJobs 工具 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.ComponentGroup.Web | ASP.NET 和 web 开发先决条件 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET 和 Web 开发 | 17.1.32112.364 | 必需
Microsoft.Component.Azure.DataLake.Tools | Azure Data Lake 和流分析工具 | 17.1.32112.364 | 建议
Microsoft.Net.Component.4.8.TargetingPack | .NET Framework 4.8 目标包 | 17.1.32112.364 | 建议
Microsoft.Net.ComponentGroup.4.8.DeveloperTools | .NET Framework 4.8 开发工具 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.AppInsights.Tools | 开发人员分析工具 | 17.1.32112.364 | 建议
VisualStudio。 | .NET Framework 项目和项模板 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.AspNet45 | 高级 ASP.NET 功能 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.Azure.AuthoringTools | Azure 创作工具 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.Azure.Compute.Emulator | Azure 计算仿真程序 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.Azure.Powershell | Azure Powershell | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.Azure.ResourceManager.Tools | Azure 资源管理器核心工具 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.Azure.ServiceFabric.Tools | Service Fabric 工具 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.Azure.Waverton | Azure 云服务核心工具 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.Azure.Waverton.BuildTools | Azure 云服务生成工具 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.Debugger.Snapshot | 快照调试程序 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.DiagnosticTools | .NET 分析工具 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.IntelliTrace.FrontEnd | IntelliTrace | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.WebDeploy | Web Deploy | 17.1.32112.364 | 建议
Microsoft.VisualStudio.ComponentGroup.Azure.CloudServices | Azure 云服务工具 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.ComponentGroup.Azure.ResourceManager.Tools | Azure 资源管理器工具 | 17.1.32112.364 | 建议
Microsoft.Net.Component.4.6.2.TargetingPack | .NET Framework 4.6.2 目标包 | 17.1.32112.364 | 可选
Microsoft.Net.Component.4.7.1.TargetingPack | .NET Framework 4.7.1 目标包 | 17.1.32112.364 | 可选
Microsoft.Net.Component.4.7.TargetingPack | .NET Framework 4.7 目标包 | 17.1.32112.364 | 可选
Microsoft.Net. ComponentGroup. 4.6.2-4.7.1. DeveloperTools | .NET Framework 4.6.2-4.7.1 开发工具 | 17.1.32112.364 | 可选
VisualStudio （& a） | TypeScript 4.4 SDK | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.Wcf.Tooling | Windows Communication Foundation | 17.1.32112.364 | 可选

## <a name="data-storage-and-processing"></a>数据存储和处理

**ID：** Microsoft.VisualStudio.Workload.Data

**描述：** 使用 SQL Server、Azure Data Lake 或 Hadoop 连接、开发和测试数据解决方案。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | “属性” | Version | 依赖项类型
--- | --- | --- | ---
Microsoft.Component.Azure.DataLake.Tools | Azure Data Lake 和流分析工具 | 17.1.32112.364 | 建议
Microsoft.Component.ClickOnce | ClickOnce 发布 | 17.1.32112.364 | 建议
Microsoft.Component.MSBuild | MSBuild | 17.1.32112.364 | 建议
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 目标包 | 17.1.32112.364 | 建议
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 17.1.32112.364 | 建议
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 开发工具 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.Common.Azure.Tools | 连接和发布工具 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.ManagedDesktop.Core | 托管桌面工作负载核心 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.MSODBC.SQL | SQL Server ODBC 驱动程序 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.MSSQL.CMDLnUtils | SQL Server 命令行实用工具 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.NuGet | NuGet 程序包管理器 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# 和 Visual Basic | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server 的 CLR 数据类型 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2019 LocalDB | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.TextTemplating | 文本模板转换 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.FSharp.Desktop | F# 桌面语言支持 | 17.1.32112.364 | 可选

## <a name="data-science-and-analytical-applications"></a>数据科学和分析应用程序

**ID：** Microsoft.VisualStudio.Workload.DataScience

**描述：** 用于创建数据科学应用程序的语言和工具，包括 Python 和 F#。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | “属性” | Version | 依赖项类型
--- | --- | --- | ---
Microsoft.Component.PythonTools | Python 语言支持 | 17.1.32112.364 | 建议
Microsoft.Component.PythonTools.Web | Python Web 支持 | 17.1.32112.364 | 建议
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 目标包 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.Common.Azure.Tools | 连接和发布工具 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.FSharp.Desktop | F# 桌面语言支持 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript 和 TypeScript 语言支持 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.NuGet | NuGet 程序包管理器 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# 和 Visual Basic | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.TypeScript.TSServer | TypeScript 服务器 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.WebDeploy | Web Deploy | 17.1.32112.364 | 建议
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET 和 Web 开发 | 17.1.32112.364 | 建议
Microsoft.ComponentGroup.PythonTools.NativeDevelopment | Python 本机开发工具 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.Graphics.Tools | 适用于 DirectX 的图形调试器和 GPU 探查器 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.TypeScript.SDK.4.4 | TypeScript 4.4 SDK | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.CoreIde | C++ 核心功能 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.DiagnosticTools | C++ 分析工具 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | MSVC v143 - VS 2022 C++ x64/x86 生成工具 (最新)  | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.Windows10SDK | Windows 通用 C 运行时 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.Windows10SDK.19041 | Windows 10 SDK (10.0.19041.0) | 17.1.32112.364 | 可选

## <a name="net-desktop-development"></a>.NET 桌面开发

**ID：** Microsoft.VisualStudio.Workload.ManagedDesktop

说明：将 C#、Visual Basic 和 F# 与 .NET 和 NET Framework 一起使用，生成 WPF、Windows 窗体和控制台应用程序。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | “属性” | Version | 依赖项类型
--- | --- | --- | ---
Microsoft.Component.ClickOnce | ClickOnce 发布 | 17.1.32112.364 | 必需
Microsoft.Component.MSBuild | MSBuild | 17.1.32112.364 | 必需
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 目标包 | 17.1.32112.364 | 必需
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 17.1.32112.364 | 必需
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 开发工具 | 17.1.32112.364 | 必须
Microsoft.NetCore.Component.Runtime.6.0 | .NET 6.0 运行时 | 17.1.32210.238 | 必需
Microsoft.NetCore.Component.SDK | .NET SDK | 17.1.32210.238 | 必需
Microsoft.VisualStudio.Component.ManagedDesktop.Core | 托管桌面工作负载核心 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.ManagedDesktop.Prerequisites | .NET 桌面开发工具 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# 和 Visual Basic | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server 的 CLR 数据类型 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.TextTemplating | 文本模板转换 | 17.1.32112.364 | 必须
Component.Microsoft.VisualStudio.LiveShare.2022 | Live Share | 1.0.5117 | 建议
Microsoft.ComponentGroup.Blend | Blend for Visual Studio | 17.1.32112.364 | 建议
Microsoft.ComponentGroup.ClickOnce.Publish | 适用于 .NET 的 ClickOnce 发布  | 17.1.32112.364 | 建议
Microsoft.Net.Component.4.8.TargetingPack | .NET Framework 4.8 目标包 | 17.1.32112.364 | 建议
Microsoft.Net.ComponentGroup.4.8.DeveloperTools | .NET Framework 4.8 开发工具 | 17.1.32112.364 | 建议
Microsoft.NetCore.Component.DevelopmentTools | 用于 .NET 的开发工具 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.Debugger.JustInTime | 实时调试器 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.DiagnosticTools | .NET 分析工具 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.DotNetModelBuilder | ML.NET Model Builder | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.EntityFramework | Entity Framework 6 工具 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.FSharp | F# 语言支持 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.IntelliTrace.FrontEnd | IntelliTrace | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript 和 TypeScript 语言支持 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.LiveUnitTesting | Live Unit Testing | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.NuGet | NuGet 程序包管理器 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.TypeScript.TSServer | TypeScript 服务器 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET 和 Web 开发 | 17.1.32112.364 | 建议
Component.Dotfuscator | PreEmptive Protection - Dotfuscator | 17.1.32112.364 | 可选
Component.Microsoft.VisualStudio.RazorExtension | Razor 语言服务 | 17.1.32112.364 | 可选
Component.Microsoft.Web.LibraryManager | 库管理器 | 17.1.32112.364 | 可选
Component.Microsoft.WebTools.BrowserLink.WebLivePreview | Web 直播预览 | 17.1.70.52095 | 可选
Microsoft.Net.Component.4.6.2.TargetingPack | .NET Framework 4.6.2 目标包 | 17.1.32112.364 | 可选
Microsoft.Net.Component.4.7.1.TargetingPack | .NET Framework 4.7.1 目标包 | 17.1.32112.364 | 可选
Microsoft.Net.Component.4.7.TargetingPack | .NET Framework 4.7 目标包 | 17.1.32112.364 | 可选
Microsoft.Net. ComponentGroup. 4.6.2-4.7.1. DeveloperTools | .NET Framework 4.6.2-4.7.1 开发工具 | 17.1.32112.364 | 可选
Microsoft.NetCore.Component.Web | 适用于 .NET 的 Web 开发工具 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.AppInsights.Tools | 开发人员分析工具 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.ClassDesigner | 类设计器 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.CodeClone | 代码克隆 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.CodeMap | 代码图 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.Common.Azure.Tools | 连接和发布工具 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.DependencyValidation.Enterprise | 实时依赖项验证 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.DockerTools | 容器开发工具 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.FSharp.Desktop | F# 桌面语言支持 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.FSharp.WebTemplates | 针对 Web 项目的 F# 语言支持 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.GraphDocument | DGML 编辑器 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 诊断 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.MSODBC.SQL | SQL Server ODBC 驱动程序 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.MSSQL.CMDLnUtils | SQL Server 命令行实用工具 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.PortableLibrary | .NET 可移植库目标包 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.SQL.DataSources | SQL Server 支持的数据源 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2019 LocalDB | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 17.1.32112.364 | 可选
VisualStudio （& a） | TypeScript 4.4 SDK | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.Wcf.Tooling | Windows Communication Foundation | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.Web | ASP.NET 和 web 开发先决条件 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.WebDeploy | Web Deploy | 17.1.32112.364 | 可选
Microsoft.VisualStudio.ComponentGroup.ArchitectureTools.Managed | 体系结构和分析工具 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.ComponentGroup.MSIX.Packaging | MSIX 打包工具 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.ComponentGroup.Web | ASP.NET 和 web 开发先决条件 | 17.1.32112.364 | 可选
VisualStudio. ComponentGroup. WindowsAppSDK | Windows App SDK c # 模板 | 17.1.32112.364 | 可选

## <a name="game-development-with-unity"></a>使用 Unity 的游戏开发

**ID：** Microsoft.VisualStudio.Workload.ManagedGame

**描述：** 使用 Unity（功能强大的跨平台开发环境）创建 2D 和 3D 游戏。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | “属性” | Version | 依赖项类型
--- | --- | --- | ---
Microsoft.Net.Component.4.7.1.TargetingPack | .NET Framework 4.7.1 目标包 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.NuGet | NuGet 程序包管理器 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# 和 Visual Basic | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Unity | Visual Studio Tools for Unity | 17.1.32112.364 | 必需
Component.UnityEngine.x64 | Unity Hub | 17.1.32112.364 | 建议

## <a name="linux-and-embedded-development-with-c"></a>带有 c + + 的 Linux 和嵌入式开发

**ID：** Microsoft.VisualStudio.Workload.NativeCrossPlat

**说明：** 创建和调试在 Linux 环境或嵌入式设备上运行的应用程序。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | “属性” | Version | 依赖项类型
--- | --- | --- | ---
Component.MDD.Linux | 适用于 Linux 开发的 C++ | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.VC.CoreIde | C++ 核心功能 | 17.1.32112.364 | 必需
Component.Linux.CMake | 适用于 Linux 的 C++ CMake 工具 | 17.1.32112.364 | 建议
VisualStudio。 | 嵌入和 IoT 工具 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 17.1.32112.364 | 建议
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET 和 Web 开发 | 17.1.32112.364 | 建议
Component.MDD.Linux.GCC.arm | 旧版嵌入和 IoT 工具 | 17.1.32112.364 | 可选

## <a name="desktop-development-with-c"></a>使用 C++ 的桌面开发

**ID：** Microsoft.VisualStudio.Workload.NativeDesktop

**描述：** 使用所选工具（包括 MSVC、Clang、CMake 或 MSBuild）生成适用于 Windows 的新式 C++ 应用。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | “属性” | Version | 依赖项类型
--- | --- | --- | ---
Microsoft.Component.MSBuild | MSBuild | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.ClassDesigner | 类设计器 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.CodeMap | 代码图 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.GraphDocument | DGML 编辑器 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2019 LocalDB | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.TextTemplating | 文本模板转换 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.VC.CoreIde | C++ 核心功能 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.VC.Redist.14.Latest | C + + 2022 可再发行更新 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.ComponentGroup.ArchitectureTools.Native | 适用于 C++ 的体系结构工具 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.ComponentGroup.NativeDesktop.Core | C++ 核心桌面功能 | 17.1.32112.364 | 必须
VisualStudio. LiveShare。 | Live Share | 1.0.5117 | 建议
Microsoft.VisualStudio.Component.Debugger.JustInTime | 实时调试器 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.Graphics.Tools | 适用于 DirectX 的图形调试器和 GPU 探查器 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.IntelliTrace.FrontEnd | IntelliTrace | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript 和 TypeScript 语言支持 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.NuGet | NuGet 程序包管理器 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# 和 Visual Basic | 17.1.32112.364 | 建议
VisualStudio. TSServer。 | TypeScript 服务器 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.VC.ASAN | C++ AddressSanitizer | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.VC.ATL | 适用于最新 v143 生成工具的 c + + ATL (x86 & x64)  | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.VC.CMake.Project | 用于 Windows 的 C++ CMake 工具 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.VC.DiagnosticTools | C++ 分析工具 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.VC.TestAdapterForBoostTest | Boost.Test 测试适配器 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.VC.TestAdapterForGoogleTest | Google Test 测试适配器 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | MSVC v143 - VS 2022 C++ x64/x86 生成工具 (最新)  | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.Windows10SDK.19041 | Windows 10 SDK (10.0.19041.0) | 17.1.32112.364 | 建议
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET 和 Web 开发 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions.CMake | JSON 编辑器 | 17.1.32112.364 | 建议
Component.Incredibuild | Incredibuild - 生成加速 | 17.1.32112.464 | 可选
Component.IncredibuildMenu | IncredibuildMenu | 1.6.0.2 | 可选
Component.Microsoft。Windows。CppWinRT | C++/WinRT | 2.0.210806.1 | 可选
Microsoft.Component.VC.Runtime.UCRTSDK | Windows 通用 CRT SDK | 17.1.32112.364 | 可选
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 目标包 | 17.1.32112.364 | 可选
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 诊断 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.TypeScript.SDK.4.4 | TypeScript 4.4 SDK | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.UWP.VC.ARM64 | C++ 通用Windows平台对 ARM64 (v143 生成工具)  | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.UWP.VC.ARM64EC | C++ Universal Windows Platform 支持 v143 生成工具 (ARM64EC - 试验)  | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.140 | MSVC v140 - VS 2015 C++ 生成工具 (v14.00) | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.ATLMFC | 适用于最新 v143 生成工具的 C++ MFC（x86 和 x64） | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.CLI.Support | 对 v143 生成工具的 C++/CLI 支持 (最新)  | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.CoreBuildTools | C++ 生成工具核心功能 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.Llvm.Clang | 适用于 13.0.0 Windows (的 C++ Clang 编译器)  | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.Llvm.ClangToolset | 适用于 v143 生成工具的 C++ Clang-cl (x64/x86)  | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.Modules.x86.x64 | 适用于 v143 生成工具的 C++ 模块（x64/x86 - 实验性） | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.Tools.ARM | MSVC v143 - VS 2022 C++ ARM 生成工具 (最新)  | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.Tools.ARM64 | MSVC v143 - VS 2022 C++ ARM64 生成工具 (最新)  | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.Tools.ARM64EC | MSVC v143 - VS 2022 C++ ARM64EC 生成工具 (最新 - 试验)  | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.v141.x86.x64 | MSVC v141 - VS 2017 C++ x64/x86 生成工具 (v14.16) | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.Windows10SDK | Windows 通用 C 运行时 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.Windows10SDK.18362 | Windows 10 SDK (10.0.18362.0) | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.Windows10SDK.20348 | Windows 10 SDK (10.0.20348.0) | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.Windows11SDK.22000 | Windows 11 SDK (10.0.22000.0)  | 17.1.32112.364 | 可选
Microsoft.VisualStudio.ComponentGroup.MSIX.Packaging | MSIX 打包工具 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.ComponentGroup.NativeDesktop.Llvm.Clang | 适用于 Windows (13.0.0 的 C++ Clang 工具 - x64/x86)  | 17.1.32112.364 | 可选
Microsoft.VisualStudio.ComponentGroup.UWP.VC | C++ (v143) 通用 Windows 平台工具 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.ComponentGroup.VC.Tools.142.x86.x64 | MSVC v142 - VS 2019 C++ x64/x86 生成工具 (v14.29) | 17.1.32112.364 | 可选
Microsoft.VisualStudio.ComponentGroup.WindowsAppSDK.Cpp | Windows应用 SDK C++ 模板 | 17.1.32112.364 | 可选

## <a name="game-development-with-c"></a>使用 C++ 的游戏开发

**ID：** Microsoft.VisualStudio.Workload.NativeGame

**描述：** 以 DirectX、Unreal 或 Cocos2d 为后盾，利用 C++ 的强大功能生成专业游戏。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | “属性” | Version | 依赖项类型
--- | --- | --- | ---
Microsoft.VisualStudio.Component.VC.CoreIde | C++ 核心功能 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.VC.Redist.14.Latest | C++ 2022 可再发行组件更新 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | MSVC v143 - VS 2022 C++ x64/x86 生成工具 (最新)  | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Windows10SDK | Windows 通用 C 运行时 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Graphics.Tools | 适用于 DirectX 的图形调试器和 GPU 探查器 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.IntelliTrace.FrontEnd | IntelliTrace | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.VC.ASAN | C++ AddressSanitizer | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.VC.DiagnosticTools | C++ 分析工具 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.Windows10SDK.19041 | Windows 10 SDK (10.0.19041.0) | 17.1.32112.364 | 建议
Component.Android.NDK.R21E | Android NDK (R21E) | 17.1.32112.364 | 可选
Component.Android.SDK25.Private | Android SDK 安装（API 级别 25）（使用 C++ 的移动开发的本地安装） | 17.1.32112.364 | 可选
Component.Ant | Apache Ant (1.9.3) | 1.9.3.8 | 可选
Component.Cocos | Cocos | 17.1.32112.364 | 可选
Component.Incredibuild | Incredibuild - 生成加速 | 17.1.32112.464 | 可选
Component.IncredibuildMenu | IncredibuildMenu | 1.6.0.2 | 可选
Component.MDD.Android | C++ Android 开发工具 | 17.1.32112.364 | 可选
Component.OpenJDK | OpenJDK（Microsoft 分发） | 17.1.32112.364 | 可选
Component.Unreal | Unreal 引擎安装程序 | 17.1.32112.364 | 可选
Component.Unreal.Android | 适用于 Unreal 引擎的 Android IDE 支持 | 17.1.32112.364 | 可选
Microsoft.Net.Component.4.6.2.TargetingPack | .NET Framework 4.6.2 目标包 | 17.1.32112.364 | 可选
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 目标包 | 17.1.32112.364 | 可选
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 17.1.32112.364 | 可选
Microsoft.Net.Component.4.8.TargetingPack | .NET Framework 4.8 目标包 | 17.1.32112.364 | 可选
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 开发工具 | 17.1.32112.364 | 可选
Microsoft.Net.ComponentGroup.TargetingPacks.Common | .NET Framework 4.8 开发工具 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.NuGet.BuildTools | NuGet 目标和生成任务 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# 和 Visual Basic | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.Windows10SDK.18362 | Windows 10 SDK (10.0.18362.0) | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.Windows10SDK.20348 | Windows 10 SDK (10.0.20348.0) | 17.1.32112.364 | 可选
VisualStudio. Windows11SDK. 22000 | Windows 11 SDK (10.0.22000.0)  | 17.1.32112.364 | 可选

## <a name="mobile-development-with-c"></a>使用 C++ 的移动开发

**ID：** Microsoft.VisualStudio.Workload.NativeMobile

**描述：** 使用 C++ 生成适用于 iOS、Android 或 Windows 的跨平台应用程序。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | “属性” | Version | 依赖项类型
--- | --- | --- | ---
Component.Android.SDK25.Private | Android SDK 安装（API 级别 25）（使用 C++ 的移动开发的本地安装） | 17.1.32112.364 | 必需
Component.OpenJDK | OpenJDK（Microsoft 分发） | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.VC.CoreIde | C++ 核心功能 | 17.1.32112.364 | 必须
R21E。 | Android NDK (R21E) | 17.1.32112.364 | 建议
Component.Ant | Apache Ant (1.9.3) | 1.9.3.8 | 建议
Component.MDD.Android | C++ Android 开发工具 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 17.1.32112.364 | 建议
Component.Google.Android.Emulator.API25.Private | Google Android Emulator（API 级别 25）（本地安装） | 17.1.32112.364 | 可选
Component.HAXM.Private | Intel 硬件加速执行管理器 (HAXM)（本地安装） | 17.1.32112.364 | 可选
Component.Incredibuild | Incredibuild - 生成加速 | 17.1.32112.464 | 可选
Component.IncredibuildMenu | IncredibuildMenu | 1.6.0.2 | 可选
Component.MDD.IOS | C++ iOS 开发工具 | 17.1.32112.364 | 可选

## <a name="mobile-development-with-net"></a>使用 .NET 的移动开发

**ID：** Microsoft.VisualStudio.Workload.NetCrossPlat

**描述：** 使用 Xamarin 生成适用于 iOS、Android 或 Windows 的跨平台应用程序。 这包括 .NET MAUI 工作负荷的预览，作为可选安装。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | “属性” | Version | 依赖项类型
--- | --- | --- | ---
Microsoft.Component.MSBuild | MSBuild | 17.1.32112.364 | 必需
Microsoft.ComponentGroup.ClickOnce.Publish | 适用于 .NET 的 ClickOnce 发布  | 17.1.32112.364 | 必需
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 目标包 | 17.1.32112.364 | 必需
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 17.1.32112.364 | 必需
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 开发工具 | 17.1.32112.364 | 必需
Microsoft.NetCore.Component.DevelopmentTools | .NET 开发工具 | 17.1.32112.364 | 必须
NetCore。6.0 版 | .NET 6.0 运行时 | 17.1.32210.238 | 必需
Microsoft.NetCore.Component.SDK | .NET SDK | 17.1.32210.238 | 必需
Microsoft.VisualStudio.Component.FSharp | F# 语言支持 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.NuGet | NuGet 程序包管理器 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# 和 Visual Basic | 17.1.32112.364 | 必须
MAUI。 | Android SDK 安装 (API 级别 31)  | 17.1.32112.364 | 建议
Component.OpenJDK | OpenJDK（Microsoft 分发） | 17.1.32112.364 | 建议
Component.Xamarin | Xamarin | 17.1.32112.364 | 建议
Component.Xamarin.RemotedSimulator | Xamarin 远程模拟器 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.Merq | 常见 Xamarin 内部工具 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.MonoDebugger | Mono 调试程序 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions.TemplateEngine | ASP.NET 模板化引擎 | 17.1.32112.364 | 建议

## <a name="aspnet-and-web-development"></a>ASP.NET 和 Web 开发

**ID：** Microsoft.VisualStudio.Workload.NetWeb

**描述：** 使用 ASP.NET Core、ASP.NET、HTML/JavaScript 和包括 Docker 支持的容器生成 Web 应用程序。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | “属性” | Version | 依赖项类型
--- | --- | --- | ---
Component.Microsoft.VisualStudio.RazorExtension | Razor 语言服务 | 17.1.32112.364 | 必需
Component.Microsoft.Web.LibraryManager | 库管理器 | 17.1.32112.364 | 必选
Component.Microsoft.WebTools.BrowserLink.WebLivePreview | Web 直播预览 | 17.1.70.52095 | 必须
Microsoft.Component.ClickOnce | ClickOnce 发布 | 17.1.32112.364 | 必需
Microsoft.Component.MSBuild | MSBuild | 17.1.32112.364 | 必需
Microsoft.ComponentGroup.ClickOnce.Publish | 适用于 .NET 的 ClickOnce 发布  | 17.1.32112.364 | 必需
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 目标包 | 17.1.32112.364 | 必需
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 17.1.32112.364 | 必需
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 开发工具 | 17.1.32112.364 | 必需
Microsoft.NetCore.Component.DevelopmentTools | 用于 .NET 的开发工具 | 17.1.32112.364 | 必须
Microsoft.NetCore.Component.Runtime.6.0 | .NET 6.0 运行时 | 17.1.32210.238 | 必需
Microsoft.NetCore.Component.SDK | .NET SDK | 17.1.32210.238 | 必需
Microsoft.NetCore.Component.Web | 适用于 .NET 的 Web 开发工具 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Common.Azure.Tools | 连接和发布工具 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.DockerTools | 容器开发工具 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.FSharp | F# 语言支持 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.FSharp.WebTemplates | 针对 Web 项目的 F# 语言支持 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 诊断 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript 和 TypeScript 语言支持 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.ManagedDesktop.Core | 托管桌面工作负载核心 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.MSODBC.SQL | SQL Server ODBC 驱动程序 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.MSSQL.CMDLnUtils | SQL Server 命令行实用工具 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.NuGet | NuGet 程序包管理器 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# 和 Visual Basic | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server 的 CLR 数据类型 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.SQL.DataSources | SQL Server 支持的数据源 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2019 LocalDB | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.TextTemplating | 文本模板转换 | 17.1.32112.364 | 必须
VisualStudio. TSServer。 | TypeScript 服务器 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Web | ASP.NET 和 web 开发先决条件 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.ComponentGroup.Web | ASP.NET 和 web 开发先决条件 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET 和 Web 开发 | 17.1.32112.364 | 必须
VisualStudio. LiveShare。 | Live Share | 1.0.5117 | 建议
Component.Microsoft.VisualStudio.Web.AzureFunctions | Azure WebJobs 工具 | 17.1.32112.364 | 建议
Microsoft.Net.Component.4.8.TargetingPack | .NET Framework 4.8 目标包 | 17.1.32112.364 | 建议
Microsoft.Net.ComponentGroup.4.8.DeveloperTools | .NET Framework 4.8 开发工具 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.AppInsights.Tools | 开发人员分析工具 | 17.1.32112.364 | 建议
VisualStudio。 | .NET Framework 项目和项模板 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.AspNet45 | 高级 ASP.NET 功能 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.Debugger.JustInTime | 实时调试器 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.Debugger.Snapshot | 快照调试程序 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.DiagnosticTools | .NET 分析工具 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.EntityFramework | Entity Framework 6 工具 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.IntelliTrace.FrontEnd | IntelliTrace | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.LiveUnitTesting | Live Unit Testing | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.WebDeploy | Web Deploy | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.WslDebugging | 使用 WSL 进行 .NET 调试 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.ComponentGroup.AzureFunctions | Azure WebJobs 工具 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.ComponentGroup.Web.CloudTools | 用于 Web 开发的云工具 | 17.1.32112.364 | 建议
Microsoft.Net.Component.4.5.2.TargetingPack | .NET Framework 4.5.2 目标包 | 17.1.32112.364 | 可选
Microsoft.Net.Component.4.6.2.TargetingPack | .NET Framework 4.6.2 目标包 | 17.1.32112.364 | 可选
Microsoft.Net.Component.4.7.1.TargetingPack | .NET Framework 4.7.1 目标包 | 17.1.32112.364 | 可选
Microsoft.Net.Component.4.7.TargetingPack | .NET Framework 4.7 目标包 | 17.1.32112.364 | 可选
Microsoft.Net. ComponentGroup. 4.6.2-4.7.1. DeveloperTools | .NET Framework 4.6.2-4.7.1 开发工具 | 17.1.32112.364 | 可选
"net.tcp"。 | Mono 运行时的共享本机生成工具 | 6.0.222.10215 | 可选
emscripten。 | Emscripten SDK 编译器工具 | 6.0.6.10204 | 可选
Microsoft.VisualStudio.Component.ClassDesigner | 类设计器 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.CodeClone | 代码克隆 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.CodeMap | 代码图 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.DependencyValidation.Enterprise | 实时依赖项验证 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.GraphDocument | DGML 编辑器 | 17.1.32112.364 | 可选
VisualStudio. TeamsFx | Microsoft Teams 开发工具 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.TestTools.WebLoadTest | Web 性能和负载测试工具 | 17.1.32112.364 | 可选
VisualStudio （& a） | TypeScript 4.4 SDK | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.Wcf.Tooling | Windows Communication Foundation | 17.1.32112.364 | 可选
Microsoft.VisualStudio.ComponentGroup.AdditionalWebProjectTemplates | 其他项目模板（早期版本） | 17.1.32112.364 | 可选
Microsoft.VisualStudio.ComponentGroup.ArchitectureTools.Managed | 体系结构和分析工具 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.ComponentGroup.IISDevelopment | 开发时 IIS 支持 | 17.1.32112.364 | 可选
wasm.tools | .NET WebAssembly 生成工具 | 6.0.222.10215 | 可选

## <a name="nodejs-development"></a>Node.js 开发

**ID：** Microsoft.VisualStudio.Workload.Node

**描述：** 使用 Node.js（一个由异步事件驱动的 JavaScript 运行时）生成可缩放的网络应用程序。 

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | “属性” | Version | 依赖项类型
--- | --- | --- | ---
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 诊断 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript 和 TypeScript 语言支持 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Node.Tools | Node.js 开发工具 | 17.1.32112.364 | 必须
Microsoft.VisualStudio.Component.TypeScript.TSServer | TypeScript 服务器 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET 和 Web 开发 | 17.1.32112.364 | 必须
Component.Microsoft.VisualStudio.LiveShare.2022 | Live Share | 1.0.5117 | 建议
Microsoft.VisualStudio.Component.Debugger.JustInTime | 实时调试器 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# 和 Visual Basic | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.WebDeploy | Web Deploy | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.AppInsights.Tools | 开发人员分析工具 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.Common.Azure.Tools | 连接和发布工具 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.TypeScript.SDK.4.4 | TypeScript 4.4 SDK | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.CoreIde | C++ 核心功能 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | MSVC v143 - VS 2022 C++ x64/x86 生成工具 (最新)  | 17.1.32112.364 | 可选

## <a name="officesharepoint-development"></a>Office/SharePoint 开发

**ID：** Microsoft.VisualStudio.Workload.Office

**描述：** 使用 C#、VB 和 JavaScript 创建 Office 和 SharePoint 外接程序、SharePoint 解决方案和 VSTO 外接程序。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | “属性” | Version | 依赖项类型
--- | --- | --- | ---
Component.Microsoft.VisualStudio.RazorExtension | Razor 语言服务 | 17.1.32112.364 | 必需
Component.Microsoft.Web.LibraryManager | 库管理器 | 17.1.32112.364 | 必选
Component.Microsoft.WebTools.BrowserLink.WebLivePreview | Web 直播预览 | 17.1.70.52095 | 必须
Microsoft.Component.ClickOnce | ClickOnce 发布 | 17.1.32112.364 | 必需
Microsoft.Component.MSBuild | MSBuild | 17.1.32112.364 | 必需
Microsoft.ComponentGroup.ClickOnce.Publish | 适用于 .NET 的 ClickOnce 发布  | 17.1.32112.364 | 必需
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 目标包 | 17.1.32112.364 | 必需
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 17.1.32112.364 | 必需
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 开发工具 | 17.1.32112.364 | 必需
Microsoft.NetCore.Component.DevelopmentTools | 用于 .NET 的开发工具 | 17.1.32112.364 | 必须
Microsoft.NetCore.Component.Runtime.6.0 | .NET 6.0 运行时 | 17.1.32210.238 | 必需
Microsoft.NetCore.Component.SDK | .NET SDK | 17.1.32210.238 | 必需
Microsoft.NetCore.Component.Web | 适用于 .NET 的 Web 开发工具 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.AppInsights.Tools | 开发人员分析工具 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Common.Azure.Tools | 连接和发布工具 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.DockerTools | 容器开发工具 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.FSharp | F# 语言支持 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.FSharp.WebTemplates | 针对 Web 项目的 F# 语言支持 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 诊断 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript 和 TypeScript 语言支持 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.ManagedDesktop.Core | 托管桌面工作负载核心 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.ManagedDesktop.Prerequisites | .NET 桌面开发工具 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.MSODBC.SQL | SQL Server ODBC 驱动程序 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.MSSQL.CMDLnUtils | SQL Server 命令行实用工具 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.NuGet | NuGet 程序包管理器 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# 和 Visual Basic | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Sharepoint.Tools | Visual Studio 的 Office 开发工具 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server 的 CLR 数据类型 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.SQL.DataSources | SQL Server 支持的数据源 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2019 LocalDB | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.TextTemplating | 文本模板转换 | 17.1.32112.364 | 必须
Microsoft.VisualStudio.Component.TypeScript.TSServer | TypeScript 服务器 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Wcf.Tooling | Windows Communication Foundation | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Web | ASP.NET 和 Web 开发先决条件 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Workflow | Windows Workflow Foundation | 17.1.32112.364 | 必需
Microsoft.VisualStudio.ComponentGroup.Web | ASP.NET 和 Web 开发先决条件 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET 和 Web 开发 | 17.1.32112.364 | 必须
Microsoft.Net.Component.4.8.TargetingPack | .NET Framework 4.8 目标包 | 17.1.32112.364 | 建议
Microsoft.Net.ComponentGroup.4.8.DeveloperTools | .NET Framework 4.8 开发工具 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.TeamOffice | Visual Studio Tools for Office (VSTO) | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.WebDeploy | Web Deploy | 17.1.32112.364 | 建议
Microsoft.Net.Component.4.6.2.TargetingPack | .NET Framework 4.6.2 目标包 | 17.1.32112.364 | 可选
Microsoft.Net.Component.4.7.1.TargetingPack | .NET Framework 4.7.1 目标包 | 17.1.32112.364 | 可选
Microsoft.Net.Component.4.7.TargetingPack | .NET Framework 4.7 目标包 | 17.1.32112.364 | 可选
Microsoft.Net.ComponentGroup.4.6.2-4.7.1.DeveloperTools | .NET Framework 4.6.2-4.7.1 开发工具 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.IntelliTrace.FrontEnd | IntelliTrace | 17.1.32112.364 | 可选
VisualStudio （& a） | TypeScript 4.4 SDK | 17.1.32112.364 | 可选
Microsoft.VisualStudio.ComponentGroup.Sharepoint.WIF | Windows Identity Foundation 3.5 | 17.1.32112.364 | 可选

## <a name="python-development"></a>Python 开发

**ID：** Microsoft.VisualStudio.Workload.Python

**描述：** 对 Python 进行编辑、调试、交互式开发和源代码管理。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | “属性” | Version | 依赖项类型
--- | --- | --- | ---
Microsoft.Component.PythonTools | Python 语言支持 | 17.1.32112.364 | 必须
CPython39 | Python 3 64 位 (3.9.7)  | 3.9.7 | 可选
VisualStudio. LiveShare。 | Live Share | 1.0.5117 | 可选
Component.Microsoft.VisualStudio.RazorExtension | Razor 语言服务 | 17.1.32112.364 | 可选
Component.Microsoft.Web.LibraryManager | 库管理器 | 17.1.32112.364 | 可选
Component.Microsoft.WebTools.BrowserLink.WebLivePreview | Web 直播预览 | 17.1.70.52095 | 可选
Microsoft.Component.ClickOnce | ClickOnce 发布 | 17.1.32112.364 | 可选
Microsoft.Component.MSBuild | MSBuild | 17.1.32112.364 | 可选
Microsoft.Component.PythonTools.Web | Python Web 支持 | 17.1.32112.364 | 可选
Microsoft.ComponentGroup.ClickOnce.Publish | 适用于 .NET 的 ClickOnce 发布  | 17.1.32112.364 | 可选
Microsoft.ComponentGroup.PythonTools.NativeDevelopment | Python 本机开发工具 | 17.1.32112.364 | 可选
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 目标包 | 17.1.32112.364 | 可选
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 17.1.32112.364 | 可选
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 开发工具 | 17.1.32112.364 | 可选
Microsoft.NetCore.Component.DevelopmentTools | .NET 开发工具 | 17.1.32112.364 | 可选
NetCore。6.0 版 | .NET 6.0 运行时 | 17.1.32210.238 | 可选
Microsoft.NetCore.Component.SDK | .NET SDK | 17.1.32210.238 | 可选
Microsoft.NetCore.Component.Web | 适用于 .NET 的 Web 开发工具 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.AppInsights.Tools | 开发人员分析工具 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.Azure.AuthoringTools | Azure 创作工具 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.Azure.ClientLibs | .NET 的 Azure 库 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.Azure.Compute.Emulator | Azure 计算仿真程序 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.Azure.Waverton | Azure 云服务核心工具 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.Azure.Waverton.BuildTools | Azure 云服务生成工具 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.Common.Azure.Tools | 连接和发布工具 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.Debugger.JustInTime | 实时调试器 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.DockerTools | 容器开发工具 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.FSharp | F# 语言支持 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.FSharp.WebTemplates | 针对 Web 项目的 F# 语言支持 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.Graphics.Tools | 适用于 DirectX 的图形调试器和 GPU 探查器 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.IISExpress | IIS Express  | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.JavaScript.Diagnostics | JavaScript 诊断 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.JavaScript.TypeScript | JavaScript 和 TypeScript 语言支持 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.ManagedDesktop.Core | 托管桌面工作负载核心 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.MSODBC.SQL | SQL Server ODBC 驱动程序 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.MSSQL.CMDLnUtils | SQL Server 命令行实用工具 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.NuGet | NuGet 程序包管理器 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# 和 Visual Basic | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server 的 CLR 数据类型 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.SQL.DataSources | SQL Server 支持的数据源 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2019 LocalDB | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.SQL.SSDT | SQL Server Data Tools | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.TextTemplating | 文本模板转换 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.TypeScript.SDK.4.4 | TypeScript 4.4 SDK | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.TypeScript.TSServer | TypeScript 服务器 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.CoreIde | C++ 核心功能 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.DiagnosticTools | C++ 分析工具 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | MSVC v143 - VS 2022 C++ x64/x86 生成工具 (最新)  | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.Web | ASP.NET 和 Web 开发先决条件 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.WebDeploy | Web Deploy | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.Windows10SDK | Windows 通用 C 运行时 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.Windows10SDK.19041 | Windows 10 SDK (10.0.19041.0) | 17.1.32112.364 | 可选
Microsoft.VisualStudio.ComponentGroup.Web | ASP.NET 和 Web 开发先决条件 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.ComponentGroup.WebToolsExtensions | ASP.NET 和 Web 开发 | 17.1.32112.364 | 可选

## <a name="universal-windows-platform-development"></a>通用 Windows 平台开发

**ID：** Microsoft.VisualStudio.Workload.Universal

**描述：** 使用 C#、VB、或可选 C++ 为通用 Windows 平台创建应用程序。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | “属性” | Version | 依赖项类型
--- | --- | --- | ---
Microsoft.Component.NetFX.Native | .NET Native | 17.1.32112.364 | 必需
Microsoft.ComponentGroup.Blend | Blend for Visual Studio | 17.1.32112.364 | 必须
Microsoft.NetCore.Component.Runtime.6.0 | .NET 6.0 运行时 | 17.1.32210.238 | 必需
Microsoft.NetCore.Component.SDK | .NET SDK | 17.1.32210.238 | 必需
Microsoft.VisualStudio.Component.AppInsights.Tools | 开发人员分析工具 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.DiagnosticTools | .NET 分析工具 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Graphics | 图像和 3D 模型编辑器 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.NuGet | NuGet 程序包管理器 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# 和 Visual Basic | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.SQL.CLR | SQL Server 的 CLR 数据类型 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Windows10SDK.19041 | Windows 10 SDK (10.0.19041.0) | 17.1.32112.364 | 必需
Microsoft.VisualStudio.ComponentGroup.MSIX.Packaging | MSIX 打包工具 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.ComponentGroup.UWP.NetCoreAndStandard | .NET 本机和 .NET 标准 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.ComponentGroup.UWP.Support | 通用 Windows 平台工具 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.ComponentGroup.UWP.Xamarin | 适用于 Xamarin 的通用 Windows 平台工具 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.IntelliTrace.FrontEnd | IntelliTrace | 17.1.32112.364 | 建议
Component.Microsoft。Windows。CppWinRT | C++/WinRT | 2.0.210806.1 | 可选
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.ClassDesigner | 类设计器 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.CodeClone | 代码克隆 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.CodeMap | 代码图 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.DependencyValidation.Enterprise | 实时依赖项验证 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.GraphDocument | DGML 编辑器 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.Graphics.Tools | 适用于 DirectX 的图形调试器和 GPU 探查器 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.SQL.LocalDB.Runtime | SQL Server Express 2019 LocalDB | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.UWP.VC.ARM64 | C++ 通用Windows平台对 ARM64 (v143 生成工具)  | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.UWP.VC.ARM64EC | C++ Universal Windows Platform 支持 v143 生成工具 (ARM64EC - 试验)  | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.14.29.16.11.ARM | MSVC v142 - VS 2019 C++ ARM 生成工具 (v14.29-16.11)  | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.14.29.16.11.ARM64 | MSVC v142 - VS 2019 C++ ARM64 生成工具 (v14.29-16.11)  | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.CoreBuildTools | C++ 生成工具核心功能 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.CoreIde | C++ 核心功能 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.Tools.ARM | MSVC v143 - VS 2022 C++ ARM 生成工具 (最新)  | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.Tools.ARM64 | MSVC v143 - VS 2022 C++ ARM64 生成工具 (最新)  | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.Tools.ARM64EC | MSVC v143 - VS 2022 C++ ARM64EC 生成工具 (最新 - 试验)  | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.Tools.x86.x64 | MSVC v143 - VS 2022 C++ x64/x86 生成工具 (最新)  | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.v141.ARM | MSVC v141 – VS 2017 C++ ARM 生成工具 (v14.16) | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.v141.ARM64 | MSVC v141 – VS 2017 C++ ARM64 生成工具 (v14.16) | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.VC.v141.x86.x64 | MSVC v141 - VS 2017 C++ x64/x86 生成工具 (v14.16) | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.Windows10SDK | Windows 通用 C 运行时 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.Windows10SDK.18362 | Windows 10 SDK (10.0.18362.0) | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.Windows10SDK.IpOverUsb | USB 设备连接性 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.Windows11SDK.22000 | Windows 11 SDK (10.0.22000.0)  | 17.1.32112.364 | 可选
Microsoft.VisualStudio.ComponentGroup.ArchitectureTools.Managed | 体系结构和分析工具 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.ComponentGroup.UWP.VC | C++ (v143) 通用 Windows 平台工具 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.ComponentGroup.UWP.VC.v141 | C++ (v141) 通用 Windows 平台工具 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.ComponentGroup.UWP.VC.v142 | C++ (v142) 通用 Windows 平台工具 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.ComponentGroup.VC.Tools.142.x86.x64 | MSVC v142 - VS 2019 C++ x64/x86 生成工具 (v14.29) | 17.1.32112.364 | 可选

## <a name="visual-studio-extension-development"></a>Visual Studio 扩展开发

**ID：** Microsoft.VisualStudio.Workload.VisualStudioExtension

**描述：** 为 Visual Studio 创建加载项和扩展，包括新命令、代码分析器和工具窗口。

### <a name="components-included-by-this-workload"></a>此工作负载所包含的组件

组件 ID | “属性” | Version | 依赖项类型
--- | --- | --- | ---
Microsoft.Component.MSBuild | MSBuild | 17.1.32112.364 | 必需
Microsoft.Net.Component.4.6.TargetingPack | .NET Framework 4.6 目标包 | 17.1.32112.364 | 必需
Microsoft.Net.Component.4.7.2.TargetingPack | .NET Framework 4.7.2 目标包 | 17.1.32112.364 | 必需
Microsoft.Net.Component.4.8.SDK | .NET Framework 4.8 SDK | 17.1.32112.364 | 必需
Microsoft.Net.ComponentGroup.DevelopmentPrerequisites | .NET Framework 4.7.2 开发工具 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.NuGet | NuGet 程序包管理器 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Roslyn.Compiler | C# 和 Visual Basic Roslyn 编译器 | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.Roslyn.LanguageServices | C# 和 Visual Basic | 17.1.32112.364 | 必需
Microsoft.VisualStudio.Component.VSSDK | Visual Studio SDK | 17.1.32112.364 | 必需
Microsoft.VisualStudio.ComponentGroup.VisualStudioExtension.Prerequisites | Visual Studio 扩展开发必备组件 | 17.1.32112.364 | 必须
Microsoft.Component.CodeAnalysis.SDK | .NET 编译器平台 SDK | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.DiagnosticTools | .NET 分析工具 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.IntelliCode | IntelliCode | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.IntelliTrace.FrontEnd | IntelliTrace | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.TextTemplating | 文本模板转换 | 17.1.32112.364 | 建议
Microsoft.VisualStudio.Component.AppInsights.Tools | 开发人员分析工具 | 17.1.32112.364 | 可选
Microsoft.VisualStudio.Component.DslTools | 建模 SDK | 17.1.32112.364 | 可选

## <a name="unaffiliated-components"></a>独立组件

这些组件不随附于任何工作负载，但可选择作为单个组件。

组件 ID | “属性” | 版本
--- | --- | ---
Component.Xamarin.Profiler | Xamarin Profiler | 17.1.32112.364
Microsoft.Component.HelpViewer | 帮助查看器 | 17.1.32112.364
Microsoft.Net.Component.3.5.DeveloperTools | .NET Framework 3.5 开发工具 | 17.1.32112.364
Microsoft.Net.Component.4.6.1.SDK | .NET Framework 4.6.1 SDK | 17.1.32112.364
Microsoft.Net.Component.4.6.2.SDK | .NET Framework 4.6.2 SDK | 17.1.32112.364
Microsoft.Net.Component.4.7.1.SDK | .NET Framework 4.7.1 SDK | 17.1.32112.364
Microsoft.Net.Component.4.7.2.SDK | .NET Framework 4.7.2 SDK | 17.1.32112.364
Microsoft.Net.Component.4.7.SDK | .NET Framework 4.7 SDK | 17.1.32112.364
Microsoft.Net.Core.Component.SDK.2.1 | .NET Core 2.1 运行时 (不支持)  | 17.1.32210.238
Microsoft.NetCore.Component.Runtime.3.1 | .NET Core 3.1 运行时 (LTS) | 17.1.32210.238
Microsoft.NetCore.Component.Runtime.5.0 | .NET 5.0 运行时 | 17.1.32210.238
Microsoft.NetCore.ComponentGroup.DevelopmentTools.2.1 | .NET Core 2.1 开发工具 (不支持)  | 17.1.32112.364
Microsoft.NetCore.ComponentGroup.Web.2.1 | .NET Core 2.1 的 Web 开发工具 (不支持)  | 17.1.32112.364
Microsoft.VisualStudio.Component.AzureDevOps.OfficeIntegration | Azure DevOps Office 集成 | 17.1.32112.364
Microsoft.VisualStudio.Component.Git | 用于 Windows 的 Git | 17.1.32112.364
Microsoft.VisualStudio.Component.LinqToSql | LINQ to SQL 工具 | 17.1.32112.364
Microsoft.VisualStudio.Component.TestTools.CodedUITest | 编码的 UI 测试 | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.29.16.11.ARM.Spectre | MSVC v142 - VS 2019 C++ ARM Spectre 缓解库 (v14.29-16.11)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.29.16.11.ARM64.Spectre | MSVC v142 - VS 2019 C++ ARM64 Spectre 缓解库 (v14.29-16.11)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.29.16.11.ATL | 适用于 v142 生成工具的 C++ v14.29 (16.11) ATL (x86 & x64)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.29.16.11.ATL.ARM | 适用于 v142 生成工具的 C++ v14.29 (16.11) ATL (ARM)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.29.16.11.ATL.ARM.Spectre | 适用于 v142 生成工具的 C++ v14.29 (16.11) ATL 和 Spectre 缓解 (ARM)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.29.16.11.ATL.ARM64 | 适用于 v142 生成工具的 C++ v14.29 (16.11) ATL (ARM64)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.29.16.11.ATL.ARM64.Spectre | 适用于 v142 生成工具的 C++ v14.29 (16.11) ATL 和 Spectre 缓解 (ARM64)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.29.16.11.ATL.Spectre | C++ v14.29 (16.11) ATL for v142 生成工具，具有 Spectre 缓解 (x86 & x64)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.29.16.11.CLI.Support | 14.29-16.11 (v142 生成工具的 C++/CLI)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.14.29.16.11.MFC | C + + v 14.29 (16.11) 用于 v142 生成工具的 MFC (x86 & x64)  | 17.1.32112.364
VisualStudio （14.29.16.11）中的 | C + + v 14.29 (16.11) 用于 v142 生成工具的 MFC (ARM)  | 17.1.32112.364
VisualStudio. 14.29.16.11. Spectre. 的 | C + + v 14.29 (16.11) 用于 v142 生成工具的 MFC (ARM 的 Spectre 缓解)  | 17.1.32112.364
VisualStudio. 14.29.16.11. ARM64。 | C + + v 14.29 (16.11) 用于 v142 生成工具的 MFC (ARM64)  | 17.1.32112.364
VisualStudio. 14.29.16.11. ARM64. Spectre。 | C + + v 14.29 (16.11) 用于 v142 生成工具的 MFC 用于 Spectre 缓解 (ARM64)  | 17.1.32112.364
VisualStudio. 14.29.16.11. Spectre。 | C + + v 14.29 (16.11) 用于 v142 生成工具的 MFC (x86 & x64)  | 17.1.32112.364
VisualStudio. 14.29.16.11. c e x | MSVC v142-VS 2019 c + + x64/x86 生成工具 (v 14.29-16.11)  | 17.1.32112.364
VisualStudio. 14.29.16.11. Spectre 的。 | MSVC v142-VS 2019 c + + x64/x86 Spectre- (14.29-16.11)  | 17.1.32112.364
VisualStudio （14.30.17.0）。 | MSVC v143-VS 2022 c + + ARM 生成工具 (v 14.30-17.0)  | 17.1.32112.364
VisualStudio. 14.30.17.0 Spectre。 | MSVC v143-VS 2022 c + + ARM Spectre-缓解库 (v 14.30-17.0)  | 17.1.32112.364
VisualStudio. 14.30.17.0. ARM64 | MSVC v143-VS 2022 c + + ARM64 生成工具 (v 14.30-17.0)  | 17.1.32112.364
VisualStudio. 14.30.17.0. ARM64. Spectre | MSVC v143-VS 2022 c + + ARM64 Spectre 缓解库 (v 14.30-17.0)  | 17.1.32112.364
VisualStudio. 14.30.17.0。 | C + + v 14.30 (17.0) ATL for v143 build tools (x86 & x64)  | 17.1.32112.364
VisualStudio。14.30.17.0 的部分。 | C + + v 14.30 (17.0) ATL for v143 build tools (ARM)  | 17.1.32112.364
VisualStudio. 14.30.17.0 Spectre.。 | C + + v 14.30 (17.0) ATL for v143 build tools with Spectre 缓解 () ARM | 17.1.32112.364
VisualStudio. 14.30.17.0 ARM64。 | C + + v 14.30 (17.0) ATL for v143 build tools (ARM64)  | 17.1.32112.364
VisualStudio. 14.30.17.0. ARM64. Spectre。 | C + + v 14.30 (17.0) ATL for v143 build tools with Spectre 缓解 (ARM64)  | 17.1.32112.364
VisualStudio. 14.30.17.0 Spectre。 | C + + v 14.30 (17.0) ATL for v143 build tools with Spectre 缓解 (x86 & x64)  | 17.1.32112.364
VisualStudio 支持（& 14.30.17.0） | C + +/CLI 支持 v143 生成工具 (14.30-17.0)  | 17.1.32112.364
VisualStudio （14.30.17.0）。 | C + + v 14.30 (17.0) 用于 v143 生成工具的 MFC (x86 & x64)  | 17.1.32112.364
VisualStudio （14.30.17.0）中的 | C + + v 14.30 (17.0) 用于 v143 生成工具的 MFC (ARM)  | 17.1.32112.364
VisualStudio. 14.30.17.0. Spectre. 的 | C + + v 14.30 (17.0) 用于 v143 生成工具的 MFC (ARM 的 Spectre 缓解)  | 17.1.32112.364
VisualStudio. 14.30.17.0. ARM64。 | C + + v 14.30 (17.0) 用于 v143 生成工具的 MFC (ARM64)  | 17.1.32112.364
VisualStudio. 14.30.17.0. ARM64. Spectre。 | C + + v 14.30 (17.0) 用于 v143 生成工具的 MFC 用于 Spectre 缓解 (ARM64)  | 17.1.32112.364
VisualStudio. 14.30.17.0. Spectre。 | C + + v 14.30 (17.0) 用于 v143 生成工具的 MFC (x86 & x64)  | 17.1.32112.364
VisualStudio. 14.30.17.0. c e x | MSVC v143-VS 2022 c + + x64/x86 生成工具 (v 14.30-17.0)  | 17.1.32112.364
VisualStudio. 14.30.17.0. Spectre 的。 | MSVC v143-VS 2022 c + + x64/x86 Spectre- (14.30-17.0)  | 17.1.32112.364
VisualStudio （14.31.17.1）。 | MSVC v143-VS 2022 c + + ARM 生成工具 (v 14.31-17.1)  | 17.1.32112.364
VisualStudio. 14.31.17.1 Spectre。 | MSVC v143-VS 2022 c + + ARM Spectre-缓解库 (v 14.31-17.1)  | 17.1.32112.364
VisualStudio. 14.31.17.1. ARM64 | MSVC v143-VS 2022 c + + ARM64 生成工具 (v 14.31-17.1)  | 17.1.32112.364
VisualStudio. 14.31.17.1. ARM64. Spectre | MSVC v143-VS 2022 c + + ARM64 Spectre 缓解库 (v 14.31-17.1)  | 17.1.32112.364
VisualStudio. 14.31.17.1。 | C + + v 14.31 (17.1) ATL for v143 build tools (x86 & x64)  | 17.1.32112.364
VisualStudio。14.31.17.1 的部分。 | C + + v 14.31 (17.1) ATL for v143 build tools (ARM)  | 17.1.32112.364
VisualStudio. 14.31.17.1 Spectre.。 | C + + v 14.31 (17.1) ATL for v143 build tools with Spectre 缓解 () ARM | 17.1.32112.364
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
Microsoft.VisualStudio.Component.VC.MFC.ARM | 适用于最新 v143 生成工具的 C++ MFC (ARM)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.MFC.ARM.Spectre | 具有 Spectre 缓解措施的最新 v143 生成工具的 C++ MFC (ARM)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.MFC.ARM64 | 适用于最新 v143 生成工具的 C++ MFC (ARM64)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.MFC.ARM64.Spectre | 具有 Spectre 缓解措施的最新 v143 生成工具的 C++ MFC (ARM64)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.MFC.ARM64EC | 适用于最新 v143 生成工具的 C++ MFC (ARM64EC - 试验)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.MFC.ARM64EC.Spectre | 具有 Spectre 缓解措施的最新 v143 生成工具的 C++ MFC (ARM64EC - 试验)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.Redist.MSM | C++ 2022 可再发行 MSM | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.Runtimes.ARM.Spectre | MSVC v143 - VS 2022 C++ ARM Spectre 缓解库 (最新)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.Runtimes.ARM64.Spectre | MSVC v143 - VS 2022 C++ ARM64 Spectre 缓解库 (最新)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.Runtimes.ARM64EC.Spectre | MSVC v143 - VS 2022 C++ ARM64EC Spectre 缓解库 (最新 - 试验)  | 17.1.32112.364
Microsoft.VisualStudio.Component.VC.Runtimes.x86.x64.Spectre | MSVC v143 - VS 2022 C++ x64/x86 Spectre 缓解库 (最新)   | 17.1.32112.364
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
Microsoft.VisualStudio.Component.VisualStudioData | 数据源和服务引用 | 17.1.32112.364
Microsoft.VisualStudio.Component.WinXP | VS 2017 (v141) 工具的 C++ Windows XP 支持 [已弃用] | 17.1.32112.364
Microsoft.VisualStudio.Web.Mvc4.ComponentGroup | ASP.NET MVC 4 | 17.1.32112.364

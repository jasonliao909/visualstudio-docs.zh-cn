---
title: 启用或安装第一方 .NET 分析器
ms.date: 08/03/2018
description: 了解如何从 .NET SDK 启用第一方 .NET 分析器，或将这些分析器安装为NuGet包。
ms.custom: SEO-VS-2020
ms.topic: how-to
helpviewer_keywords:
- .NET analyzers
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-code-analysis
ms.workload:
- dotnet
ms.openlocfilehash: 25d98bfd0ddbc691c6fbc1ce22a129f9c6cfa692
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122091274"
---
# <a name="enable-or-install-first-party-net-analyzers"></a>启用或安装第一方 .NET 分析器

## <a name="overview"></a>概述

.NET Compiler Platform (Roslyn) 分析器会检查 C# 或 Visual Basic 代码的代码质量和代码样式问题。 第一方 .NET 分析器与 **目标平台无关**。 也就是说，项目不需要面向特定的 .NET 平台。 分析器适用于面向 以及早期 .NET 版本（如 `net5.0` 、 和 ） `netcoreapp` `netstandard` 的项目 `net472` 。

可以通过以下方式之一启用或安装第一方 .NET 分析器：

- **从 .NET SDK 启用**：从 Visual Studio 2019 16.8 和 .NET 5.0 开始，这些分析器包含在 [.NET SDK 中](/dotnet/fundamentals/code-analysis/overview)。 分析功能针对面向 .NET 5.0 或更高版本的项目默认启用。 可以通过将 MSBUILD [EnableNETAnalyzers](/dotnet/core/project-sdk/msbuild-props#enablenetanalyzers) 属性设置为 ，对面向早期 .NET 版本的项目启用代码分析 `true` 。 你也可通过将 `EnableNETAnalyzers` 设置为 `false`，对项目禁用代码分析。

- 作为 **NuGet** 包安装：如果不想移动到 .NET 5+ SDK，或者想要使用基于 NuGet 包的模型，分析器也可在 `Microsoft.CodeAnalysis.NetAnalyzers` Visual Studio 2019 上的 [NuGet](https://www.nuget.org/packages/Microsoft.CodeAnalysis.NetAnalyzers)包中使用。  对于按需版本更新，你可能更倾向于使用基于包的模型。 如果使用 2017 Visual Studio，请改为安装最新版本NuGet `2.9.x` `Microsoft.CodeAnalysis.FxCopAnalyzers` [包](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/)。

> [!NOTE]
> 建议在可能的情况下从 .NET SDK 启用分析器 `Microsoft.CodeAnalysis.NetAnalyzers` [，NuGet包](https://www.nuget.org/packages/Microsoft.CodeAnalysis.NetAnalyzers)。 从 .NET SDK 启用分析器可确保在更新 SDK 后自动获取分析器 bug 修复和新分析器。 在 NuGet模型中，每次需要最新的 bug 修复NuGet更新包。 更新NuGet更新包。

## <a name="see-also"></a>请参阅

- [中代码分析器Visual Studio](roslyn-analyzers-overview.md)
- [在 Visual Studio 中使用代码分析器](use-roslyn-analyzers.md)
- [从旧版分析迁移到 .NET 分析器](migrate-from-legacy-analysis-to-net-analyzers.md)
- [从 FxCop 分析器迁移到 .NET 分析器](migrate-from-fxcop-analyzers-to-net-analyzers.md)

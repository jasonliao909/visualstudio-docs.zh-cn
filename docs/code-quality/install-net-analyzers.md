---
title: 启用或安装第一方 .NET 分析器
ms.date: 01/13/2022
description: 了解如何从 .NET SDK 启用第一方 .NET 分析器，或将这些分析器作为 NuGet 包安装。
ms.custom: SEO-VS-2020, devdivchpfy22
ms.topic: how-to
helpviewer_keywords:
- .NET analyzers
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-code-analysis
ms.workload:
- dotnet
ms.openlocfilehash: 15d4322fdd50f3d6c71bf00ef6f5c1a7bbaefceb
ms.sourcegitcommit: 2a8c7de72f952203289459736107c875837bb07e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/20/2022
ms.locfileid: "137110083"
---
# <a name="enable-or-install-first-party-net-analyzers"></a>启用或安装第一方 .NET 分析器

## <a name="overview"></a>概述

.NET Compiler Platform (Roslyn) 分析器会检查 C# 或 Visual Basic 代码的代码质量和代码样式问题。 第一方 .NET 分析器与目标平台无关。 也就是说，你的项目不需要面向特定的 .NET 平台。 分析器适用于面向 `net5.0` 和早期的 .net 版本的项目，例如 `netcoreapp` 、 `netstandard` 和 `net472` 。

可以通过以下一种方式启用或安装第一方 .NET 分析器：

- 从 .NET SDK 中启用：从 Visual Studio 2019 16.8 和 .NET 5.0 开始，这些分析器[包含在 .NET SDK 中](/dotnet/fundamentals/code-analysis/overview)。 分析功能针对面向 .NET 5.0 或更高版本的项目默认启用。 可通过将 MSBUILD [EnableNETAnalyzers](/dotnet/core/project-sdk/msbuild-props#enablenetanalyzers) 属性设置为 `true`，在面向 .NET 早期版本的项目上启用代码分析。 你也可通过将 `EnableNETAnalyzers` 设置为 `false`，对项目禁用代码分析。

- 安装为 NuGet 包：如果不想迁移到 .NET 5+ SDK，或者更喜欢基于 NuGet 包的模型，则 Visual Studio 2019 上的 `Microsoft.CodeAnalysis.NetAnalyzers` [NuGet 包](https://www.nuget.org/packages/Microsoft.CodeAnalysis.NetAnalyzers)中也提供了这些分析器。  对于按需版本更新，你可能更倾向于使用基于包的模型。 如果你在 Visual Studio 2017 上，请改为安装最新 `2.9.x` 版本的 `Microsoft.CodeAnalysis.FxCopAnalyzers` [NuGet 包](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/)。

> [!NOTE]
> 建议从 .NET SDK 启用分析器，而不是安装 `Microsoft.CodeAnalysis.NetAnalyzers` [NuGet 包](https://www.nuget.org/packages/Microsoft.CodeAnalysis.NetAnalyzers)（如果可能）。 从 .NET SDK 启用分析器可以确保在更新 SDK 后，立即自动获取分析器 bug 修复和新分析器。 在 NuGet 模型中，每次需要最新的 bug 修复时都需要更新 NuGet 包。 NuGet 包会更频繁地进行更新。

## <a name="see-also"></a>另请参阅

- [Visual Studio 中的代码分析器概述](roslyn-analyzers-overview.md)
- [在 Visual Studio 中使用代码分析器](use-roslyn-analyzers.md)
- [从旧版分析迁移到 .NET 分析器](migrate-from-legacy-analysis-to-net-analyzers.md)
- [从 FxCop 分析器迁移到 .NET 分析器](migrate-from-fxcop-analyzers-to-net-analyzers.md)

---
title: 支持的 Roslyn 包版本映射
description: 本文介绍不同版本的 (支持哪些 .NET 编译器平台) Roslyn Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 04/29/2019
ms.topic: reference
helpviewer_keywords:
- roslyn package versions
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 213dd6f76cab8dfaf87e498ea5e020386e3d3e8af4a68ee50df704fe4ed2b193
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121447787"
---
# <a name="net-compiler-platform-package-version-reference"></a>.NET 编译器平台包版本参考

下表显示了不同版本的[ (支持 Roslyn](https://www.nuget.org/packages/Microsoft.Net.Compilers/)) 版本的 .NET 编译器平台Visual Studio。

例如，为了确保自定义分析器适用于 Visual Studio 2017 的所有版本，它应面向 Microsoft.Net.Compilers 版本 2.0。

| Roslyn 包版本 | 支持的最低Visual Studio版本 |
| - | - |
| 3.x | Visual Studio 2019 |
| 2.10.0 | Visual Studio 2017 版本 15.9 |
| 2.9.0 | Visual Studio 2017 版本 15.8 |
| 2.8.2 | Visual Studio 2017 15.7 版 |
| 2.7.0 | Visual Studio 2017 版本 15.6 |
| 2.6.1 | Visual Studio 2017 版本 15.5 |
| 2.4.0 | Visual Studio 2017 版本 15.4 |
| 2.3.2 | Visual Studio 2017 版本 15.3 |
| 2.2.0 | Visual Studio 2017 版本 15.2 |
| 2.1.0 | Visual Studio 2017 版本 15.1 |
| 2.0.0 | Visual Studio 2017 RTM |
| 1.3.2 | Visual Studio 2015 更新 3 |
| 1.2.2 | Visual Studio 2015 更新 2 |
| 1.1.1 | Visual Studio 2015 更新 1 |
| 1.0.1 | Visual Studio 2015 RTM |

> [!TIP]
> 对于最低支持的 Visual Studio 版本为 Visual Studio 2017 版本的 Roslyn 包，Visual Studio 2019 的所有版本也受支持，因为它们是更高版本。

## <a name="see-also"></a>另请参阅

- [.NET 编译器平台 SDK](/dotnet/csharp/roslyn-sdk/)
- [Roslyn 分析器入门](getting-started-with-roslyn-analyzers.md)

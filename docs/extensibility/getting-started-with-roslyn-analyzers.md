---
title: 入门 Roslyn 分析器|Microsoft Docs
description: 使用这些资源开始在 Visual Studio 中开始使用 Roslyn 分析器;包括教程和几个示例。
ms.custom: SEO-VS-2020
ms.date: 04/02/2018
ms.topic: conceptual
ms.assetid: 367c2ec8-3059-46a5-9d1c-57bead0419e7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: f61eedca093e0fa9f86eb6e78dccca4aabd21827
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122087127"
---
# <a name="get-started-with-roslyn-analyzers"></a>Roslyn 分析器入门

借助 Visual Studio 中的实时基于项目的代码分析器，API 作者可以将特定于域的代码分析作为其包的一NuGet一部分。 由于这些分析器由 .NET Compiler Platform (代码（名为"Roslyn") ）提供电源，因此，即使在你完成行之前键入，它们也可以生成代码中的警告 (无需再等待生成代码来发现问题) 。 分析器还可通过灯泡提示Visual Studio自动代码修复，让你能够立即清理代码。

## <a name="get-started"></a>入门

[Roslyn 分析器概述](../code-quality/roslyn-analyzers-overview.md)

[教程：编写第一个分析器和代码修补程序](/dotnet/csharp/roslyn-sdk/tutorials/how-to-write-csharp-analyzer-code-fix)

[添加代码修复演练：为用户提供分析器问题的修补程序](/archive/msdn-magazine/2015/february/csharp-adding-a-code-fix-to-your-roslyn-analyzer)

[真实 Roslyn 分析](../extensibility/roslyn-analyzers-and-code-aware-library-for-immutablearrays.md) 器，也可作为对话 [观看](https://channel9.msdn.com/events/Build/2015/3-725)

[有关分析器GitHub示例，分为三种类型的分析器](https://github.com/dotnet/roslyn/blob/master/docs/analyzers/Analyzer%20Samples.md)

## <a name="see-also"></a>请参阅

- [.NET 编译器平台包版本参考](roslyn-version-support.md)
- [有关 OSS 站点GitHub文档](https://github.com/dotnet/roslyn/tree/master/docs/analyzers)
- [使用 Roslyn 分析器实现的 FxCop 规则](../code-quality/fxcop-rule-port-status.md)

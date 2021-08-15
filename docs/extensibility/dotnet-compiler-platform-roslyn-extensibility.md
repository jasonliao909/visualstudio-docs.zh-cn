---
title: .NET Compiler Platform (&quot; Roslyn &quot;) 扩展性|Microsoft Docs
description: 了解.NET Compiler Platform，它允许工具和开发人员共享编译器具有的关于程序丰富的信息。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 564201b3-1e18-4b88-b615-42c2f57f3fe8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: b09aa03ae6af6789ddcc87dc60797af5eda3f19bcde6148dd7bfe1b568b7f0f2
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121388924"
---
# <a name="net-compiler-platform-quotroslynquot-extensibility"></a>.NET Compiler Platform (&quot; Roslyn &quot;) 扩展性
.NET Compiler Platform ("Roslyn") 的核心任务是打开 C# 和 Visual Basic 编译器，并允许工具和开发人员共享编译器具有的丰富程序信息。 代码分析工具可以提高代码质量，代码生成器有助于应用程序构造。 随着工具的智能，它们需要访问越来越多的只有编译器拥有的深入代码知识。 Roslyn 编译器 (中的源代码和对象代码作为不透明的) ，而是提供可用于工具和应用程序中代码相关任务的 API。

 最好的部分是 Roslyn 编译器、其 API、示例和演练，以及基于这些 API 构建的实际工具都是[github.com/dotnet/roslyn。](https://github.com/dotnet/Roslyn) 请转到 OSS 站点了解详情并开始使用 Roslyn。 可找到链接，获取Visual Basic最终用户使用的最新 C# 和 Visual Basic 功能，以及利用 Roslyn API 作为工具构建者入门的链接。

## <a name="see-also"></a>另请参阅
- [Roslyn 分析器入门](../extensibility/getting-started-with-roslyn-analyzers.md)

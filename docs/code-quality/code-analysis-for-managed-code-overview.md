---
title: 托管代码分析
ms.date: 08/27/2020
description: 了解 Visual Studio 中基于 .NET Compiler Platform 的代码分析器。 了解为什么这些分析器可以取代托管程序集的 FxCop 静态分析。
ms.custom: SEO-VS-2020
ms.topic: conceptual
helpviewer_keywords:
- code analysis, managed code
- managed code, code analysis
author: mikadumont
ms.author: midumont
manager: jmartens
ms.technology: vs-ide-code-analysis
ms.workload:
- dotnet
ms.openlocfilehash: 5fbd9e0df806e038e4016a128a4340aa46777470
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601343"
---
# <a name="overview-of-code-analysis-for-net-in-visual-studio"></a>概述：Visual Studio 中的 .NET 代码分析

Visual Studio 可以通过两种方式对托管代码执行代码分析：第一种是[旧版分析](../code-quality/walkthrough-analyzing-managed-code-for-code-defects.md)（即托管程序集的 FxCop 静态分析），第二种是较为新式的[基于 .NET Compiler Platform 的代码分析器](../code-quality/roslyn-analyzers-overview.md)。 基于 .NET Compiler Platform 的代码分析器在键入时实时分析代码，能替代旧版 FxCop 静态代码分析，后者仅分析已编译的代码。

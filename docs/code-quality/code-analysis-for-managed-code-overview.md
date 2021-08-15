---
title: 托管代码分析
ms.date: 08/27/2020
description: 了解 .NET Compiler Platform 中基于 Visual Studio 的代码分析器。 了解为什么这些分析器取代了托管程序集的 FxCop 静态分析。
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
ms.openlocfilehash: 08a90f1d2157088f060fe15a5a370413a55b79e7e04e736f7ac0e5a4c9b76e7b
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121405599"
---
# <a name="overview-of-code-analysis-for-net-in-visual-studio"></a>中 .NET 的代码分析Visual Studio

Visual Studio两种方式对托管代码执行代码分析：使用旧分析，也称为托管[](../code-quality/walkthrough-analyzing-managed-code-for-code-defects.md)程序集的 FxCop 静态分析，以及更新式的基于 .NET Compiler Platform 的代码分析器[。](../code-quality/roslyn-analyzers-overview.md) .NET Compiler Platform代码分析器（在键入时实时分析代码）替换旧版 FxCop 静态代码分析，该分析仅分析已编译的代码。

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
ms.openlocfilehash: 5fbd9e0df806e038e4016a128a4340aa46777470
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122031726"
---
# <a name="overview-of-code-analysis-for-net-in-visual-studio"></a>中 .NET 的代码分析Visual Studio

Visual Studio两种方式执行托管代码的代码分析：使用旧分析（也称为托管程序集[](../code-quality/walkthrough-analyzing-managed-code-for-code-defects.md)的 FxCop 静态分析）和基于 .NET Compiler Platform 的新式代码分析[器。](../code-quality/roslyn-analyzers-overview.md) .NET Compiler Platform代码分析器（在键入时实时分析代码）替换旧版 FxCop 静态代码分析，该分析仅分析已编译的代码。

---
title: 托管代码分析
ms.date: 08/27/2020
description: 了解 Visual Studio 中基于 .NET Compiler Platform 的代码分析器。 了解这些分析器为何替换托管程序集的 FxCop 静态分析。
ms.custom: SEO-VS-2020
ms.topic: conceptual
helpviewer_keywords:
- code analysis, managed code
- managed code, code analysis
author: mikadumont
ms.author: midumont
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: 542747f650888b384a9f9c4910b0d9caea93e948
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99860563"
---
# <a name="overview-of-code-analysis-for-net-in-visual-studio"></a>Visual Studio 中的 .NET 代码分析概述

Visual Studio 可以通过以下两种方式对托管代码执行代码分析：通过 [传统分析](../code-quality/walkthrough-analyzing-managed-code-for-code-defects.md)（也称为 FxCop 静态分析）托管程序集，以及更新式的 [基于 .NET Compiler Platform 的代码分析器](../code-quality/roslyn-analyzers-overview.md)。 基于 .NET Compiler Platform 的代码分析器（在你键入时实时分析你的代码）将替换旧的 FxCop 静态代码分析，后者仅分析已编译的代码。

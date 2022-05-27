---
title: 如何为 .NET 手动运行代码分析
ms.date: 05/13/2022
description: 了解如何在 Visual Studio 2019 16.5 或更高版本中手动运行代码分析。 了解如何在 C# 或 Visual Basic 代码上运行 Roslyn 分析器。
ms.custom: SEO-VS-2020
ms.topic: how-to
helpviewer_keywords:
- code analysis, running
- run code analysis
ms.assetid: 5086d228-f92e-4515-9708-c5b89b9e9a03
author: mikadumont
ms.author: midumont
manager: jmartens
ms.technology: vs-ide-code-analysis
ms.workload:
- dotnet
ms.openlocfilehash: 837f2baa0c3031b3ad9ff9a10146f86c5bc374f5
ms.sourcegitcommit: b86afb55321ec393bd29afffc2574772f36f94bd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/18/2022
ms.locfileid: "145148965"
---
# <a name="run-code-analysis-manually-for-net"></a>为 .NET 手动运行代码分析

[!INCLUDE [Visual Studio](~/includes/applies-to-version/vs-windows-only.md)]

默认情况下，.NET 编译器平台（“Roslyn”）分析器会在键入内容时通过实时分析以及在生成过程中分析 C# 或 Visual Basic 代码。 因此，通常不需要手动触发代码分析。 但是，在某些情况下，可能需要手动触发代码分析：

- 默认情况下，实时代码分析仅在 Visual Studio 2022 年 2022 及更高版本中为活动文档执行分析器。 但是，你可能想要查看特定项目或解决方案中所有文件的代码分析警告。 如果是这样，建议在项目或解决方案上触发一次代码分析。 或者，可以启用连续实时代码分析，以便在整个解决方案上执行。 有关详细信息，请参阅[如何：配置托管代码的实时代码分析范围](./configure-live-code-analysis-scope-managed-code.md)。
- 你可能更喜欢按需使用代码分析执行工作流，而不是使用持续的实时分析或生成时分析。 如果是这样，可以在实时分析和/或生成期间禁用分析器执行。 有关禁用分析的信息，请参阅[如何禁用源代码分析](disable-code-analysis.md)。 然后，可以在项目或解决方案上手动触发代码分析一次。

> [!NOTE]
> 手动运行代码分析需要 Visual Studio 2019 16.5 或更高版本

## <a name="run-code-analysis-manually"></a>手动运行代码分析

1. 在“解决方案资源管理器”中，选择项目。

2. 在“**分析**”菜单上，选择 **“在 [Project 名称]上运行Code Analysis**。

代码分析将在后台开始执行。 应在左下角的Visual Studio状态栏中看到运行 **代码分析\<project>** 的消息。 代码分析完成后，状态消息将更改为“针对 \<project> 的代码分析已完成”。 错误列表将很快刷新所有代码分析诊断。

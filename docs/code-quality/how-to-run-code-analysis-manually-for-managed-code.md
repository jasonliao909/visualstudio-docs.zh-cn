---
title: 如何为 .NET 手动运行代码分析
ms.date: 09/02/2020
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
ms.openlocfilehash: 571845c313a0712a10383a1cb718fea4bc4817f2
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601299"
---
# <a name="run-code-analysis-manually-for-net"></a>为 .NET 手动运行代码分析
默认情况下，.NET 编译器平台（“Roslyn”）分析器会在键入内容时通过实时分析以及在生成过程中分析 C# 或 Visual Basic 代码。 因此，通常不需要手动触发代码分析。 但是，在某些情况下，可能需要手动触发代码分析：

> [!NOTE]
> 手动运行代码分析需要 Visual Studio 2019 16.5 或更高版本

- 默认情况下，实时代码分析仅对 Visual Studio 中打开的文件执行分析器。 但是，你可能想要查看特定项目或解决方案中所有文件的代码分析警告。 如果是这样，建议在项目或解决方案上触发一次代码分析。 也可启用持续的实时代码分析，以对整个解决方案执行分析。 有关详细信息，请参阅[如何：配置托管代码的实时代码分析范围](./configure-live-code-analysis-scope-managed-code.md)。
- 你可能更喜欢按需使用代码分析执行工作流，而不是使用持续的实时分析或生成时分析。 如果是这样，可以在实时分析和/或生成期间禁用分析器执行。 有关禁用分析的信息，请参阅[如何禁用源代码分析](disable-code-analysis.md)。 然后，建议在项目或解决方案上手动触发一次代码分析。

### <a name="run-code-analysis-manually"></a>手动运行代码分析

1. 在“解决方案资源管理器”中，选择项目。

2. 在“分析”菜单上的“项目名称”中选择“运行代码分析” 。

代码分析将在后台开始执行。 应会在 Visual Studio 状态栏中的左下角看到消息“为 \<project> 运行代码分析…”。 代码分析完成后，状态消息将更改为“针对 \<project> 的代码分析已完成”。 错误列表将很快刷新所有代码分析诊断。

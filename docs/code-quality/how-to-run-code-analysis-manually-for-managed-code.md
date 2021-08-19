---
title: 如何手动为 .NET 运行代码分析
ms.date: 09/02/2020
description: 了解如何在 2019 Visual Studio 16.5 或更高版本中手动运行代码分析。 了解如何在 C# 或 Visual Basic 运行 Roslyn 分析器。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122075289"
---
# <a name="run-code-analysis-manually-for-net"></a>为 .NET 手动运行代码分析
默认情况下，.NET Compiler Platform ("Roslyn") 分析器通过执行实时分析以及生成期间Visual Basic键入的 C# 或 Visual Basic 代码。 因此，通常不需要手动触发代码分析。 但是，在某些情况下，可能需要手动触发代码分析：

> [!NOTE]
> 手动运行代码分析Visual Studio 2019 版本 16.5 或更高版本

- 默认情况下，实时代码分析仅对打开的文件执行分析Visual Studio。 但是，你可能有兴趣查看特定项目或解决方案中所有文件的代码分析警告。 如果是这样，则希望对项目或解决方案触发一次代码分析。 或者，可以启用在整个解决方案上执行连续实时代码分析。 有关详细信息，请参阅[如何：配置托管代码的实时代码分析范围](./configure-live-code-analysis-scope-managed-code.md)。
- 你可能更喜欢按需代码分析执行工作流，而不想使用持续实时分析或生成时分析。 如果是这样，可以在实时分析和/或生成期间禁用分析器执行。 有关禁用分析的信息，请参阅 [如何禁用源代码分析](disable-code-analysis.md)。 然后，你想要在项目或解决方案上手动触发一次代码分析。

### <a name="run-code-analysis-manually"></a>手动运行代码分析

1. 在 **解决方案资源管理器** 中，选择项目。

2. 在"**分析"** 菜单上，选择"Code Analysis **名称***Project"。*

代码分析将在后台开始执行。 在左 **下角的 \<project>**"Visual Studio"状态栏中，应会显示"正在运行 ...的代码分析"消息。 代码分析完成后，状态消息将更改为为 **完成的代码分析 \<project>**。 错误列表很快就会刷新，并包含所有代码分析诊断。

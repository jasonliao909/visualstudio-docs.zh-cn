---
title: 托管代码的传统分析
ms.date: 06/12/2019
description: 了解 Visual Studio 中的传统分析。 请参阅如何禁止显示警告以及如何在签入和生成过程中手动、自动和运行分析。
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
ms.openlocfilehash: 6ec5d5a5bc491ef820631af942db8ad5c320fa22
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601258"
---
# <a name="overview-of-legacy-analysis-for-managed-code-in-visual-studio"></a>Visual Studio 中的托管代码的传统分析概述

Visual Studio 可以通过两种方式对托管代码执行代码分析：通过[传统分析](../code-quality/walkthrough-analyzing-managed-code-for-code-defects.md)（也称为 FxCop 静态分析）托管程序集，以及更新式的基于 .NET Compiler Platform 的[代码分析器](../code-quality/roslyn-analyzers-overview.md)。 本主题介绍了旧式分析。 若要详细了解基于 .NET Compiler Platform 的代码分析，请参阅[基于 .NET Compiler Platform 的分析器概述](../code-quality/roslyn-analyzers-overview.md)。

托管代码的代码分析分析托管程序集，并报告有关程序集的信息，如 [.Net 设计准则](/dotnet/standard/design-guidelines/)中规定的编程和设计规则的冲突。

分析工具将它在分析期间执行的检查表示为警告消息。 警告消息标识任何相关的编程和设计问题，如有可能，还提供有关如何修复问题的信息。

> [!NOTE]
> 旧分析 (Visual Studio 中的 .NET Core 和 .NET Standard 项目不支持静态代码分析) 。 如果在作为 msbuild 的一部分的 .NET Core 或 .NET Standard 项目上运行代码分析，则会看到类似于错误的错误 **： CA0055：无法识别的 \<your.dll> 平台**。 若要分析 .NET Core 或 .NET Standard 项目中的代码，请改用 [代码分析器](../code-quality/roslyn-analyzers-overview.md) 。

## <a name="ide-integrated-development-environment-integration"></a>IDE (集成开发环境) 集成

可以手动或自动对项目运行代码分析。

若要在每次生成项目时运行代码分析，请在项目的 " **Code Analysis** " 属性页上选择相应的选项。 有关详细信息，请参阅[如何：启用和禁用自动 Code Analysis](../code-quality/how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)。

若要在项目上手动运行代码分析，请从菜单栏中选择 "**分析**  >  **运行 Code Analysis**  >  **在上 \<project> 运行 Code Analysis**。

## <a name="rule-sets"></a>规则集

托管代码的代码分析规则划分到规则集中[](../code-quality/using-rule-sets-to-group-code-analysis-rules.md)。 您可以使用其中一个 Microsoft 标准规则集，也可以 [创建自定义规则集](../code-quality/how-to-create-a-custom-rule-set.md) 来满足特定需求。

## <a name="suppress-warnings"></a>禁止显示警告

它通常用于指示警告不适用。 这样，便可以通知开发人员以及可能会在以后评审代码的其他人员：已调查了一个警告，且禁止显示或忽略了该警告。

通过自定义特性实现的源代码中禁止显示警告。 若要禁止显示警告，请向源代码添加特性 `SuppressMessage`，如下面的示例所示：

```csharp
[System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Design", "CA1039:ListsAreStrongTyped")]
Public class MyClass
{
   // code
}
```

有关详细信息，请参阅[取消警告](../code-quality/in-source-suppression-overview.md)。

::: moniker range="vs-2017"

> [!NOTE]
> 如果将项目迁移到 Visual Studio 2017，可能会突然遇到大量代码分析警告。 如果尚未准备好修复警告，则可以通过选择 "**分析**  >  **运行 Code Analysis 并取消显示活动问题** 来禁止显示这些警告。
>
> ![运行代码分析并取消 Visual Studio 中的问题](media/suppress-active-issues.png)

::: moniker-end

::: moniker range=">=vs-2019"

> [!NOTE]
> 如果将项目迁移到 Visual Studio 2019，可能会突然遇到大量代码分析警告。 如果尚未准备好修复警告，可以通过选择 "**分析**  >  **生成并取消活动问题**" 来取消所有这些警告。

::: moniker-end

## <a name="run-code-analysis-as-part-of-check-in-policy"></a>作为签入策略的一部分运行代码分析

作为一个单位，可能希望所有签入行为满足特定的策略。 特别是希望确保遵从下列策略：

- 要签入的代码中没有生成错误。

- 代码分析作为最新生成的一部分运行。

可以通过指定签入策略来实现该任务。 有关详细信息，请参阅[利用 Project 签入策略提高代码质量](../code-quality/how-to-create-or-update-standard-code-analysis-check-in-policies.md)。

## <a name="team-build-integration"></a>Team build 集成

你可以使用生成系统的集成功能在生成过程中运行分析工具。 有关详细信息，请参阅 [Azure Pipelines](/azure/devops/pipelines/index?view=vsts&preserve-view=true)。

## <a name="see-also"></a>另请参阅

- [基于 .NET Compiler Platform 的分析器概述](../code-quality/roslyn-analyzers-overview.md)
- [使用规则集对代码分析规则进行分组](../code-quality/using-rule-sets-to-group-code-analysis-rules.md)
- [如何：启用和禁用自动代码分析](../code-quality/how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)

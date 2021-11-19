---
title: 创建/更新标准代码分析签入策略
description: 了解如何确保代码分析在 Azure DevOps 项目中的所有代码项目上运行。 了解如何配置项目代码分析签入策略。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.codeanalysis.policyeditor
helpviewer_keywords:
- code analysis, migrating check-in policy
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-code-analysis
ms.workload:
- multiple
ms.openlocfilehash: 70442184ae7a8ce36657ce9c2dbc8887f9d3b9e7
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601305"
---
# <a name="how-to-create-or-update-standard-code-analysis-check-in-policies"></a>如何：创建或更新标准代码分析签入策略

可使用代码分析签入策略，要求在 Azure DevOps 项目中的所有代码项目上运行代码分析。 要求代码分析可以提高签入到代码库的代码的质量。

> [!NOTE]
> 此功能仅在使用 Team Foundation Server 时可用。

代码分析签入策略在项目设置中设置，并应用于每个代码项目。 代码分析运行在代码项目的项目 (.xxproj) 文件中是为代码项目配置的。 代码分析运行在本地计算机上执行。 启用代码分析签入策略时，必须在最后一次编辑后编译要签入的代码项目中的文件，并且至少包含项目设置中的规则的代码分析运行必须在已更改的计算机上执行。

- 对于托管代码，通过指定包含代码分析规则子集的规则集来设置签入策略。

- 对于 C/C++ 代码，在 Visual Studio 2017 版本 15.6 及更早的版本中，签入策略要求运行所有代码分析规则。 可以添加预处理器指令，以禁用 Azure DevOps 项目中各个代码项目的特定规则。 在 15.7 及更高版本中，可以使用 /analyze:ruleset 来指定要运行的规则。 有关详细信息，请参阅[使用规则集指定要运行的 C++ 规则](/cpp/code-quality/using-rule-sets-to-specify-the-cpp-rules-to-run)。

在为托管代码指定签入策略后，团队成员可以将其代码项目的代码分析设置同步到 Azure DevOps 项目策略设置。

## <a name="to-open-the-check-in-policy-editor"></a>打开签入策略编辑器

1. 在“团队资源管理器”中，右键单击项目名称，指向“项目设置”，然后单击“源代码管理” 。

1. 在“源代码管理”对话框中，选择“签入策略”选项卡 。

1. 执行下列操作之一：

    - 单击“添加”创建新的签入策略。

    - 双击“策略类型”列表中的现有“代码分析”项以更改策略 。

## <a name="to-set-policy-options"></a>设置策略选项

选择或清除以下选项：

|选项|说明|
|------------|-----------------|
|**执行签入以只包含属于当前解决方案的文件。**|代码分析只能在解决方案和项目配置文件中指定的文件上运行。 此策略保证分析属于解决方案一部分的所有代码。|
|**执行 C/C++ 代码分析 (/analyze)**|要求使用 /analyze 编译器选项生成所有 C 或 C++ 项目以运行代码分析，然后才能进行签入。|
|**对托管代码执行代码分析**|要求所有托管项目运行代码分析和生成，然后才能签入它们。|

## <a name="to-specify-a-managed-rule-set"></a>指定托管规则集

在“运行此规则集”列表中，使用以下方法之一：

- 选择 Microsoft 标准规则集。

- 通过单击 \<Select Rule Set from Source Control...> 选择自定义规则集。 然后，在源代码管理浏览器中键入规则集的版本控制路径。 版本控制路径的语法为：

   **$/** `TeamProjectName` **/** `VersionControlPath`

有关如何创建和实现自定义签入策略规则集的详细信息，请参阅[对托管代码实施自定义签入策略](../code-quality/implementing-custom-code-analysis-check-in-policies-for-managed-code.md)。

## <a name="see-also"></a>另请参阅

- [实现托管代码的自定义代码分析签入策略](../code-quality/implementing-custom-code-analysis-check-in-policies-for-managed-code.md)

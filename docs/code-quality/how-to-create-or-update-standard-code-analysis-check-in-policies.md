---
title: 创建/更新标准代码分析签入策略
description: 了解如何确保代码分析在项目的所有代码Azure DevOps运行。 了解如何配置项目代码分析签入策略。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122031674"
---
# <a name="how-to-create-or-update-standard-code-analysis-check-in-policies"></a>如何：创建或更新标准代码分析签入策略

可以使用代码分析签入策略，要求对 Azure DevOps 项目的所有代码项目运行代码分析。 要求代码分析可以提高签入到代码库的代码的质量。

> [!NOTE]
> 此功能仅在使用 Team Foundation Server。

代码分析签入策略在项目设置中设置，并应用于每个代码项目。 代码分析运行为项目代码项目中的代码项目配置 (.xxproj) 代码项目的文件。 代码分析运行在本地计算机上执行。 启用代码分析签入策略时，必须在上次编辑后编译要签入的代码项目中的文件，并且运行至少包含项目设置中规则的代码分析运行必须在进行了更改的计算机上执行。

- 对于托管代码，通过指定包含代码分析规则子集的规则集来设置签入策略。

- 对于 C/C++ 代码，在 Visual Studio 2017 版本 15.6 及更早版本中，签入策略要求运行所有代码分析规则。 可以添加预处理器指令，以禁用单个代码项目中各个代码Azure DevOps规则。 在 15.7 及更高版本中，可以使用 **/analyze：ruleset** 指定要运行的规则。 有关详细信息，请参阅 [使用规则集指定要运行的 C++ 规则](/cpp/code-quality/using-rule-sets-to-specify-the-cpp-rules-to-run)。

为托管代码指定签入策略后，团队成员可以将代码项目的代码分析设置同步到Azure DevOps策略设置。

## <a name="to-open-the-check-in-policy-editor"></a>打开签入策略编辑器

1. 在团队资源管理器，右键单击项目名称，指向Project 设置，然后单击"**源代码****管理"。**

1. 在" **源代码管理"** 对话框中，选择" **签入策略"** 选项卡。

1. 执行下列操作之一：

    - 单击 **"** 添加"以创建新的签入策略。

    - 双击"策略类型 **Code Analysis** 中的现有策略 **项** 以更改策略。

## <a name="to-set-policy-options"></a>设置策略选项

选择或清除以下选项：

|选项|说明|
|------------|-----------------|
|**强制签入以仅包含属于当前解决方案的文件。**|代码分析只能对解决方案和项目配置文件中指定的文件运行。 此策略保证分析属于解决方案一部分的所有代码。|
|**强制执行 C/C++ Code Analysis (/analyze)**|要求使用 /analyze 编译器选项生成所有 C 或 C++ 项目，以运行代码分析，然后才能签入它们。|
|**强制执行Code Analysis代码的强制要求**|要求所有托管项目运行代码分析和生成，然后才能签入它们。|

## <a name="to-specify-a-managed-rule-set"></a>指定托管规则集

在" **运行此规则集** "列表中，使用以下方法之一：

- 选择 Microsoft 标准规则集。

- 通过单击 选择自定义规则集 **\<Select Rule Set from Source Control...>** 。 然后，在源代码管理浏览器中键入规则集的版本控制路径。 版本控制路径的语法为：

   **$/** `TeamProjectName` **/** `VersionControlPath`

若要详细了解如何创建和实现自定义签入策略规则集，请参阅为托管代码实现自定义 [签入策略](../code-quality/implementing-custom-code-analysis-check-in-policies-for-managed-code.md)。

## <a name="see-also"></a>请参阅

- [实现托管代码的自定义代码分析签入策略](../code-quality/implementing-custom-code-analysis-check-in-policies-for-managed-code.md)

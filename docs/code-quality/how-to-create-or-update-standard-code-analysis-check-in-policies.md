---
title: 创建/更新标准代码分析签入策略
description: 了解如何确保在 Azure DevOps 项目的所有代码项目中运行代码分析。 请参阅如何配置项目代码分析签入策略。
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
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601305"
---
# <a name="how-to-create-or-update-standard-code-analysis-check-in-policies"></a>如何：创建或更新标准代码分析签入策略

您可以通过使用代码分析签入策略，要求在 Azure DevOps 项目的所有代码项目中运行代码分析。 需要代码分析可以提高签入到代码库中的代码的质量。

> [!NOTE]
> 仅当使用 Team Foundation Server 时，此功能才可用。

代码分析签入策略是在项目设置中设置的，适用于每个代码项目。 为代码项目 ( 的项目中的代码项目配置代码分析运行。 .xxproj) 文件中的代码项目。 代码分析运行在本地计算机上执行。 启用代码分析签入策略时，必须在其上一次编辑后编译代码项目中要签入的文件，并且至少必须在已进行更改的计算机上执行项目设置中的规则时才执行此代码分析。

- 对于托管代码，你可以通过指定包含部分代码分析规则的 *规则集* 来设置签入策略。

- 对于 C/c + + 代码，在 Visual Studio 2017 版本15.6 及更早版本中，签入策略要求运行所有代码分析规则。 可以添加预处理器指令来禁用 Azure DevOps 项目中各个代码项目的特定规则。 在15.7 和更高版本中，可以使用 **/analyze：规则集** 来指定要运行的规则。 有关详细信息，请参阅 [使用规则集指定要运行的 c + + 规则](/cpp/code-quality/using-rule-sets-to-specify-the-cpp-rules-to-run)。

为托管代码指定签入策略后，团队成员可以将代码项目的代码分析设置同步到 Azure DevOps 项目策略设置。

## <a name="to-open-the-check-in-policy-editor"></a>打开签入策略编辑器

1. 在团队资源管理器中，右键单击项目名称，指向 " **Project 设置**"，然后单击 "**源代码管理**"。

1. 在 " **源代码管理** " 对话框中，选择 " **签入策略** " 选项卡。

1. 执行下列操作之一：

    - 单击 " **添加** " 以创建新的签入策略。

    - 双击 "**策略类型**" 列表中的现有 **Code Analysis** 项以更改策略。

## <a name="to-set-policy-options"></a>设置策略选项

选择或清除以下选项：

|选项|说明|
|------------|-----------------|
|**强制签入只包含属于当前解决方案的文件。**|代码分析只能对在解决方案和项目配置文件中指定的文件运行。 此策略可保证分析作为解决方案一部分的所有代码。|
|**强制执行 c/c + + Code Analysis (/analyze)**|要求所有 C 或 c + + 项目都用 "/analyze 编译器" 选项生成，以便在签入之前运行代码分析。|
|**强制实施托管代码 Code Analysis**|要求所有托管项目运行代码分析和生成，然后才能将其签入。|

## <a name="to-specify-a-managed-rule-set"></a>指定托管规则集

从 " **运行此规则集** " 列表中，使用以下方法之一：

- 选择 Microsoft 标准规则集。

- 通过单击选择自定义规则集 **\<Select Rule Set from Source Control...>** 。 然后，在源代码管理器浏览器中键入规则集的版本控制路径。 版本控制路径的语法为：

   **$/** `TeamProjectName` **/** `VersionControlPath`

有关如何创建和实现自定义签入策略规则集的详细信息，请参阅 [为托管代码实现自定义签入策略](../code-quality/implementing-custom-code-analysis-check-in-policies-for-managed-code.md)。

## <a name="see-also"></a>另请参阅

- [实现托管代码的自定义代码分析签入策略](../code-quality/implementing-custom-code-analysis-check-in-policies-for-managed-code.md)

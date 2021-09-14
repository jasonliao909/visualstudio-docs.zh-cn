---
title: 使用签入策略同步项目规则集
ms.date: 11/04/2016
description: 了解如何将Visual Studio代码项目规则集与Azure DevOps签入策略同步。
ms.custom: SEO-VS-2020
ms.topic: how-to
f1_keywords:
- vs.codeanalysis.selecttfsruleset
ms.assetid: 9b02f934-2db6-41ec-aaff-9c31ceec2f04
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-code-analysis
ms.workload:
- multiple
ms.openlocfilehash: 20c4d0c6fc5583686648507be2a36c5183ca70c6
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601289"
---
# <a name="how-to-synchronize-code-project-rule-sets-with-an-azure-devops-project-check-in-policy"></a>如何：将代码Project规则集与Azure DevOps Project签入策略同步

通过指定至少包含签入策略的规则集内指定的规则集，将代码项目的代码分析设置同步到 Azure DevOps 项目的签入策略。 开发人员主管可以告知你签入策略的规则集的名称和位置。 可以使用以下选项之一来确保项目的代码分析使用正确的规则集：

- 如果签入策略使用 Microsoft 内置规则集之一，请打开代码项目的属性对话框，显示Code Analysis页，然后选择规则集。 Microsoft 标准规则集随 Visual Studio设置为只读，不应编辑。 如果未编辑规则集，则保证策略和本地规则集中的规则匹配。

- 如果签入策略使用自定义规则集，请在版本控制中对规则集文件执行 get 操作，以创建本地副本。 然后在代码项目的代码分析设置中指定该本地位置。 如果签入策略的规则集是最新的，则保证规则匹配。

     如果将版本控制位置映射到与代码项目相同的 Azure DevOps 项目根目录的本地文件夹，则使用相对路径设置规则的位置。 相对路径可确保代码分析的代码项目设置可以移动到其他计算机。

- 为代码项目的签入策略自定义规则集的副本。 请确保新规则集包含签入策略中的所有规则和要包含的其他任何规则。 必须确保规则集包含签入策略的规则集内的所有规则。

## <a name="to-specify-a-microsoft-standard-rule-set"></a>指定 Microsoft 标准规则集

1. 在 **解决方案资源管理器** 中，右键单击代码项目，然后单击"属性 **"。**

2. 单击“代码分析”。

::: moniker range="vs-2017"

3. 在" **运行此规则集** "列表中，选择签入策略规则集。

::: moniker-end

::: moniker range=">=vs-2019"

3. 在" **活动规则"** 列表中，选择签入策略规则集。

::: moniker-end

## <a name="to-specify-a-custom-check-in-policy-rule-set"></a>指定自定义签入策略规则集

1. 如有必要，请对指定签入策略的规则集文件执行 get 操作。

2. 在 **解决方案资源管理器** 中，右键单击代码项目，然后单击"属性 **"。**

3. 单击“代码分析”。

::: moniker range="vs-2017"

4. 在" **运行此规则集"列表中** ，单击 **\<Browse>** 。

::: moniker-end

::: moniker range=">=vs-2019"

4. 在" **活动规则"列表中** ，单击 **\<Browse>** 。

::: moniker-end

5. 在" **打开** "对话框中，指定签入策略规则集文件。

## <a name="to-create-a-custom-rule-set-for-a-code-project"></a>为代码项目创建自定义规则集

有关创建自定义规则集的信息，请参阅 [自定义规则集](how-to-create-a-custom-rule-set.md)。

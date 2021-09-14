---
title: 配置Code Analysis
ms.date: 04/04/2018
description: 了解如何配置旧代码分析Visual Studio规则集。 了解如何将规则集应用于解决方案中的一个或多个项目。
ms.custom: SEO-VS-2020
ms.topic: how-to
f1_keywords:
- vs.codeanalysis.propertypages.csvb
- vs.codeanalysis.propertypages.solution
- vs.codeanalysis.propertypages.asp
dev_langs:
- CSharp
- VB
- FSharp
helpviewer_keywords:
- code analysis, selecting rule sets
- code analysis, rule sets
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-code-analysis
ms.workload:
- dotnet
ms.openlocfilehash: 645441b8961ca84534bd9f4a503189ceb2cb5ab3
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601310"
---
# <a name="how-to-configure-legacy-analysis-for-managed-code"></a>如何：为托管代码配置旧分析

在Visual Studio中，可以从要应用于托管代码项目的代码分析规则集[](../code-quality/rule-set-reference.md)列表进行选择。 默认情况下， **已选择"Microsoft 建议的最低** 规则"规则集，但如果需要，可以应用其他规则集。 规则集可以应用于解决方案中的一个或多个项目。

> [!NOTE]
> 本文适用于旧版分析，.NET Compiler Platform[分析器 。](use-roslyn-analyzers.md)

## <a name="configure-a-rule-set-for-a-net-framework-project"></a>为项目配置.NET Framework集

1. 打开Code Analysis **属性** 页上的"属性"选项卡。 可以通过下列任一方法完成此操作：

   - 在 **解决方案资源管理器** 中，选择项目。 在菜单栏上，选择 **"分析**  >  **配置Code Analysis**  >  **For"。 \<projectname>**

   - 右键单击"属性"中的 **解决方案资源管理器** 并选择"属性 **"，然后选择****"Code Analysis选项卡**。

2. 在" **配置** 和 **平台"** 列表中，选择生成配置和目标平台。

::: moniker range="vs-2017"

3. 若要每次使用所选配置生成项目时运行代码分析，请选择"生成时 **启用Code Analysis代码分析**" 。 也可通过在 上选择"分析运行"Code Analysis  >    >  **运行Code Analysis代码分析 \<projectname>**。

::: moniker-end

::: moniker range=">=vs-2019"

3. 若要每次使用所选配置生成项目时运行代码分析，请在"二进制分析器"部分选择" **生成** 时 **运行** "。 还可以手动运行旧代码分析，有关详细信息，请参阅[如何：手动Code Analysis旧版](how-to-run-legacy-code-analysis-manually-for-managed-code.md)代码。

::: moniker-end

4. 若要查看生成的代码中的警告，请清除" **禁止显示生成的代码的结果** "复选框。

    > [!NOTE]
    > 当生成的代码所产生的代码分析错误和警告出现在窗体和模板中时，此选项不会取消显示它们。 可以查看和维护窗体或模板的源代码，并且不会覆盖它。

::: moniker range="vs-2017"

5. 在" **运行此规则集** "列表中，执行以下操作之一：

::: moniker-end

::: moniker range=">=vs-2019"

5. 在 **"活动规则"** 列表中，执行以下操作之一：

::: moniker-end

   - 选择想要使用的规则集。

   - 选择此选项 **\<Browse>** 可查找不在列表中的现有自定义规则集。

   - 定义自定义 [规则集](../code-quality/how-to-create-a-custom-rule-set.md)。

## <a name="specify-rule-sets-for-multiple-projects-in-a-solution"></a>为解决方案中的多个项目指定规则集

默认情况下，解决方案的所有托管项目都分配有 Microsoft 最低建议 *规则* 代码分析规则集。 可以在解决方案的"属性"对话框中更改分配给解决方案项目的规则集。 

1. 在 Visual Studio 中打开解决方案。

2. 在"**分析"** 菜单上，选择 **"Code Analysis解决方案"。**

3. 如有必要，展开"**通用属性"，** 然后选择 **"Code Analysis 设置"。**

4. 你可以为一个或多个项目指定规则集：

    - 若要为单个项目指定规则集，请选择项目名称。

    - 若要为多个项目指定规则集，请选择 **Ctrl** 和项目名称。

    - 若要指定解决方案中的所有项目，请选择 **"Shift"** 和项目列表。

5. 选择 **项目的"** 规则集"字段，然后选择要应用的规则集的名称。

## <a name="see-also"></a>另请参阅

- [代码分析规则集参考](../code-quality/rule-set-reference.md)

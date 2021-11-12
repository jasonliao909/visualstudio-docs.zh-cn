---
title: 配置代码分析
ms.date: 04/04/2018
description: 了解如何配置 Visual Studio 旧式代码分析所使用的规则集。 了解如何将规则集应用于解决方案中的一个或多个项目。
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
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601310"
---
# <a name="how-to-configure-legacy-analysis-for-managed-code"></a>如何：为托管代码配置旧式分析

在 Visual Studio 中，可以从代码分析[规则集](../code-quality/rule-set-reference.md)列表中选择要应用于托管代码项目的规则集。 默认选择“Microsoft 最小推荐规则”规则集，但你可以根据需要应用不同的规则集。 可以将规则集应用于解决方案中的一个或多个项目。

> [!NOTE]
> 本文适用于旧式分析，不适用于[基于 .NET Compiler Platform 的代码分析器](use-roslyn-analyzers.md)。

## <a name="configure-a-rule-set-for-a-net-framework-project"></a>为 .NET Framework 项目配置规则集

1. 打开项目属性页上的“代码分析”选项卡。 可以通过下列任一方法完成此操作：

   - 在“解决方案资源管理器”中，选择该项目。 在菜单栏上，选择“分析” > “配置代码分析” > “适用对象”\<projectname>  。

   - 在解决方案资源管理器中右键单击项目并选择“属性”，然后选择“代码分析”选项卡  。

2. 在“配置”和“平台”列表中，选择生成配置和目标平台 。

::: moniker range="vs-2017"

3. 若要在每次使用选定配置生成项目时运行代码分析，请选择“在生成时启用代码分析”。 你还可以通过选择“分析” > “运行代码分析” > “在 \<projectname> 上运行代码分析”来手动运行代码分析  。

::: moniker-end

::: moniker range=">=vs-2019"

3. 若要在每次使用选定配置生成项目时运行代码分析，请在“二进制分析器”部分中选择“在生成时运行” 。 你还可以手动运行旧式代码分析，有关详细信息，请参阅[如何：为托管代码手动运行旧式代码分析](how-to-run-legacy-code-analysis-manually-for-managed-code.md)。

::: moniker-end

4. 若要查看生成的代码所产生的警告，请清除“取消显示由生成代码产生的结果”复选框。

    > [!NOTE]
    > 当生成的代码所产生的代码分析错误和警告出现在窗体和模板中时，此选项不会取消显示它们。 可以查看和维护窗体或模板的源代码，并且该源代码不会被覆盖。

::: moniker range="vs-2017"

5. 在“运行此规则集”列表中，执行以下操作之一：

::: moniker-end

::: moniker range=">=vs-2019"

5. 在“主动规则”列表中，执行以下操作之一：

::: moniker-end

   - 选择要使用的规则集。

   - 选择 \<Browse>查找不属于列表的现有自定义规则集。

   - 定义[自定义规则集](../code-quality/how-to-create-a-custom-rule-set.md)。

## <a name="specify-rule-sets-for-multiple-projects-in-a-solution"></a>为解决方案中的多个项目指定规则集

默认情况下，解决方案的所有托管项目都分配有 Microsoft 最小推荐规则代码分析规则集。 可以在解决方案的“属性”对话框中更改分配给解决方案项目的规则集。

1. 在 Visual Studio 中打开解决方案。

2. 在“分析”菜单中，选择“为解决方案配置代码分析” 。

3. 如有需要，展开“公共属性”，然后选择“代码分析设置” 。

4. 可以为一个或多个项目指定规则集：

    - 若要为单个项目指定规则集，请选择项目名称。

    - 若要为多个项目指定规则集，请选择 Ctrl 和项目名称。

    - 若要指定解决方案中的所有项目，请选择 Shift 和项目列表。

5. 选择项目的规则集字段，然后选择要应用的规则集的名称。

## <a name="see-also"></a>另请参阅

- [代码分析规则集参考](../code-quality/rule-set-reference.md)

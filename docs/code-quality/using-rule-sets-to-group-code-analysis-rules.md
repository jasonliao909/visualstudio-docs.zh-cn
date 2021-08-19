---
title: 代码分析规则集
ms.date: 07/23/2021
description: 了解 Visual Studio 代码分析中的内置和自定义规则集。 请参阅如何在文件中指定规则集和如何配置项目中的规则集。
ms.custom: SEO-VS-2020
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.rulesets.learnmore
helpviewer_keywords:
- code analysis, rule sets
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-code-analysis
ms.workload:
- multiple
ms.openlocfilehash: 856fd236959b8335ded1ff2007bc5a5d1dd29a90
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122122067"
---
# <a name="use-rule-sets-to-group-code-analysis-rules"></a>使用规则集对代码分析规则进行分组

在 Visual Studio 中配置代码分析时，可以从内置 *规则集* 列表中进行选择。 规则集是一组代码分析规则，用于标识目标问题和该项目的特定条件。 例如，你可以应用一个规则集，设计用于扫描代码以实现公开可用的 Api。 还可以应用包含所有可用规则的规则集。

你可以通过添加或删除规则或将规则严重性更改为在 **错误列表** 中显示为警告或错误来自定义规则集。 自定义规则集可以满足特定开发环境的需求。 自定义规则集时，规则集编辑器会提供搜索和筛选工具，以帮助您在此过程中使用。

规则集可用于 [托管代码分析](/dotnet/fundamentals/code-analysis/code-quality-rule-options)、 [托管代码的传统分析](how-to-configure-code-analysis-for-a-managed-code-project.md)和 [c + + 代码分析](/cpp/code-quality/using-rule-sets-to-specify-the-cpp-rules-to-run)。

>[!NOTE]
> 从 Visual Studio 2019 版16.3 开始，你可以使用 EditorConfig 文件来配置 .net 源代码分析的规则，但不能配置旧的分析。 有关详细信息，请参阅常见问题解答中的 [EditorConfig 与规则集](../code-quality/analyzers-faq.yml) 部分。

## <a name="rule-set-format"></a>规则集格式

规则集是以 XML 格式 *指定的规则集文件。* 由 ID 和 *操作* 组成的规则按文件中的分析器 ID 和命名空间分组。

*规则集* 文件的内容类似于以下 XML：

```xml
<RuleSet Name="Rules for Hello World project" Description="These rules focus on critical issues for the Hello World app." ToolsVersion="10.0">
  <Localization ResourceAssembly="Microsoft.VisualStudio.CodeAnalysis.RuleSets.Strings.dll" ResourceBaseName="Microsoft.VisualStudio.CodeAnalysis.RuleSets.Strings.Localized">
    <Name Resource="HelloWorldRules_Name" />
    <Description Resource="HelloWorldRules_Description" />
  </Localization>
  <Rules AnalyzerId="Microsoft.Analyzers.ManagedCodeAnalysis" RuleNamespace="Microsoft.Rules.Managed">
    <Rule Id="CA1001" Action="Warning" />
    <Rule Id="CA1009" Action="Warning" />
    <Rule Id="CA1016" Action="Warning" />
    <Rule Id="CA1033" Action="Warning" />
  </Rules>
  <Rules AnalyzerId="Microsoft.CodeQuality.Analyzers" RuleNamespace="Microsoft.CodeQuality.Analyzers">
    <Rule Id="CA1802" Action="Error" />
    <Rule Id="CA1814" Action="Info" />
    <Rule Id="CA1823" Action="None" />
    <Rule Id="CA2217" Action="Warning" />
  </Rules>
</RuleSet>
```

> [!TIP]
> 在图形 **规则集编辑器** 中 [编辑规则集](../code-quality/working-in-the-code-analysis-rule-set-editor.md)比使用手动更容易。

## <a name="specify-a-rule-set-for-a-project"></a>为项目指定规则集

项目的规则集由 Visual Studio 项目文件中的 **CodeAnalysisRuleSet** 属性指定。 例如：

```xml
<PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|AnyCPU' ">
  ...
  <CodeAnalysisRuleSet>HelloWorld.ruleset</CodeAnalysisRuleSet>
</PropertyGroup>
```

## <a name="see-also"></a>请参阅

- [代码分析规则集参考](../code-quality/rule-set-reference.md)
---
title: 代码分析规则集
ms.date: 07/23/2021
description: 了解代码分析中的内置和自定义Visual Studio规则集。 请参阅如何在文件中指定规则集以及如何在项目中配置规则集。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601254"
---
# <a name="use-rule-sets-to-group-code-analysis-rules"></a>使用规则集对代码分析规则进行分组

在 Visual Studio 中配置代码分析时，可以从内置规则集 *的列表进行选择*。 规则集是一组代码分析规则，用于标识该项目的目标问题和特定条件。 例如，可以应用一个旨在扫描代码以寻找公开可用的 API 的规则集。 还可以应用包含所有可用规则的规则集。

可以通过添加或删除规则或更改规则严重性以在错误列表中显示为警告或错误来 **自定义规则集**。 自定义规则集可以满足特定开发环境需求。 自定义规则集时，规则集编辑器会提供搜索和筛选工具来帮助你完成该过程。

规则集可用于托管[代码分析、](/dotnet/fundamentals/code-analysis/code-quality-rule-options)[托管代码的旧式](how-to-configure-code-analysis-for-a-managed-code-project.md)分析和[C++ 代码分析](/cpp/code-quality/using-rule-sets-to-specify-the-cpp-rules-to-run)。

>[!NOTE]
> 从 Visual Studio 2019 版本 16.3 开始，可以使用 EditorConfig 文件为 .NET 源代码分析配置规则，但不能配置旧分析。 有关详细信息，请参阅 [常见问题解答中的 EditorConfig 与规则](../code-quality/analyzers-faq.yml) 集部分。

## <a name="rule-set-format"></a>规则集格式

规则集在 *.ruleset* 文件中以 XML 格式指定。 规则由 ID 和操作 *组成*，在文件中按分析器 ID 和命名空间进行分组。

*.ruleset* 文件的内容类似于以下 XML：

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
> 在图形规则 [集编辑器中](../code-quality/working-in-the-code-analysis-rule-set-editor.md) 编辑规则集 **比手动编辑** 规则集更容易。

## <a name="specify-a-rule-set-for-a-project"></a>为项目指定规则集

项目的规则集由项目文件中 **CodeAnalysisRuleSet** Visual Studio指定。 例如：

```xml
<PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|AnyCPU' ">
  ...
  <CodeAnalysisRuleSet>HelloWorld.ruleset</CodeAnalysisRuleSet>
</PropertyGroup>
```

## <a name="see-also"></a>另请参阅

- [代码分析规则集参考](../code-quality/rule-set-reference.md)
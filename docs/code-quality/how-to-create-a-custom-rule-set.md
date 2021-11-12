---
title: 创建自定义代码分析规则集
ms.date: 11/02/2018
description: 了解如何在 Visual Studio 中自定义代码分析规则集。 了解如何从头开始或从现有集创建新集。 了解规则优先级。
ms.custom: SEO-VS-2020
ms.topic: how-to
f1_keywords:
- vs.codeanalysis.addremoverulesets
helpviewer_keywords:
- rule sets
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-code-analysis
ms.workload:
- multiple
ms.openlocfilehash: 181f94ccc9b83053673e49746d757708afdbf966
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601308"
---
# <a name="customize-a-rule-set"></a>自定义规则集

可创建自定义规则集来满足代码分析的特定项目需求。

## <a name="create-a-custom-rule-set-from-an-existing-rule-set"></a>根据现有规则集创建自定义规则集

若要创建自定义规则集，可在规则集编辑器中打开内置规则集。 可在这里添加或删除特定规则，并还可更改违反规则时发生的操作 &mdash; 例如显示警告或错误。

1. 在解决方案资源管理器中，右键单击项目，然后选择“属性” 。

2. 在“属性”页中，请选择“代码分析”选项卡 。

::: moniker range="vs-2017"

3. 在“运行此规则集”下拉列表中，请执行以下操作之一：

::: moniker-end

::: moniker range=">=vs-2019"

3. 在“活动规则”下拉列表中，请执行以下操作之一：

::: moniker-end

   - 选择要自定义的规则集。

     \- 或 -

   - 选择“\<Browse>”，指定列表外部的现有规则集。

4. 选择“打开”，在规则集编辑器中显示规则。

> [!NOTE]
> 如果你有 .NET Core 或 .NET Standard 项目，则过程会有所不同，因为项目属性中的“代码分析”选项卡不支持这些选项。 按照步骤[将预定义规则集复制到项目，并将其设置为活动规则集](/dotnet/fundamentals/code-analysis/code-quality-rule-options)。 复制规则集后，可从解决方案资源管理器中打开它，[在 Visual Studio 规则集编辑器中进行编辑](working-in-the-code-analysis-rule-set-editor.md)。

## <a name="create-a-new-rule-set"></a>创建新的规则集

可从“新建文件”对话框创建新的规则集文件：

1. 选择“文件” > “新建” > “文件”，或者按 Ctrl+N。    。

2. 在“新建文件”对话框中选择左侧的“通用”类别，然后选择“代码分析规则集”  。

3. 选择“打开”  。

   规则集编辑器中会打开新的 .ruleset 文件。

## <a name="create-a-custom-rule-set-from-multiple-rule-sets"></a>根据多个规则集创建自定义规则集

> [!NOTE]
> 以下过程不适用于 .NET Core 或 .NET Standard 项目，这些项目不支持“代码分析”属性选项卡中的相同功能。

1. 在解决方案资源管理器中，右键单击项目，然后选择“属性” 。

2. 在“属性”页中，请选择“代码分析”选项卡 。

::: moniker range="vs-2017"

3. 在“运行此规则集”中，单击“\<Choose multiple rule sets>” 。

::: moniker-end

::: moniker range=">=vs-2019"

3. 在“活动规则”中，单击“\<Choose multiple rule sets>” 。

::: moniker-end

4. 在“添加或删除规则集”对话框中，选择要包括在新规则集的规则集。

   ![“添加或删除规则集”对话框](media/add-remove-rule-sets.png)

5. 选择“另存为”，输入 .ruleset 文件的名称，然后选择“保存”。

   在“运行此规则集”列表中，选择新规则集。

6. 选择“打开”，在规则集编辑器中打开新的规则集。

## <a name="rule-precedence"></a>规则优先级

- 如果同一规则在规则集内列出两次或多次且显示不同的严重性，编译器将生成错误。 例如：

   ```xml
   <RuleSet Name="Rules for ClassLibrary21" Description="Code analysis rules for ClassLibrary21.csproj." ToolsVersion="15.0">
     <Rules AnalyzerId="Microsoft.Analyzers.ManagedCodeAnalysis" RuleNamespace="Microsoft.Rules.Managed">
       <Rule Id="CA1021" Action="Warning" />
       <Rule Id="CA1021" Action="Error" />
     </Rules>
   </RuleSet>
   ```

- 如果同一规则在规则集内列出两次或多次且显示不同的严重性，那么你可能会在错误列表中看到以下警告：

   CA0063: 未能加载规则集文件 "\[your].ruleset" 或其依赖的规则集文件之一。该文件不符合规则集架构。

- 如果规则集使用 Include 标记包含子规则集，并且子规则集和父规则集都列出相同规则，但具有不同的严重性，则父规则集中的严重性优先。 例如：

   ```xml
   <!-- Parent rule set -->
   <?xml version="1.0" encoding="utf-8"?>
   <RuleSet Name="Rules for ClassLibrary21" Description="Code analysis rules for ClassLibrary21.csproj." ToolsVersion="15.0">
     <Include Path="classlibrary_child.ruleset" Action="Default" />
     <Rules AnalyzerId="Microsoft.Analyzers.ManagedCodeAnalysis" RuleNamespace="Microsoft.Rules.Managed">
       <Rule Id="CA1021" Action="Warning" /> <!-- Overrides CA1021 severity from child rule set -->
     </Rules>
   </RuleSet>

   <!-- Child rule set -->
   <?xml version="1.0" encoding="utf-8"?>
   <RuleSet Name="Rules from child" Description="Code analysis rules from child." ToolsVersion="15.0">
     <Rules AnalyzerId="Microsoft.Analyzers.ManagedCodeAnalysis" RuleNamespace="Microsoft.Rules.Managed">
       <Rule Id="CA1021" Action="Error" />
     </Rules>
   </RuleSet>
   ```

## <a name="name-and-description"></a>名称和说明

若要更改在编辑器中打开的规则集的显示名称，请选择菜单栏上的“视图” > “属性窗口”，打开属性窗口  。 在“名称”框中输入显示名称。 还可输入规则集的说明。

## <a name="next-steps"></a>后续步骤

有了规则集后，接下来是添加或删除规则或修改规则冲突的严重性来自定义规则。

> [!div class="nextstepaction"]
> [在规则集编辑器中修改规则](../code-quality/working-in-the-code-analysis-rule-set-editor.md)

## <a name="see-also"></a>另请参阅

- [如何：配置托管代码项目的代码分析](../code-quality/how-to-configure-code-analysis-for-a-managed-code-project.md)
- [代码分析规则集参考](../code-quality/rule-set-reference.md)
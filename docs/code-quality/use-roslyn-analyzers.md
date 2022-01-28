---
title: 分析器配置
ms.date: 01/24/2022
description: 了解如何自定义 Roslyn 分析器规则。 了解如何调整分析器严重性、抑制冲突以及将文件指定为生成的代码。
ms.custom: SEO-VS-2020, devdivchpfy22
ms.topic: conceptual
helpviewer_keywords:
- code analysis, managed code
- analyzers
- Roslyn analyzers
author: mikadumont
ms.author: midumont
manager: jmartens
ms.technology: vs-ide-code-analysis
ms.workload:
- dotnet
ms.openlocfilehash: 928cc90c5e9017f7e2362e179bea0fc2edb2c03f
ms.sourcegitcommit: f303d052e451bcfd4722b99a9adbcb3f575d1678
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/27/2022
ms.locfileid: "137816825"
---
# <a name="overview"></a>概述

每个 Roslyn 分析器诊断或规则都有默认的严重性和抑制状态，可在项目中对其覆盖和自定义。 本文介绍了如何设置分析器严重性和抑制分析器冲突。

## <a name="configure-severity-levels"></a>配置严重性级别

::: moniker range=">=vs-2019"

从 Visual Studio 2019 版16.3 开始，你可以在 [EditorConfig 文件](#set-rule-severity-in-an-editorconfig-file)中的 "灯泡"[菜单](#set-rule-severity-from-the-light-bulb-menu)和 "错误列表" 中配置分析器规则或 *诊断* 的严重性。

::: moniker-end

::: moniker range="vs-2017"

如果以 NuGet 包的形式[安装分析器](../code-quality/install-roslyn-analyzers.md)，可以配置分析器规则或诊断的严重性。 可以[从解决方案资源管理器](#set-rule-severity-from-solution-explorer)或[在规则集文件中](#set-rule-severity-in-the-rule-set-file)更改规则的严重性。

::: moniker-end

下表显示了不同的严重性选项：

| 严重性（解决方案资源管理器） | 严重性（EditorConfig 文件） | 生成时行为 | 编辑器行为 |
|-|-|-|
| 错误 | `error` | 此类冲突在错误列表和命令行生成输出中显示为“错误”，并导致生成失败。| 违规代码用红色波浪下划线表示，并用滚动条中的红色小框标记。 |
| 警告 | `warning` | 冲突在错误列表和命令行生成输出中显示为 *警告* ，但不会导致生成失败。 | 违规代码用绿色波浪下划线表示，并用滚动条中的绿色小框标记。 |
| 信息 | `suggestion` | 此类冲突在错误列表中显示为“消息”，而不会在命令行生成输出中显示。 | 违规代码用灰色波浪下划线表示，并用滚动条中的灰色小框标记。 |
| Hidden | `silent` | 对用户不可见。 | 对用户不可见。 但是，诊断会报告给 IDE 诊断引擎。 |
| 无 | `none` | 完全禁止显示。 | 完全禁止显示。 |
| 默认 | `default` | 对应于规则的默认严重性。 若要确定规则的默认值，请查看“属性”窗口。 | 对应于规则的默认严重性。 |

分析器发现的规则冲突在 "代码编辑器" 中以波形曲线的形式出现在 "有问题的代码" 下， (作为 *波形曲线* 出现) 在 "错误列表" 窗口中。

错误列表中报告的分析器冲突与规则的[严重性级别设置](../code-quality/use-roslyn-analyzers.md#configure-severity-levels)相匹配。 分析器冲突也会在代码编辑器中以波浪线的形式显示在违规代码下。 下图显示了三个冲突&mdash;一个错误（红色波浪线）、一个警告（绿色波浪线）和一个建议（三个灰点）：

![Visual Studio 中代码编辑器中的波浪线](media/diagnostics-severity-colors.png)

以下屏幕截图显示了相同的三个冲突在错误列表中的样子：

![错误列表中的错误、警告和信息冲突](media/diagnostics-severities-in-error-list.png)

许多分析器规则或诊断都有一个或多个相关的代码修复程序，可以应用它们来纠正规则冲突。 代码修复以及其他类型的[快速操作](../ide/quick-actions.md)显示在灯泡图标菜单中。 有关这些代码修复的信息，请参阅[常见快速操作](../ide/quick-actions.md)。

![分析器冲突和快速操作代码修复](../code-quality/media/built-in-analyzer-code-fix.png)

### <a name="hidden-severity-versus-none-severity"></a>“隐藏”严重性与“无”严重性

`Hidden` 默认情况下启用的严重级别规则不同于 `None` 某些方面的 "已禁用" 或 "严重性规则"。

- 如果为严重级别规则注册了任何代码修复 `Hidden` ，Visual Studio 会将修复作为灯泡代码重构操作提供，即使隐藏的诊断对用户不可见。 如果严重级别规则被禁用，则不提供此修补程序 `None` 。
- `Hidden` 严重性规则可以通过条目[在 EditorConfig 文件中一次性设置多个分析器规则的规则严重性](#set-rule-severity-of-multiple-analyzer-rules-at-once-in-an-editorconfig-file)进行批量配置。 `None` 不能以这种方式配置严重级别规则。 而是必须通过条目[在 EditorConfig 文件中为每个规则 ID 设置规则严重性](#set-rule-severity-in-an-editorconfig-file)进行配置。

::: moniker range=">=vs-2019"

### <a name="set-rule-severity-in-an-editorconfig-file"></a>在 EditorConfig 文件中设置规则严重性

（Visual Studio 2019 版本 16.3 及更高版本）

可以使用以下语法在 EditorConfig 文件中为编译器警告或分析器规则设置严重性：

`dotnet_diagnostic.<rule ID>.severity = <severity>`

在 EditorConfig 文件中设置规则的严重性优先于在规则集或解决方案资源管理器中设置的任何严重性。 你可以在 EditorConfig 文件中[手动](#manually-configure-rule-severity-in-an-editorconfig-file)配置严重性，或者通过出现在冲突旁边的灯泡[自动](#set-rule-severity-from-the-light-bulb-menu)配置。

### <a name="set-rule-severity-of-multiple-analyzer-rules-at-once-in-an-editorconfig-file"></a>在 EditorConfig 文件中一次性设置多个分析器规则的规则严重性

（Visual Studio 2019 版本 16.5 及更高版本）

可以使用 EditorConfig 文件中的单个条目为特定类别的分析器规则或所有分析器规则设置严重性。

- 为某类分析器规则设置规则严重性：

`dotnet_analyzer_diagnostic.category-<rule category>.severity = <severity>`

- 为所有分析器规则设置规则严重性：

`dotnet_analyzer_diagnostic.severity = <severity>`

> [!NOTE]
> 一次性配置多个分析器规则的条目仅适用于默认已启用的规则。 在分析器包中默认标记为“已禁用”的分析器规则必须通过显式的 `dotnet_diagnostic.<rule ID>.severity = <severity>` 条目来启用。

如果有多个项适用于特定的规则 ID，则适用项的优先顺序如下：

- 基于 ID 的单个规则的严重性条目优先于一个类别的严重性条目。
- 一个类别的严重性条目优先于所有分析器规则的严重性条目。

请考虑以下 EditorConfig 示例，其中 [CA1822](/dotnet/fundamentals/code-analysis/quality-rules/ca1822) 属于“性能”类别：

   ```ini
   [*.cs]
   dotnet_diagnostic.CA1822.severity = error
   dotnet_analyzer_diagnostic.category-performance.severity = warning
   dotnet_analyzer_diagnostic.severity = suggestion
   ```

在前面的示例中，所有这三个条目都适用于 CA1822。 但是，按照指定的优先级规则，第一个基于规则 ID 的严重性条目优先于后续条目。 在此示例中，CA1822 的严重严重性为 "错误"。 剩余的 "性能" 类别规则的严重性为 "warning"，没有 "性能" 类别的分析器规则的严重性为 "建议"。

#### <a name="manually-configure-rule-severity-in-an-editorconfig-file"></a>在 EditorConfig 文件中手动配置规则严重性

1. 如果你的项目还没有 EditorConfig 文件，请[添加一个](../ide/create-portable-custom-editor-options.md#add-an-editorconfig-file-to-a-project)。

2. 在相应的文件扩展名下为要配置的每个规则添加一个条目。 例如，若要将 C# 文件的 [CA1822](/dotnet/fundamentals/code-analysis/quality-rules/ca1822) 的严重性设置为 `error`，条目如下所示：

   ```ini
   [*.cs]
   dotnet_diagnostic.CA1822.severity = error
   ```

> [!NOTE]
> 对于 IDE 代码样式分析器，还可以使用不同的语法（例如 `dotnet_style_qualification_for_field = false:suggestion`）在 EditorConfig 文件中配置它们。 但是，如果使用 `dotnet_diagnostic` 语法设置严重性，则优先使用该严重性。 有关详细信息，请参阅 [EditorConfig 适用的 .NET 语言约定](/dotnet/fundamentals/code-analysis/style-rules/language-rules)。

### <a name="set-rule-severity-from-the-light-bulb-menu"></a>从灯泡菜单设置规则严重性

Visual Studio 提供了一种从[快速操作](../ide/quick-actions.md)灯泡菜单配置规则严重性的方便方法。

1. 发生冲突后，将鼠标悬停在编辑器中表示冲突的波浪线上，然后打开灯泡菜单。 或者，将光标放在该行上并按 Ctrl+.  （句点）。

2. 从灯泡菜单中，选择“配置或禁止显示问题”>“配置 \<rule ID> 的严重性” 。

   ![从 Visual Studio 的灯泡菜单配置规则严重性](media/configure-rule-severity.png)

3. 从此处选择一个严重性选项。

   ![将规则严重性配置为“建议”](media/configure-rule-severity-suggestion.png)

   Visual Studio 会在 EditorConfig 文件中添加一个条目，以将规则配置为请求的级别，如预览框中所示。

   > [!TIP]
   > 如果项目中还没有 EditorConfig 文件，Visual Studio 将为你创建一个。

### <a name="set-rule-severity-from-the-error-list-window"></a>从“错误列表”窗口设置规则严重性

Visual Studio 还提供了一种从“错误列表”上下文菜单配置规则严重性的方便方法。

1. 发生冲突后，右键单击“错误列表”中的诊断条目。

2. 从上下文菜单中选择“设置严重性”。

   ![从 Visual Studio 中的“错误列表”配置规则严重性](media/configure-rule-severity-error-list.png)

3. 从此处选择一个严重性选项。

   Visual Studio 会在 EditorConfig 文件中添加一个条目，以将规则配置为请求的级别。

   > [!TIP]
   > 如果项目中还没有 EditorConfig 文件，Visual Studio 将为你创建一个。

::: moniker-end

### <a name="set-rule-severity-from-solution-explorer"></a>从解决方案资源管理器设置规则严重性

可以在“解决方案资源管理器”中自定义分析器诊断。 如果以 NuGet 包的形式[安装分析器](../code-quality/install-roslyn-analyzers.md)，则“解决方案资源管理器”中的“引用”或“依赖项”节点下会出现“分析器”节点   。 如果展开“分析器”，然后展开其中一个分析器程序集，你将看到该程序集中的所有诊断。

![解决方案资源管理器中的分析器节点](media/analyzers-expanded-in-solution-explorer.png)

可以在“属性”窗口中查看诊断的属性，包括其描述和默认严重性。 若要查看属性，请右键单击规则并选择"属性 **"，** 或选择规则，然后按 **Alt** + **Enter**。

![属性窗口中的诊断属性](media/analyzer-diagnostic-properties.png)

若要查看诊断的联机文档，请右键单击诊断并选择“查看帮助”。

**解决方案资源管理器** 中每个诊断旁边的图标对应于在编辑器中打开规则集时在其中看到的图标：

- 圆圈中的"x"指示 [错误](#configure-severity-levels)**的严重性**
- 三角形中的"！" 指示 [警告](#configure-severity-levels)**的严重性**
- 圆圈中的"i"表示 [信息](#configure-severity-levels)**的严重性**
- 浅色背景上的圆圈中的"i"表示 [严重性为](#configure-severity-levels)**"隐藏"**
- 圆圈中的向下箭头指示诊断已取消

![解决方案资源管理器中的诊断图标](media/diagnostics-icons-solution-explorer.png)

::: moniker range=">=vs-2019"

#### <a name="convert-an-existing-ruleset-file-to-editorconfig-file"></a>将现有的 Ruleset 文件转换为 EditorConfig 文件

从 Visual Studio 2019 版本 16.5 开始，不建议使用 ruleset 文件，请改为针对用于托管代码的分析器配置使用 EditorConfig 文件。 用于分析Visual Studio严重性配置的大多数工具都更新为适用于 EditorConfig 文件，而不是规则集文件。 EditorConfig 文件允许配置分析器规则严重性和分析器选项，包括Visual Studio IDE 代码样式选项。 建议将现有规则集文件转换为 EditorConfig 文件。 此外，将 EditorConfig 文件保存在存储库的根目录或解决方案文件夹中。 通过使用存储库或解决方案文件夹的根目录，你可以确保此文件中的严重性设置分别自动应用于整个存储库或解决方案。

可通过几种方法将现有 ruleset 文件转换为 EditorConfig 文件：

- 通过 Visual Studio 中的 Ruleset 编辑器（需要 Visual Studio 2019 16.5 或更高版本）。 如果项目已将特定 ruleset 文件用作其 `CodeAnalysisRuleSet`，可以通过 Visual Studio 中的 Ruleset 编辑器将其转换为等效的 EditorConfig 文件。

    1. 在“解决方案资源管理器”中双击“ruleset 文件”。

       Ruleset 文件应会在 Ruleset 编辑器中打开。 Ruleset 编辑器的顶部应会出现一个可点击的信息栏。

       ![在 Ruleset 编辑器中将 Ruleset 转换为 EditorConfig 文件](media/convert-ruleset-to-editorconfig-file-ruleset-editor.png)

    2. 选择“信息栏”链接。

       该操作应打开" **另存** 为"对话框，用于选择要生成 EditorConfig 文件的目录。

    3. 选择“保存”按钮以生成 EditorConfig 文件。

       生成的 EditorConfig 应会在编辑器中打开。 此外，MSBuild 属性 `CodeAnalysisRuleSet` 在项目文件中进行了更新，因此它不再引用原始 ruleset 文件。

- 通过命令行：

    1. 安装 NuGet 包 [Microsoft.CodeAnalysis.RulesetToEditorconfigConverter](https://www.nuget.org/packages/Microsoft.CodeAnalysis.RulesetToEditorconfigConverter)。

    2. 从已安装的包中执行 `RulesetToEditorconfigConverter.exe`，并将 ruleset 文件和 EditorConfig 文件的路径作为命令行参数。

   ```
   Usage: RulesetToEditorconfigConverter.exe <%ruleset_file%> [<%path_to_editorconfig%>]
   ```

下面是要转换的示例规则集文件：

```xml
<?xml version="1.0" encoding="utf-8"?>
<RuleSet Name="Rules for ConsoleApp" Description="Code analysis rules for ConsoleApp.csproj." ToolsVersion="16.0">
  <Rules AnalyzerId="Microsoft.Analyzers.ManagedCodeAnalysis" RuleNamespace="Microsoft.Rules.Managed">
    <Rule Id="CA1001" Action="Warning" />
    <Rule Id="CA1821" Action="Warning" />
    <Rule Id="CA2213" Action="Warning" />
    <Rule Id="CA2231" Action="Warning" />
  </Rules>
</RuleSet>
```

下面是转换后的 EditorConfig 文件：

```ini
# NOTE: Requires **VS2019 16.3** or later

# Rules for ConsoleApp
# Description: Code analysis rules for ConsoleApp.csproj.

# Code files
[*.{cs,vb}]


dotnet_diagnostic.CA1001.severity = warning

dotnet_diagnostic.CA1821.severity = warning

dotnet_diagnostic.CA2213.severity = warning

dotnet_diagnostic.CA2231.severity = warning
```
::: moniker-end

### <a name="set-rule-severity-from-solution-explorer"></a>从解决方案资源管理器设置规则严重性

1. 在“解决方案资源管理器”中，展开“引用” > “分析器”（如果是 .NET Core 项目，则为“依赖项” > “分析器”）   。

2. 展开包含待设置严重性的规则的程序集。

::: moniker range=">=vs-2019"
3. 右键单击规则并选择“设置严重性”。 在上下文菜单中，选择其中一个严重性选项。

   Visual Studio 会在 EditorConfig 文件中添加一个条目，以将规则配置为请求的级别。 如果项目使用的是 ruleset 文件而不是 EditorConfig 文件，则会将严重性条目添加到 ruleset 文件中。

   > [!TIP]
   > 如果项目中还没有 EditorConfig 文件或 ruleset 文件，Visual Studio 会创建一个新的 EditorConfig 文件。
::: moniker-end

::: moniker range="vs-2017"
3. 右键单击规则并选择“设置规则集严重性”。 在上下文菜单中，选择其中一个严重性选项。

   规则的严重性保存在活动规则集文件中。
::: moniker-end

### <a name="set-rule-severity-in-the-rule-set-file"></a>在规则集文件中设置规则严重性

1. 通过下列方式之一打开活动规则集文件：

    - 在 **解决方案资源管理器** 中，双击文件，右键单击"引用分析器"节点，  >  然后选择"**打开活动规则集"。**
  
        ![解决方案资源管理器中的规则集文件](media/ruleset-in-solution-explorer.png)

    - 在项目的“Code Analysis”属性页上，选择“打开” 。

    如果是首次编辑规则集，Visual Studio创建默认规则集文件的副本，将其命名为 *\<projectname> .ruleset*，并添加到项目中。 此自定义规则集也将成为项目的活动规则集。

    > [!NOTE]
    > .NET Core .NET Standard项目不支持中规则集的菜单命令解决方案资源管理器例如，**打开活动规则集**。  若要为 .NET Core 或 .NET Standard 项目指定非默认规则集，请在项目文件中手动[添加 CodeAnalysisRuleSet 属性](using-rule-sets-to-group-code-analysis-rules.md#specify-a-rule-set-for-a-project)。 你仍可以在 Visual Studio 规则集编辑器 UI 中的规则集内配置规则。

1. 展开包含规则的程序集并浏览到该规则。

1. 在“操作”列中，选择值以打开下拉列表，然后从列表中选择所需的严重性。

   ![在编辑器中打开规则集文件](media/ruleset-file-in-editor.png)

::: moniker range=">=vs-2019"

## <a name="configure-generated-code"></a>配置生成的代码

分析器在项目中的所有源文件上运行并在其上报告冲突。 但是，冲突对生成的代码文件（如设计器生成的代码文件、生成系统生成的临时源文件等）没有用。 用户无法手动编辑文件，并且不会担心在工具生成的文件中修复冲突。

默认情况下，运行分析器的分析器驱动程序将具有特定名称、文件扩展名或自动生成的文件头的文件视为生成的代码文件。 例如，以 .designer.cs 或 .generated.cs 结尾的文件名被视为生成的代码。 但是，这些启发可能无法识别用户源代码中所有自定义生成的代码文件。

从 Visual Studio 2019 16.5 开始，最终用户可以将特定文件和/或文件夹配置为在 [EditorConfig 文件](https://editorconfig.org/)中生成的代码。 按照以下步骤添加此类配置：

1. 如果你的项目还没有 EditorConfig 文件，请[添加一个](../ide/create-portable-custom-editor-options.md#add-an-editorconfig-file-to-a-project)。

2. 为特定文件和/或文件夹添加 `generated_code = true | false` 条目。 例如，若要将其名称以 `.MyGenerated.cs` 结尾的所有文件视为生成的代码，条目将如下所示：

   ```ini
   [*.MyGenerated.cs]
   generated_code = true
   ```

::: moniker-end

## <a name="suppress-violations"></a>禁止显示冲突

可以使用各种方法抑制规则冲突。 有关详细信息，请参阅[抑制代码分析冲突](../code-quality/in-source-suppression-overview.md)。

## <a name="command-line-usage"></a>命令行用法

在命令行生成项目时，如果满足以下条件，则生成输出中将显示规则冲突：

- 分析器随 .NET SDK 一起安装或作为 NuGet 包（而不是作为 VSIX 扩展）安装。

  对于使用 .NET SDK 安装的分析器，可能需要[启用分析器](../code-quality/install-net-analyzers.md)。 对于代码样式，也可通过设置 MSBuild 属性[在生成时强制执行代码样式](/dotnet/fundamentals/code-analysis/overview#code-style-analysis)。

- 项目的代码中违反了一个或多个规则。

- 代码所违反规则的[严重性](#configure-severity-levels)设置为“警告”（在这种情况下，违规不会导致生成失败）或“错误”（在这种情况下，违规会导致生成失败） 。

生成输出详细程度不会影响是否显示规则冲突。 即使有“相当级别”的详细程度，规则冲突也会出现在生成输出中。

> [!TIP]
> 如果你习惯于使用 FxCopCmd.exe 或通过 msbuild 使用“RunCodeAnalysis”标志从命令行运行旧版分析，下面介绍了如何对代码分析器执行该操作，供你参考。

若要在使用 msbuild 生成项目时在命令行中查看分析器冲突，请运行以下命令：

```cmd
msbuild myproject.csproj /target:rebuild /verbosity:minimal
```

以下图像显示了生成包含分析器规则冲突的项目时的命令行生成输出：

![带规则冲突的 MSBuild 输出](media/command-line-build-analyzers.png)

## <a name="dependent-projects"></a>依赖项目

在 .NET Core 项目中，如果添加对具有分析器NuGet的引用，则这些分析器也会自动添加到依赖项目中。 若要禁用此行为，例如，如果依赖项目是单元测试项目，请通过设置 **PrivateAssets** 属性，在所引用项目的 *.csproj* 或 *.vbproj* 文件中将 NuGet 包标记为私有：

```xml
<PackageReference Include="Microsoft.CodeAnalysis.NetAnalyzers" Version="5.0.0" PrivateAssets="all" />
```

## <a name="see-also"></a>另请参阅

- [Visual Studio 中的代码分析器概述](../code-quality/roslyn-analyzers-overview.md)
- [提交代码分析器 bug](https://github.com/dotnet/roslyn-analyzers/issues)
- [使用规则集](../code-quality/using-rule-sets-to-group-code-analysis-rules.md)
- [抑制代码分析警告](../code-quality/in-source-suppression-overview.md)
- [用于代码分析的配置选项 (.NET)](/dotnet/fundamentals/code-analysis/configuration-options)
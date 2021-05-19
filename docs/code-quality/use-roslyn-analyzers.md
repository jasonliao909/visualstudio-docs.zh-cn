---
title: 分析器配置
ms.date: 05/10/2021
description: 了解如何自定义 Roslyn 分析器规则。 请参阅如何调整分析器严重性，取消冲突，并将文件指定为生成的代码。
ms.custom: SEO-VS-2020
ms.topic: conceptual
helpviewer_keywords:
- code analysis, managed code
- analyzers
- Roslyn analyzers
author: mikadumont
ms.author: midumont
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: 36a9f1651a4aef7742b6bf52f8691f6ae8f9c616
ms.sourcegitcommit: 162be102d2c22a1c4ad2c447685abd28e0e85d15
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2021
ms.locfileid: "109973377"
---
# <a name="overview"></a>概述

每个 Roslyn 分析器 *诊断* 或规则都有一个默认严重性和隐含状态，可对项目进行覆盖和自定义。 本文介绍如何设置分析器严重级别并抑制分析器冲突。

## <a name="configure-severity-levels"></a>配置严重级别

::: moniker range=">=vs-2019"

从 Visual Studio 2019 版本16.3 开始，你可以在 [EditorConfig 文件](#set-rule-severity-in-an-editorconfig-file)中的 "灯泡"[菜单](#set-rule-severity-from-the-light-bulb-menu)和 "错误列表" 中配置分析器规则或 *诊断* 的严重性。

::: moniker-end

::: moniker range="vs-2017"

如果将分析器作为 NuGet 包进行 [安装](../code-quality/install-roslyn-analyzers.md)，则可以配置分析器规则或 *诊断* 的严重性。 你可以 [从解决方案资源管理器](#set-rule-severity-from-solution-explorer) 或 [规则集文件中](#set-rule-severity-in-the-rule-set-file)更改规则的严重性。

::: moniker-end

下表显示了不同的严重性选项：

| 严重性（解决方案资源管理器） | 严重性（EditorConfig 文件） | 生成时行为 | 编辑器行为 |
|-|-|-|
| 错误 | `error` | 此类冲突在错误列表和命令行生成输出中显示为“错误”，并导致生成失败。| 违规代码用红色波浪下划线表示，并用滚动条中的红色小框标记。 |
| 警告 | `warning` | 此类冲突在错误列表和命令行生成输出中显示为“警告”，但不会导致生成失败。 | 违规代码用绿色波浪下划线表示，并用滚动条中的绿色小框标记。 |
| 信息 | `suggestion` | 此类冲突在错误列表中显示为“消息”，而不会在命令行生成输出中显示。 | 违规代码用灰色波浪下划线表示，并用滚动条中的灰色小框标记。 |
| Hidden | `silent` | 对用户不可见。 | 对用户不可见。 但是，诊断会报告给 IDE 诊断引擎。 |
| 无 | `none` | 完全禁止显示。 | 完全禁止显示。 |
| 默认 | `default` | 对应于规则的默认严重性。 若要确定规则的默认值，请查看“属性”窗口。 | 对应于规则的默认严重性。 |

如果分析器发现规则冲突，将在代码编辑器（违规代码下方有波浪线）和“错误列表”窗口中报告。

错误列表中报告的分析器冲突与规则的[严重性级别设置](../code-quality/use-roslyn-analyzers.md#configure-severity-levels)相匹配。 分析器冲突也会在代码编辑器中以波浪线的形式显示在违规代码下。 下图显示了三个冲突&mdash;一个错误（红色波浪线）、一个警告（绿色波浪线）和一个建议（三个灰点）：

![Visual Studio 中代码编辑器中的波浪线](media/diagnostics-severity-colors.png)

以下屏幕截图显示的是错误列表中显示的三个冲突：

![错误列表中的错误、警告和信息冲突](media/diagnostics-severities-in-error-list.png)

许多分析器规则或诊断都有一个或多个相关的代码修复程序，可以应用它们来纠正规则冲突。 代码修复以及其他类型的[快速操作](../ide/quick-actions.md)显示在灯泡图标菜单中。 有关这些代码修复的信息，请参阅[常见快速操作](../ide/quick-actions.md)。

![分析器冲突和快速操作代码修复](../code-quality/media/built-in-analyzer-code-fix.png)

### <a name="hidden-severity-versus-none-severity"></a>"Hidden" 严重性与 "无" 严重性

`Hidden` 默认情况下启用的严重级别规则不同于禁用或 `None` 严重性规则。

- 如果已为某个严重性规则注册了任何代码修复，则在 `Hidden` Visual Studio 中将此修补程序作为灯泡代码重构操作提供，即使用户看不到隐藏的诊断也是如此。 这不是已禁用的 `None` 严重性规则的情况。
- `Hidden` 可以通过在 [EditorConfig 文件中同时设置多个分析器规则的规则严重性的](#set-rule-severity-of-multiple-analyzer-rules-at-once-in-an-editorconfig-file)项来批量配置严重级别规则。 `None` 不能以这种方式配置严重级别规则。 相反，必须通过在 [EditorConfig 文件中为每个规则 ID 设置规则严重性](#set-rule-severity-in-an-editorconfig-file)的条目来配置它们。

::: moniker range=">=vs-2019"

### <a name="set-rule-severity-in-an-editorconfig-file"></a>在 EditorConfig 文件中设置规则严重性

 (Visual Studio 2019 版本16.3 及更高版本) 

可以使用以下语法在 EditorConfig 文件中设置编译器警告或分析器规则的严重性：

`dotnet_diagnostic.<rule ID>.severity = <severity>`

在 EditorConfig 文件中设置规则的严重性优先于规则集或规则设置中设置的任何解决方案资源管理器。 可以在 [EditorConfig](#manually-configure-rule-severity-in-an-editorconfig-file) 文件中手动配置严重性，或者 [通过](#set-rule-severity-from-the-light-bulb-menu) 冲突旁边出现的灯泡自动配置严重性。

### <a name="set-rule-severity-of-multiple-analyzer-rules-at-once-in-an-editorconfig-file"></a>在 EditorConfig 文件中一次设置多个分析器规则的规则严重性

 (Visual Studio 2019 版本 16.5 及更高版本) 

可以设置特定分析器规则类别或 EditorConfig 文件中单个条目的所有分析器规则的严重性。

- 为分析器规则类别设置规则严重性：

`dotnet_analyzer_diagnostic.category-<rule category>.severity = <severity>`

- 设置所有分析器规则的规则严重性：

`dotnet_analyzer_diagnostic.severity = <severity>`

> [!NOTE]
> 用于一次配置多个分析器规则的条目仅适用于默认 *启用的规则*。 分析器包中默认标记为禁用的分析器规则必须通过显式条目 `dotnet_diagnostic.<rule ID>.severity = <severity>` 启用。

如果有多个适用于特定规则 ID 的条目，则选择适用条目的优先顺序如下：

- 按 ID 表示的单个规则的严重性条目优先于类别的严重性条目。
- 类别的严重性条目优先于所有分析器规则的严重性条目。

请考虑以下 EditorConfig 示例，其中 [CA1822](/dotnet/fundamentals/code-analysis/quality-rules/ca1822) 的类别为"性能"：

   ```ini
   [*.cs]
   dotnet_diagnostic.CA1822.severity = error
   dotnet_analyzer_diagnostic.category-performance.severity = warning
   dotnet_analyzer_diagnostic.severity = suggestion
   ```

在上一示例中，所有三个条目都适用于 CA1822。 但是，使用指定的优先规则时，第一个基于规则 ID 的严重性条目优先于下一个条目。 此示例中，CA1822 的有效严重性为"error"。 具有"性能"类别的所有剩余规则将具有严重性"警告"。 所有剩余的分析器规则（没有"性能"类别）将具有严重性"建议"。

#### <a name="manually-configure-rule-severity-in-an-editorconfig-file"></a>在 EditorConfig 文件中手动配置规则严重性

1. 如果你的项目还没有 EditorConfig 文件，则 [添加一个](../ide/create-portable-custom-editor-options.md#add-an-editorconfig-file-to-a-project)。

2. 在相应的文件扩展名下为要配置的每个规则添加一个条目。 例如，若要将 [CA1822](/dotnet/fundamentals/code-analysis/quality-rules/ca1822) 的严重性设置为 `error` c # 文件，该条目如下所示：

   ```ini
   [*.cs]
   dotnet_diagnostic.CA1822.severity = error
   ```

> [!NOTE]
> 对于 IDE 代码样式分析器，还可以使用不同的语法（例如）在 EditorConfig 文件中配置它们 `dotnet_style_qualification_for_field = false:suggestion` 。 但是，如果使用语法设置了严重性 `dotnet_diagnostic` ，则优先使用该语法。 有关详细信息，请参阅 [EditorConfig 的语言约定](/dotnet/fundamentals/code-analysis/style-rules/language-rules)。

### <a name="set-rule-severity-from-the-light-bulb-menu"></a>设置灯泡菜单中的规则严重性

Visual Studio 提供了一种简便的方法，可用于在 " [快速操作](../ide/quick-actions.md) " 灯泡菜单中配置规则的严重性。

1. 发生冲突后，将鼠标悬停在编辑器中的冲突波形曲线上，并打开灯泡菜单。 或者，将光标放在行上，然后按 **Ctrl** 键 + **。** （句点）。

2. 在灯泡菜单中，选择 " **配置" 或 "禁止显示问题** > **配置 \<rule ID> 严重级别**"。

   ![在 Visual Studio 中配置灯泡菜单中的规则严重性](media/configure-rule-severity.png)

3. 从此处选择一个严重性选项。

   ![将规则严重性配置为建议](media/configure-rule-severity-suggestion.png)

   Visual Studio 将向 EditorConfig 文件中添加一个条目，以将规则配置为请求的级别，如 "预览" 框中所示。

   > [!TIP]
   > 如果项目中还没有 EditorConfig 文件，则 Visual Studio 会为你创建一个。

### <a name="set-rule-severity-from-the-error-list-window"></a>从 "错误列表" 窗口中设置规则严重性

Visual Studio 还提供了一种简便的方法来配置 "错误列表" 上下文菜单中的规则严重性。

1. 发生冲突后，右键单击 "错误列表" 中的诊断条目。

2. 从上下文菜单中，选择 " **设置严重性**"。

   ![从错误列表中的错误列表配置规则Visual Studio](media/configure-rule-severity-error-list.png)

3. 从中选择一个严重性选项。

   Visual Studio EditorConfig 文件添加一个条目，以将规则配置为请求的级别。

   > [!TIP]
   > 如果项目中还没有 EditorConfig 文件，Visual Studio创建一个。

::: moniker-end

### <a name="set-rule-severity-from-solution-explorer"></a>从设置规则严重性解决方案资源管理器

可以从 中自定义分析器诊断 **解决方案资源管理器。** 如果将 [分析器安装](../code-quality/install-roslyn-analyzers.md)为 NuGet 包，则 **分析器** 节点会显示在"引用" 或 "依赖项" 节点 **解决方案资源管理器。** 如果展开 **"分析器"，** 然后展开其中一个分析器程序集，则会看到程序集中的所有诊断。

![分析器节点解决方案资源管理器](media/analyzers-expanded-in-solution-explorer.png)

可以在"属性"窗口中查看诊断的属性，包括其说明和 **默认** 严重性。 若要查看属性，请右键单击规则并选择"属性 **"，** 或选择规则，然后按 **Alt** + **Enter**。

![诊断属性属性窗口](media/analyzer-diagnostic-properties.png)

若要查看诊断的联机文档，请右键单击诊断并选择"**查看帮助"。**

每个诊断旁边的图标解决方案资源管理器编辑器中打开规则集时看到的图标：

- 圆圈中的"x"指示 [错误](#configure-severity-levels)**的严重性**
- 三角形中的"！" 指示 [警告](#configure-severity-levels)**的严重性**
- 圆圈中的"i"指示 [信息](#configure-severity-levels)**的严重性**
- 浅色背景上的圆圈中的"i"指示 ["隐藏"](#configure-severity-levels)**的严重性**
- 圆圈中的向下箭头指示诊断已取消

![诊断图标解决方案资源管理器](media/diagnostics-icons-solution-explorer.png)

::: moniker range=">=vs-2019"

#### <a name="convert-an-existing-ruleset-file-to-editorconfig-file"></a>将现有的规则集文件转换为 EditorConfig 文件

从 Visual Studio 2019 版本16.5 开始，规则集文件已弃用，以支持托管代码的分析器配置的 EditorConfig 文件。 大多数用于 analyzer 的 Visual Studio 工具规则严重性配置已更新为在 EditorConfig 文件而不是规则集文件上运行。 EditorConfig 文件允许配置分析器规则严重性和分析器选项，包括 Visual Studio IDE 代码样式选项。 强烈建议将现有的规则集文件转换为 EditorConfig 文件。 此外，建议将 EditorConfig 文件保存到存储库的根目录或解决方案文件夹中。 通过使用存储库或解决方案文件夹的根，可以确保将此文件中的严重性设置分别自动应用于整个存储库或解决方案。

有几种方法可以将现有的规则集文件转换为 EditorConfig 文件：

- 在 Visual Studio 中的规则集编辑器中 (需要 Visual Studio 2019 16.5 或更高版本) 。 如果你的项目已使用特定规则集文件作为其 `CodeAnalysisRuleSet` ，则可以通过 Visual Studio 中的 "规则集编辑器" 将其转换为等效的 EditorConfig 文件。

    1. 双击解决方案资源管理器中的规则集文件。

       规则集文件应在规则集编辑器中打开。 "规则集编辑器" 顶部应该会显示一个可单击的 **信息栏** 。

       ![在规则集编辑器中将规则集转换为 EditorConfig 文件](media/convert-ruleset-to-editorconfig-file-ruleset-editor.png)

    2. 选择 " **信息栏** " 链接。

       这将打开 " **另存为** " 对话框，该对话框允许您选择要在其中生成 EditorConfig 文件的目录。

    3. 选择 " **保存** " 按钮以生成 EditorConfig 文件。

       生成的 EditorConfig 应在编辑器中打开。 此外，MSBuild 属性 `CodeAnalysisRuleSet` 在项目文件中进行了更新，使其不再引用原始规则集文件。

- 通过命令行：

    1. 安装 NuGet 包 [CodeAnalysis. RulesetToEditorconfigConverter](https://www.nuget.org/packages/Microsoft.CodeAnalysis.RulesetToEditorconfigConverter)。

    2. 从 `RulesetToEditorconfigConverter.exe` 已安装的包执行，规则集文件和 EditorConfig 文件的路径作为命令行参数。

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

### <a name="set-rule-severity-from-solution-explorer"></a>从设置规则严重性解决方案资源管理器

1. 在解决方案资源管理器中 **，展开**"引用分析器" (或 "用于 .NET Core 项目的依赖项分析器  >  "   >  ) 。

2. 展开包含要设置其严重性的规则的程序集。

::: moniker range=">=vs-2019"
3. 右键单击规则，然后选择"**设置严重性"。** 在上下文菜单中，选择一个严重性选项。

   Visual Studio EditorConfig 文件添加一个条目，以将规则配置为请求的级别。 如果项目使用规则集文件而不是 EditorConfig 文件，则严重性条目将添加到规则集文件。

   > [!TIP]
   > 如果项目中还没有 EditorConfig 文件或规则集文件，Visual Studio创建一个新的 EditorConfig 文件。
::: moniker-end

::: moniker range="vs-2017"
3. 右键单击规则，然后选择"**设置规则集严重性"。** 在上下文菜单中，选择一个严重性选项。

   规则的严重性保存在活动规则集文件中。
::: moniker-end

### <a name="set-rule-severity-in-the-rule-set-file"></a>在规则集文件中设置规则严重性

![规则集文件解决方案资源管理器](media/ruleset-in-solution-explorer.png)

1. 通过下列方式之一打开活动规则集文件：

- 在 **解决方案资源管理器** 中，双击文件，右键单击"引用分析器"节点，  >  然后选择"**打开活动规则集"。**
- 在项目的 **Code Analysis** 属性页上，选择"打开 **"。**

  如果这是首次编辑规则集，Visual Studio创建默认规则集文件的副本，将其命名为 *\<projectname> .ruleset*，并添加到项目中。 此自定义规则集还会成为项目的活动规则集。

   > [!NOTE]
   > .NET Core 和 .NET Standard 项目不支持 **解决方案资源管理器** 中规则集的菜单命令，例如， **打开活动规则集**。 若要为 .NET Core 或 .NET Standard 项目指定非默认规则集，请手动 [将 **CodeAnalysisRuleSet** 属性添加](using-rule-sets-to-group-code-analysis-rules.md#specify-a-rule-set-for-a-project) 到项目文件。 你仍可以在 Visual Studio 规则集编辑器 UI 中配置规则集内的规则。

1. 通过展开其包含的程序集，浏览到该规则。

1. 在 " **操作** " 列中，选择要打开下拉列表的值，并从列表中选择所需的严重性。

   ![已在编辑器中打开规则集文件](media/ruleset-file-in-editor.png)

::: moniker range=">=vs-2019"

## <a name="configure-generated-code"></a>配置生成的代码

分析器运行于项目中的所有源文件上，并在其上报告冲突。 但是，这些冲突对生成的代码文件（如设计器生成的代码文件、生成系统生成的临时源文件等）不起作用。用户无法手动编辑这些文件，并且/或者不关心修复这类工具生成文件中的冲突。

默认情况下，analyzer 驱动程序执行分析器会将具有特定名称、文件扩展名或自动生成的文件头的文件视为生成的代码文件。 例如，以 `.designer.cs` 或 `.generated.cs` 结尾的文件名被视为生成的代码。 但是，这些试探法可能无法确定用户源代码中所有自定义生成的代码文件。

从 Visual Studio 2019 16.5 开始，最终用户可以将特定的文件和/或文件夹配置为在 [EditorConfig 文件](https://editorconfig.org/)中被视为生成的代码。 按照以下步骤添加这样的配置：

1. 如果你的项目还没有 EditorConfig 文件，则 [添加一个](../ide/create-portable-custom-editor-options.md#add-an-editorconfig-file-to-a-project)。

2. 添加 `generated_code = true | false` 特定文件和/或文件夹的条目。 例如，若要将名称以结尾的所有文件视为 `.MyGenerated.cs` 生成的代码，该条目应如下所示：

   ```ini
   [*.MyGenerated.cs]
   generated_code = true
   ```

::: moniker-end

## <a name="suppress-violations"></a>禁止冲突

您可以使用各种方法取消规则冲突。 有关详细信息，请参阅 [取消代码分析冲突](../code-quality/in-source-suppression-overview.md)。

## <a name="command-line-usage"></a>命令行用法

在命令行生成项目时，如果满足以下条件，则生成输出中会出现规则冲突：

- 分析器随 .NET SDK 或 NuGet 包一起安装，而不是作为 VSIX 扩展安装。

  对于使用 .NET SDK 安装的分析器，可能需要 [启用分析器](../code-quality/install-net-analyzers.md)。 对于代码样式，还可通过设置 MSBuild [属性在](/dotnet/fundamentals/code-analysis/overview#code-style-analysis) 生成时强制实施代码样式。

- 项目代码中违反了一个或多个规则。

- 违反[规则](#configure-severity-levels)的严重性设置为警告 （在这种情况下，冲突不会导致生成失败）或错误 （在这种情况下，冲突会导致生成失败）。 

生成输出详细程度不会影响是否显示规则冲突。 即使不 **详细** ，生成输出中也会出现规则冲突。

> [!TIP]
> 如果你习惯从命令行运行旧分析，无论是使用 *FxCopCmd.exe，* 还是通过具有 **RunCodeAnalysis** 标志的 msbuild 运行，下面将了解如何使用代码分析器来运行。

若要在使用 msbuild 生成项目时在命令行查看分析器冲突，请运行如下所示的命令：

```cmd
msbuild myproject.csproj /target:rebuild /verbosity:minimal
```

以下图像显示了生成包含分析器规则冲突的项目时的命令行生成输出：

![带规则冲突的 MSBuild 输出](media/command-line-build-analyzers.png)

## <a name="dependent-projects"></a>依赖项目

在 .NET Core 项目中，如果添加对具有 NuGet 分析器的项目的引用，这些分析器也会自动添加到依赖项目中。 若要禁用此行为（例如，如果依赖项目是单元测试项目，请通过设置 **PrivateAssets** 属性，在所引用项目的 *.csproj* 或 *.vbproj* 文件中将 NuGet 包标记为专用）：

```xml
<PackageReference Include="Microsoft.CodeAnalysis.NetAnalyzers" Version="5.0.0" PrivateAssets="all" />
```

## <a name="see-also"></a>另请参阅

- [中代码分析器Visual Studio](../code-quality/roslyn-analyzers-overview.md)
- [提交代码分析器 bug](https://github.com/dotnet/roslyn-analyzers/issues)
- [使用规则集](../code-quality/using-rule-sets-to-group-code-analysis-rules.md)
- [抑制代码分析警告](../code-quality/in-source-suppression-overview.md)
- [用于代码分析的配置选项 (.NET) ](/dotnet/fundamentals/code-analysis/configuration-options)

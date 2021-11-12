---
title: 从 IDE 或命令行生成代码度量
ms.date: 11/02/2018
description: 了解如何在 Visual Studio 中生成代码度量数据。 了解如何使用解决方案资源管理器、规则集文件、命令行或菜单命令。
ms.custom: SEO-VS-2020
ms.topic: how-to
helpviewer_keywords:
- code metrics data
- code metrics results
- code metrics [Visual Studio]
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-code-analysis
ms.workload:
- multiple
ms.openlocfilehash: 1e7928b06a75ed3a27d654182ab65f0baeba6144
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601300"
---
# <a name="how-to-generate-code-metrics-data"></a>操作方法：生成代码度量数据

可以通过三种法生成代码度量数据：

- 通过启用 [.NET 代码质量分析器](#net-code-quality-analyzers-code-metrics-rules)并启用该分析器包含的四个代码度量（可维护性）规则。

- 通过在 Visual Studio 中选择[“分析” > “计算代码度量”](#calculate-code-metrics-menu-command)菜单命令 。

- 通过 C# 和 Visual Basic 项目的[命令行](#command-line-code-metrics)。

## <a name="net-code-quality-analyzers-code-metrics-rules"></a>.NET 代码质量分析器代码度量规则

.NET 代码质量分析器包括几个代码度量[分析器](roslyn-analyzers-overview.md)规则：

- [CA1501](/dotnet/fundamentals/code-analysis/quality-rules/ca1501)
- [CA1502](/dotnet/fundamentals/code-analysis/quality-rules/ca1502)
- [CA1505](/dotnet/fundamentals/code-analysis/quality-rules/ca1505)
- [CA1506](/dotnet/fundamentals/code-analysis/quality-rules/ca1506)

这些规则默认处于禁用状态，但你可以从[“解决方案资源管理器”](use-roslyn-analyzers.md#set-rule-severity-from-solution-explorer)或在 [EditorConfig](use-roslyn-analyzers.md#set-rule-severity-in-an-editorconfig-file) 文件中启用它们。 例如，若要启用规则 CA1502 作为警告，EditorConfig 文件将包含以下条目：

```cs
dotnet_diagnostic.CA1502.severity = warning
```

### <a name="configuration"></a>Configuration

可以配置触发代码度量规则的阈值。

1. 创建文本文件。 例如，可以将其命名为 CodeMetricsConfig.txt。

2. 按以下格式将所需的阈值添加到文本文件中：

   ```txt
   CA1502: 10
   ```

   在此示例中，规则 [CA1502](/dotnet/fundamentals/code-analysis/quality-rules/ca1502) 配置为在方法的圈复杂度大于 10 时触发。

3. 在 Visual Studio 的“属性”窗口或项目文件中，将配置文件的生成操作标记为 [AdditionalFiles](../ide/build-actions.md#build-action-values) 。 例如：

   ```xml
   <ItemGroup>
     <AdditionalFiles Include="CodeMetricsConfig.txt" />
   </ItemGroup>
   ```

## <a name="calculate-code-metrics-menu-command"></a>计算代码度量菜单命令

使用“分析” > “计算代码度量”菜单为 IDE 中的一个或所有打开的项目生成代码度量 。

### <a name="generate-code-metrics-results-for-an-entire-solution"></a>为整个解决方案生成代码度量结果

可以通过以下任一方式为整个解决方案生成代码度量结果：

- 从菜单栏中选择“分析” > “计算代码度量” > “解决方案”  。

- 在“解决方案资源管理器”中，右键单击解决方案，然后选择“计算代码度量” 。

- 在“代码度量结果”窗口中，选择“计算解决方案的代码度量”按钮 。

系统将生成结果并显示“代码度量结果”窗口。 若要查看结果详细信息，请展开“层次结构”列中的树。

### <a name="generate-code-metrics-results-for-one-or-more-projects"></a>为一个或多个项目生成代码度量结果

1. 在“解决方案资源管理器”中，选择一个或多个项目。

1. 从菜单栏中选择“分析” > “计算代码度量” > “对于选定的项目”  。

系统将生成结果并显示“代码度量结果”窗口。 若要查看结果详细信息，请展开“层次结构”中的树。

::: moniker range="vs-2017"

> [!NOTE]
> 计算代码度量命令不适用于 .NET Core 和 .NET Standard 项目。 若要计算 .NET Core 或 .NET Standard 项目的代码度量，可以：
>
> - 改为从[命令行](#command-line-code-metrics)计算代码度量
>
> - 升级到 [Visual Studio 2019](https://visualstudio.microsoft.com/downloads)

::: moniker-end

## <a name="command-line-code-metrics"></a>命令行代码度量

可以从命令行为 .NET Framework、.NET Core 和 .NET Standard 应用的 C# 和 Visual Basic 项目生成代码度量数据。 若要从命令行运行代码度量，请安装 [Microsoft.CodeAnalysis.Metrics NuGet 包](#microsoftcodeanalysismetrics-nuget-package)或自行生成 [Metrics.exe](#metricsexe) 可执行文件。

### <a name="microsoftcodeanalysismetrics-nuget-package"></a>Microsoft.CodeAnalysis.Metrics NuGet 包

从命令行生成代码度量数据的最简单方法是安装 [Microsoft.CodeAnalysis.Metrics](https://www.nuget.org/packages/Microsoft.CodeAnalysis.Metrics/) NuGet 包。 安装包后，从包含项目文件的目录运行 `msbuild /t:Metrics`。 例如：

```shell
C:\source\repos\ClassLibrary3\ClassLibrary3>msbuild /t:Metrics
Microsoft (R) Build Engine version 16.0.360-preview+g9781d96883 for .NET Framework
Copyright (C) Microsoft Corporation. All rights reserved.

Build started 1/22/2019 4:29:57 PM.
Project "C:\source\repos\ClassLibrary3\ClassLibrary3\ClassLibrary3.csproj" on node 1 (Metrics target(s))
.
Metrics:
  C:\source\repos\ClassLibrary3\packages\Microsoft.CodeMetrics.2.6.4-ci\build\\..\Metrics\Metrics.exe /project:C:\source\repos\ClassLibrary3\ClassLibrary3\ClassLibrary3.csproj /out:ClassLibrary3.Metrics.xml
  Loading ClassLibrary3.csproj...
  Computing code metrics for ClassLibrary3.csproj...
  Writing output to 'ClassLibrary3.Metrics.xml'...
  Completed Successfully.
Done Building Project "C:\source\repos\ClassLibrary3\ClassLibrary3\ClassLibrary3.csproj" (Metrics target(s)).

Build succeeded.
    0 Warning(s)
    0 Error(s)
```

可以通过指定 `/p:MetricsOutputFile=<filename>` 来替代输出文件名。 也可通过指定 `/p:LEGACY_CODE_METRICS_MODE=true` 来获取[旧式](#previous-versions)代码度量数据。 例如：

```shell
C:\source\repos\ClassLibrary3\ClassLibrary3>msbuild /t:Metrics /p:LEGACY_CODE_METRICS_MODE=true /p:MetricsOutputFile="Legacy.xml"
Microsoft (R) Build Engine version 16.0.360-preview+g9781d96883 for .NET Framework
Copyright (C) Microsoft Corporation. All rights reserved.

Build started 1/22/2019 4:31:00 PM.
The "MetricsOutputFile" property is a global property, and cannot be modified.
Project "C:\source\repos\ClassLibrary3\ClassLibrary3\ClassLibrary3.csproj" on node 1 (Metrics target(s))
.
Metrics:
  C:\source\repos\ClassLibrary3\packages\Microsoft.CodeMetrics.2.6.4-ci\build\\..\Metrics.Legacy\Metrics.Legacy.exe /project:C:\source\repos\ClassLibrary3\ClassLibrary3\ClassLibrary3.csproj /out:Legacy.xml
  Loading ClassLibrary3.csproj...
  Computing code metrics for ClassLibrary3.csproj...
  Writing output to 'Legacy.xml'...
  Completed Successfully.
Done Building Project "C:\source\repos\ClassLibrary3\ClassLibrary3\ClassLibrary3.csproj" (Metrics target(s)).

Build succeeded.
    0 Warning(s)
    0 Error(s)
```

### <a name="code-metrics-output"></a>代码度量输出

生成的 XML 输出采用以下格式：

::: moniker range=">=vs-2019"

```xml
<?xml version="1.0" encoding="utf-8"?>
<CodeMetricsReport Version="1.0">
  <Targets>
    <Target Name="ConsoleApp20.csproj">
      <Assembly Name="ConsoleApp20, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
        <Metrics>
          <Metric Name="MaintainabilityIndex" Value="100" />
          <Metric Name="CyclomaticComplexity" Value="1" />
          <Metric Name="ClassCoupling" Value="1" />
          <Metric Name="DepthOfInheritance" Value="1" />
          <Metric Name="SourceLines" Value="11" />
          <Metric Name="ExecutableLines" Value="1" />
        </Metrics>
        <Namespaces>
          <Namespace Name="ConsoleApp20">
            <Metrics>
              <Metric Name="MaintainabilityIndex" Value="100" />
              <Metric Name="CyclomaticComplexity" Value="1" />
              <Metric Name="ClassCoupling" Value="1" />
              <Metric Name="DepthOfInheritance" Value="1" />
              <Metric Name="SourceLines" Value="11" />
              <Metric Name="ExecutableLines" Value="1" />
            </Metrics>
            <Types>
              <NamedType Name="Program">
                <Metrics>
                  <Metric Name="MaintainabilityIndex" Value="100" />
                  <Metric Name="CyclomaticComplexity" Value="1" />
                  <Metric Name="ClassCoupling" Value="1" />
                  <Metric Name="DepthOfInheritance" Value="1" />
                  <Metric Name="SourceLines" Value="7" />
                  <Metric Name="ExecutableLines" Value="1" />
                </Metrics>
                <Members>
                  <Method Name="void Program.Main(string[] args)" File="C:\source\repos\ConsoleApp20\ConsoleApp20\Program.cs" Line="7">
                    <Metrics>
                      <Metric Name="MaintainabilityIndex" Value="100" />
                      <Metric Name="CyclomaticComplexity" Value="1" />
                      <Metric Name="ClassCoupling" Value="1" />
                      <Metric Name="SourceLines" Value="4" />
                      <Metric Name="ExecutableLines" Value="1" />
                    </Metrics>
                  </Method>
                </Members>
              </NamedType>
            </Types>
          </Namespace>
        </Namespaces>
      </Assembly>
    </Target>
  </Targets>
</CodeMetricsReport>
```

::: moniker-end
::: moniker range="vs-2017"

```xml
<?xml version="1.0" encoding="utf-8"?>
<CodeMetricsReport Version="1.0">
  <Targets>
    <Target Name="ConsoleApp20.csproj">
      <Assembly Name="ConsoleApp20, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
        <Metrics>
          <Metric Name="MaintainabilityIndex" Value="100" />
          <Metric Name="CyclomaticComplexity" Value="1" />
          <Metric Name="ClassCoupling" Value="1" />
          <Metric Name="DepthOfInheritance" Value="1" />
          <Metric Name="LinesOfCode" Value="11" />
        </Metrics>
        <Namespaces>
          <Namespace Name="ConsoleApp20">
            <Metrics>
              <Metric Name="MaintainabilityIndex" Value="100" />
              <Metric Name="CyclomaticComplexity" Value="1" />
              <Metric Name="ClassCoupling" Value="1" />
              <Metric Name="DepthOfInheritance" Value="1" />
              <Metric Name="LinesOfCode" Value="11" />
            </Metrics>
            <Types>
              <NamedType Name="Program">
                <Metrics>
                  <Metric Name="MaintainabilityIndex" Value="100" />
                  <Metric Name="CyclomaticComplexity" Value="1" />
                  <Metric Name="ClassCoupling" Value="1" />
                  <Metric Name="DepthOfInheritance" Value="1" />
                  <Metric Name="LinesOfCode" Value="7" />
                </Metrics>
                <Members>
                  <Method Name="void Program.Main(string[] args)" File="C:\source\repos\ConsoleApp20\ConsoleApp20\Program.cs" Line="7">
                    <Metrics>
                      <Metric Name="MaintainabilityIndex" Value="100" />
                      <Metric Name="CyclomaticComplexity" Value="1" />
                      <Metric Name="ClassCoupling" Value="1" />
                      <Metric Name="LinesOfCode" Value="4" />
                    </Metrics>
                  </Method>
                </Members>
              </NamedType>
            </Types>
          </Namespace>
        </Namespaces>
      </Assembly>
    </Target>
  </Targets>
</CodeMetricsReport>
```

::: moniker-end

### <a name="metricsexe"></a>Metrics.exe

如果不想安装 NuGet 包，可以直接生成和使用 Metrics.exe 可执行文件。 若要生成 Metrics.exe 可执行文件，请执行以下操作：

1. 克隆 [dotnet/roslyn-analyzers](https://github.com/dotnet/roslyn-analyzers) 存储库。
2. 以管理员身份打开 Visual Studio 的开发人员命令提示。
3. 从 roslyn-analyzers 存储库的根目录，执行以下命令：`Restore.cmd`
4. 将目录更改为 src\Tools\Metrics。
5. 若要生成 Metrics.csproj 项目，请执行以下命令：

   ```shell
   msbuild /m /v:m /p:Configuration=Release Metrics.csproj
   ```

   在存储库根目录下的 artifacts\bin 目录中生成名为 Metrics.exe 的可执行文件 。

#### <a name="metricsexe-usage"></a>Metrics.exe 用法

若要运行 Metrics.exe，请提供项目或解决方案以及输出 XML 文件作为参数。 例如：

```shell
C:\>Metrics.exe /project:ConsoleApp20.csproj /out:report.xml
Loading ConsoleApp20.csproj...
Computing code metrics for ConsoleApp20.csproj...
Writing output to 'report.xml'...
Completed Successfully.
```

#### <a name="legacy-mode"></a>旧模式

可选择在“旧模式”下生成 Metrics.exe 。 该工具的旧模式版本生成的度量值与[旧版工具生成的值](#previous-versions)更接近。 此外，在旧模式下，Metrics.exe 会为与该工具的早期版本为其生成代码度量的同一组方法类型生成代码度量。 例如，它不会为字段和属性初始值设定项生成代码度量数据。 对于后向兼容性或若有基于代码度量编号的代码签入入口，旧模式非常有用。 用于在旧模式下生成 Metrics.exe 的命令是：

```shell
msbuild /m /v:m /t:rebuild /p:LEGACY_CODE_METRICS_MODE=true Metrics.csproj
```

有关详细信息，请参阅[在旧模式下启用生成代码度量](https://github.com/dotnet/roslyn-analyzers/pull/1841)。

### <a name="previous-versions"></a>以前的版本

::: moniker range=">=vs-2019"
Visual Studio 2015 包含一个命令行代码度量工具，也称为 Metrics.exe。 该工具的早期版本进行了二进制分析，即基于程序集的分析。 较新版本的 Metrics.exe 工具将改为分析源代码。 由于较新的 Metrics.exe 工具基于源代码，因此命令行代码度量结果可能与 Visual Studio IDE 和早期版本的 Metrics.exe 生成的结果不同。 从 Visual Studio 2019 开始，Visual Studio IDE 像命令行工具一样分析源代码，结果应该是相同的。

::: moniker-end
::: moniker range="vs-2017"
Visual Studio 2015 包含一个命令行代码度量工具，也称为 Metrics.exe。 该工具的早期版本进行了二进制分析，即基于程序集的分析。 新的 Metrics.exe 工具改为分析源代码。 由于新的 Metrics.exe 工具基于源代码，因此命令行代码度量结果与 Visual Studio IDE 和早期版本的 Metrics.exe 生成的结果不同 。
::: moniker-end

新的命令行代码度量工具即使在存在源代码错误的情况下也能计算度量，只要可以加载解决方案和项目。

#### <a name="metric-value-differences"></a>度量值差异

::: moniker range=">=vs-2019"
从 Visual Studio 2019 版本 16.4 和 Microsoft.CodeAnalysis.Metics (2.9.5) 开始，`SourceLines` 和 `ExecutableLines` 将替换以前的 `LinesOfCode` 指标。 有关新指标的说明，请参阅[代码度量值](../code-quality/code-metrics-values.md)。 `LinesOfCode` 度量在旧模式下可用。
::: moniker-end
::: moniker range="vs-2017"
`LinesOfCode` 度量在新的命令行代码度量工具中更加准确且更可靠。 它独立于任何代码生成差异，并且不会在工具集或运行时发生更改时更改。 新工具将计算实际的代码行数，包括空行和注释。
::: moniker-end

其他指标（例如 `CyclomaticComplexity` 和 `MaintainabilityIndex`）使用与早期版本的 Metrics.exe 相同的公式，但新工具计算的是 `IOperations`（逻辑源指令）而不是中间语言 (IL) 说明的数量。 这些数字与 Visual Studio IDE 和早期版本的 Metrics.exe 生成的数字略有不同。

## <a name="see-also"></a>另请参阅

- [使用“代码度量结果”窗口](../code-quality/working-with-code-metrics-data.md)
- [代码度量值](../code-quality/code-metrics-values.md)
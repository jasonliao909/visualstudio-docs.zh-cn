---
title: 从 IDE 或命令行生成代码指标
ms.date: 11/02/2018
description: 了解如何在 Visual Studio 中生成代码指标数据。 请参阅如何使用解决方案资源管理器、规则集文件、命令行或菜单命令。
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
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601300"
---
# <a name="how-to-generate-code-metrics-data"></a>如何：生成代码指标数据

可以通过三种方式生成代码指标数据：

- 通过启用 [.NET 代码质量](#net-code-quality-analyzers-code-metrics-rules) 分析器并启用四个代码指标， (包含) 可维护性。

- 通过选择"[**分析**  >  **计算代码指标"菜单**](#calculate-code-metrics-menu-command)命令，Visual Studio。

- 从[C#](#command-line-code-metrics)和项目Visual Basic命令行。

## <a name="net-code-quality-analyzers-code-metrics-rules"></a>.NET 代码质量分析器代码指标规则

.NET 代码质量分析器包括多个代码指标 [分析器](roslyn-analyzers-overview.md) 规则：

- [CA1501](/dotnet/fundamentals/code-analysis/quality-rules/ca1501)
- [CA1502](/dotnet/fundamentals/code-analysis/quality-rules/ca1502)
- [CA1505](/dotnet/fundamentals/code-analysis/quality-rules/ca1505)
- [CA1506](/dotnet/fundamentals/code-analysis/quality-rules/ca1506)

这些规则默认处于禁用状态，但你可以从 解决方案资源管理器[EditorConfig](use-roslyn-analyzers.md#set-rule-severity-in-an-editorconfig-file)文件中启用它们。 [](use-roslyn-analyzers.md#set-rule-severity-from-solution-explorer) 例如，若要启用规则 CA1502 作为警告，EditorConfig 文件将包含以下条目：

```cs
dotnet_diagnostic.CA1502.severity = warning
```

### <a name="configuration"></a>配置

可以配置触发代码指标规则的阈值。

1. 创建文本文件。 例如，可以将它 *CodeMetricsConfig.txt。*

2. 将所需的阈值添加到文本文件中，格式如下：

   ```txt
   CA1502: 10
   ```

   本示例将规则 [CA1502](/dotnet/fundamentals/code-analysis/quality-rules/ca1502) 配置为在方法的循环复杂性大于 10 时执行。

3. 在 **文件的"** 属性Visual Studio或项目文件中，将配置文件的生成操作标记为 [**AdditionalFiles**](../ide/build-actions.md#build-action-values)。 例如：

   ```xml
   <ItemGroup>
     <AdditionalFiles Include="CodeMetricsConfig.txt" />
   </ItemGroup>
   ```

## <a name="calculate-code-metrics-menu-command"></a>"计算代码指标"菜单命令

使用"分析计算代码指标"菜单为 IDE 中的一个或所有打开的项目  >  **生成代码** 指标。

### <a name="generate-code-metrics-results-for-an-entire-solution"></a>生成整个解决方案的代码指标结果

可以通过以下任一方式为整个解决方案生成代码指标结果：

- 在菜单栏中，选择 **"分析**  >  **""计算解决方案**  >  **的代码指标"。**

- 在 **解决方案资源管理器** 中，右键单击解决方案，然后选择"**计算代码指标"。**

- 在" **代码指标结果"窗口中** ，选择"计算解决方案 **的代码指标"** 按钮。

将生成结果并显示" **代码指标结果** "窗口。 若要查看结果详细信息，请展开"层次结构" **列中的** 树。

### <a name="generate-code-metrics-results-for-one-or-more-projects"></a>为一个或多个项目生成代码指标结果

1. 在 **解决方案资源管理器** 中，选择一个或多个项目。

1. 在菜单栏中，选择"**分析** 所选代码的计算代码  >    >  **Project () "。**

将生成结果并显示" **代码指标结果** "窗口。 若要查看结果详细信息，请展开"层次结构"中的 **树**。

::: moniker range="vs-2017"

> [!NOTE]
> " **计算代码指标** "命令对 .NET Core 和 .NET Standard不起作用。 若要计算 .NET Core 或 .NET Standard 的代码指标，可以：
>
> - 改为从命令行 [计算代码](#command-line-code-metrics) 指标
>
> - 升级到 Visual Studio [2019](https://visualstudio.microsoft.com/downloads)

::: moniker-end

## <a name="command-line-code-metrics"></a>命令行代码指标

可以从 C# 命令行生成代码指标数据，Visual Basic、.NET Core 和 .NET Framework 应用生成.NET Standard数据。 若要从命令行运行代码指标，请安装[Microsoft.CodeAnalysis.Metrics](#microsoftcodeanalysismetrics-nuget-package) NuGet包或自行[Metrics.exe可执行文件](#metricsexe)。

### <a name="microsoftcodeanalysismetrics-nuget-package"></a>Microsoft.CodeAnalysis.Metrics NuGet包

从命令行生成代码指标数据的最简单方法是安装[Microsoft.CodeAnalysis.Metrics](https://www.nuget.org/packages/Microsoft.CodeAnalysis.Metrics/) NuGet包。 安装包后，从包含项目文件的目录中 `msbuild /t:Metrics` 运行 。 例如：

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

可以通过指定 来替代输出文件名 `/p:MetricsOutputFile=<filename>` 。 还可通过指定 [获取](#previous-versions) 旧式代码指标数据 `/p:LEGACY_CODE_METRICS_MODE=true` 。 例如：

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

### <a name="code-metrics-output"></a>代码指标输出

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

如果不想安装 NuGet 包，可以直接生成并使用Metrics.exe可执行文件。  若要 *生成Metrics.exe可执行* 文件：

1. 克隆 [dotnet/roslyn-analyzers](https://github.com/dotnet/roslyn-analyzers) 存储库。
2. 以开发人员命令提示Visual Studio打开"用户"。
3. 从 **roslyn-analyzers** 存储库的根目录下，执行以下命令： `Restore.cmd`
4. 将目录更改为 *src\Tools\Metrics*。
5. 执行以下命令以生成 **Metrics.csproj** 项目：

   ```shell
   msbuild /m /v:m /p:Configuration=Release Metrics.csproj
   ```

   在存储库 *根Metrics.exe* *artifacts\bin* 目录中生成名为Metrics.exe的可执行文件。

#### <a name="metricsexe-usage"></a>Metrics.exe使用情况

若要运行 *Metrics.exe，* 请提供项目或解决方案以及输出 XML 文件作为参数。 例如：

```shell
C:\>Metrics.exe /project:ConsoleApp20.csproj /out:report.xml
Loading ConsoleApp20.csproj...
Computing code metrics for ConsoleApp20.csproj...
Writing output to 'report.xml'...
Completed Successfully.
```

#### <a name="legacy-mode"></a>旧模式

可以选择在旧模式下 *Metrics.exe**生成应用程序*。 该工具的旧模式版本生成指标值，这些值与工具生成的较旧版本 [更接近](#previous-versions)。 此外，在旧 *模式下，Metrics.exe* 为以前版本的工具生成代码指标的同一组方法类型生成代码指标。 例如，它不会为字段和属性初始值设置器生成代码指标数据。 如果具有基于代码指标编号的代码签入入口，则旧模式对于向后兼容性非常有用。 在旧模式下生成 *Metrics.exe* 的命令为：

```shell
msbuild /m /v:m /t:rebuild /p:LEGACY_CODE_METRICS_MODE=true Metrics.csproj
```

有关详细信息，请参阅 [启用在旧模式下生成代码指标](https://github.com/dotnet/roslyn-analyzers/pull/1841)。

### <a name="previous-versions"></a>旧版

::: moniker range=">=vs-2019"
Visual Studio 2015 年包含一个命令行代码指标工具，该工具也称为 *Metrics.exe。* 此早期版本的工具执行二进制分析，即基于程序集的分析。 较新版本的 *Metrics.exe* 工具改为分析源代码。 由于较新的 *Metrics.exe* 工具基于源代码，因此命令行代码指标结果可能不同于 Visual Studio IDE 和早期版本的Metrics.exe生成 *的结果*。 从 2019 Visual Studio开始，Visual Studio IDE 会分析命令行工具等源代码，结果应相同。

::: moniker-end
::: moniker range="vs-2017"
Visual Studio 2015 年包含一个命令行代码指标工具，该工具也称为 *Metrics.exe。* 此早期版本的工具执行二进制分析，即基于程序集的分析。 新的 *Metrics.exe* 工具将改为分析源代码。 由于新的 *Metrics.exe* 工具基于源代码，因此命令行代码指标结果不同于 Visual Studio IDE 和早期版本的 *Metrics.exe。*
::: moniker-end

新的命令行代码指标工具即使在出现源代码错误时也计算指标，只要可以加载解决方案和项目。

#### <a name="metric-value-differences"></a>指标值差异

::: moniker range=">=vs-2019"
从 Visual Studio 2019 版本 16.4 和 Microsoft.CodeAnalysis.Metics (2.9.5) 开始，并替换 `SourceLines` `ExecutableLines` 以前的指标 `LinesOfCode` 。 有关新指标的说明，请参阅 [代码指标值](../code-quality/code-metrics-values.md)。 指标 `LinesOfCode` 在旧模式下可用。
::: moniker-end
::: moniker range="vs-2017"
该 `LinesOfCode` 指标在新的命令行代码指标工具中更加准确可靠。 它独立于任何 codegen 差异，在工具集或运行时更改时不会更改。 新工具对实际代码行（包括空白行和注释）进行计数。
::: moniker-end

其他指标（如 和 ）使用与以前版本的Metrics.exe相同的公式，但新工具将计算 (逻辑源指令数) 而不是中间语言 `CyclomaticComplexity` `MaintainabilityIndex` (IL)  `IOperations` 指令。 这些数字与 IDE 和早期版本的 Visual Studio 生成的数字略有不同 *Metrics.exe。*

## <a name="see-also"></a>另请参阅

- [使用"代码指标结果"窗口](../code-quality/working-with-code-metrics-data.md)
- [代码指标值](../code-quality/code-metrics-values.md)
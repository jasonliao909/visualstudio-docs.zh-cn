---
title: 使用 .runsettings 文件配置单元测试
description: 了解如何使用 Visual Studio 中的 .runsettings 文件配置命令行、IDE 或生成工作流运行的单元测试。
ms.custom: SEO-VS-2020
ms.date: 12/06/2021
ms.topic: conceptual
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-test
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: 5bc7610a65b2bc5b8f7194781fd05c04a26f0cb2
ms.sourcegitcommit: 965372ad0d75f015403c1af508080bf799914ce3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2022
ms.locfileid: "135805346"
---
# <a name="configure-unit-tests-by-using-a-runsettings-file"></a>使用 .runsettings 文件配置单元测试

通过使用 .runsettings 文件，可配置 Visual Studio 中的单元测试。 例如，可更改正在运行测试的 .NET 版本、测试结果的目录，或者在测试运行期间收集的数据。 .runsettings 文件常见的用途是自定义[代码覆盖率分析](../test/customizing-code-coverage-analysis.md)。

可以使用运行设置文件配置测试，这些测试可以从[命令行](vstest-console-options.md)IDE 运行，或者在使用 Azure Test Plans 或 Team Foundation Server (TFS) 的[生成工作流](/azure/devops/pipelines/test/getting-started-with-continuous-testing?view=vsts&preserve-view=true)中运行。

运行设置文件是可选的。 如果不需要执行任何特殊配置，则无需 .runsettings 文件。

## <a name="create-a-run-settings-file-and-customize-it"></a>创建一个运行设置文件并对其进行自定义

1. 将运行设置文件添加到解决方案中。 在“解决方案资源管理器”的解决方案快捷菜单上，依次选择“添加” > “新建项”和“XML 文件”   。 保存带有类似于 test.runsettings 的名称的文件。

   > [!TIP]
   > 只要使用扩展名 .runsettings，文件名就无关紧要。

2. 添加[示例 *.runsettings 文件](#example-runsettings-file)中的内容，然后按需要进行自定义，如以下章节所述。

3. 使用以下某个方法指定要使用的 *.runsettings 文件：

   - [Visual Studio IDE](#specify-a-run-settings-file-in-the-ide)
   - [命令行](#specify-a-run-settings-file-from-the-command-line)
   - 使用 Azure Test Plans 或 Team Foundation Server (TFS) [生成工作流](/azure/devops/pipelines/test/getting-started-with-continuous-testing?view=vsts&preserve-view=true)。

4. 运行单元测试以使用自定义运行设置。

::: moniker range="vs-2017"

若要禁用和启用 IDE 中的自定义设置，请依次选择“测试”>“测试设置”菜单，然后取消选择或选择文件 。

![Visual Studio 2017 中包含自定义设置文件的测试设置菜单](../test/media/codecoverage-settingsfile.png)

::: moniker-end

::: moniker range=">=vs-2019"

若要禁用和启用 IDE 中的自定义设置，请在“测试”菜单中取消选择或选择文件。

::: moniker-end

> [!TIP]
> 可以在解决方案中创建多个 .runsettings 文件，然后按需选择一个作为活动测试设置文件。

## <a name="specify-a-run-settings-file-in-the-ide"></a>在 IDE 中指定运行设置文件

可用的方法取决于 Visual Studio 的版本。

::: moniker range="vs-2017"
若要在 IDE 中指定一个运行设置文件，请选择“测试”>“测试设置”>“选择测试设置文件”，然后选择 .runsettings 文件。

![在 Visual Studio 2017 中选择测试设置文件菜单](media/select-test-settings-file.png)

该文件将显示在“测试设置”菜单上，你可以选择或取消选择它。 选择后，每当选择“分析代码覆盖率”时，都会应用运行设置文件。
::: moniker-end

::: moniker range=">=vs-2019"

### <a name="visual-studio-2019-version-164-and-later"></a>Visual Studio 2019 版本 16.4 及更高版本

在 Visual Studio 2019 版本 16.4 及更高版本中，指定运行设置文件的方法有三种。

- [自动检测运行设置](#autodetect-the-run-settings-file)
- [手动设置运行设置](#manually-select-the-run-settings-file)
- [设置生成属性](#set-a-build-property)

#### <a name="autodetect-the-run-settings-file"></a>自动检测运行设置文件

> [!NOTE]
> 这仅适用于名为 `.runsettings` 的文件。

若要自动检测运行设置文件，请将其放在解决方案的根目录下。

如果启用了自动检测运行设置文件，则此文件中的设置将应用到所有测试运行。 可使用两种方法打开 runsettings 文件自动检测：

- 选择“工具”>“选项”>“测试”>“自动检测 runsettings 文件”   

   ![Visual Studio 中的自动检测 .runsettings 文件选项](media/auto-detect-runsettings-tools-window.png)

- 选择“测试”>“配置运行设置”>“自动检测 runsettings 文件”  

   ![Visual Studio 中的 "自动检测 .runsettings 文件" 菜单](media/auto-detect-runsettings-menu.png)

#### <a name="manually-select-the-run-settings-file"></a>手动选择运行设置文件

在 IDE 中，选择“测试”>“配置运行设置”>“选择解决方案范围的 runsettings 文件”，然后选择 .runsettings 文件。

- 此文件替代解决方案根目录下的 .runsettings 文件（如果存在），并应用于所有测试运行。
- 此文件选择仅在本地保留。

![在 Visual Studio 中选择 "测试解决方案范围内的 .runsettings 文件" 菜单](media/select-solution-settings-file.png)

#### <a name="set-a-build-property"></a>设置生成属性

通过项目文件或 Directory.Build.props 文件将生成属性添加到项目。 项目的运行设置文件由 RunSettingsFilePath 属性指定。

- 当前 C#、VB、C++ 和 F# 项目中支持项目级运行设置。
- 为项目指定的文件将替代解决方案中指定的任何其他运行设置文件。
- [这些 MSBuild 属性](../msbuild/msbuild-reserved-and-well-known-properties.md) 可用于指定 runsettings 文件的路径。

指定项目的 .runsettings 文件示例：

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <RunSettingsFilePath>$(MSBuildProjectDirectory)\example.runsettings</RunSettingsFilePath>
  </PropertyGroup>
  ...
</Project>
```

### <a name="visual-studio-2019-version-163-and-earlier"></a>Visual Studio 2019 版本 16.3 及更早版本

若要在 IDE 中指定运行设置文件，请选择“测试” > “选择设置文件”。 浏览到并选择 .runsettings 文件。

![在 Visual Studio 2019 中选择测试设置文件菜单](media/vs-2019/select-settings-file.png)

该文件将显示在“测试”菜单上，你可以选择或取消选择它。 选择后，每当选择“分析代码覆盖率”时，都会应用运行设置文件。
::: moniker-end

## <a name="specify-a-run-settings-file-from-the-command-line"></a>从命令行指定运行设置文件

若要从命令行运行测试，请使用 vstest.console.exe 并使用 /Settings 参数指定设置文件。

1. 打开 [Visual Studio 的开发人员命令提示](../ide/reference/command-prompt-powershell.md)。

2. 输入类似的命令：

   ```cmd
   vstest.console.exe MyTestAssembly.dll /EnableCodeCoverage /Settings:CodeCoverage.runsettings
   ```

   or

   ```cmd
   vstest.console.exe --settings:test.runsettings test.dll
   ```

有关详细信息，请参阅 [VSTest.Console.exe 命令行选项](vstest-console-options.md)。

## <a name="the-runsettings-file"></a>*.runsettings 文件

*.runsettings 文件是一个 XML 文件，其中的 RunSettings 元素中包含各种配置元素。 以下各节详细介绍了不同元素。 有关完整示例，请参阅[示例 *.runsettings 文件](#example-runsettings-file)。

```xml
<?xml version="1.0" encoding="utf-8"?>
<RunSettings>
  <!-- configuration elements -->
</RunSettings>
```

每个配置元素都是可选的，因为它有默认值。

## <a name="runconfiguration-element"></a>RunConfiguration 元素

```xml
<RunConfiguration>
    <MaxCpuCount>1</MaxCpuCount>
    <ResultsDirectory>.\TestResults</ResultsDirectory>
    <TargetPlatform>x86</TargetPlatform>
    <TargetFrameworkVersion>Framework40</TargetFrameworkVersion>
    <TestAdaptersPaths>%SystemDrive%\Temp\foo;%SystemDrive%\Temp\bar</TestAdaptersPaths>
    <TestSessionTimeout>10000</TestSessionTimeout>
    <TreatNoTestsAsError>true</TreatNoTestsAsError>
</RunConfiguration>
```

RunConfiguration 元素可以包含下列元素：

|节点|默认|值|
|-|-|-|
|**MaxCpuCount**|1|此设置利用计算机上的可用内核，在运行单元测试时控制并行测试执行的程度。 测试执行引擎在每个可用内核上作为单独的进程启动，并为每个内核提供包含要运行的测试的容器。 容器可以是程序集、DLL 或相关项目。 测试容器即计划单位。 在每个容器中，测试将根据测试框架进行执行。 如果存在多个容器，进程在容器内完成测试执行时，系统会向它们提供下一个可用容器。<br /><br />MaxCpuCount 可以是：<br /><br />n，其中 1 <= n <= 内核数：最多启动 n 个进程<br /><br />n，其中 n = 任何其他值：启动的进程数最多可达可用内核数。 例如，设置 n = 0 可使平台根据环境自动决定要启动的最佳进程数。|
|**ResultsDirectory**||在其中放置测试结果的目录。 该路径相对于包含 .runsettings 文件的目录。|
|**TargetFrameworkVersion**|Framework40|适用于 .NET Core 源的 `FrameworkCore10`、适用于基于 UWP 源的 `FrameworkUap10`、适用于 .NET Framework 4.5 及更高版本的 `Framework45`、适用于 .NET Framework 4.0 的 `Framework40` 以及适用于 .NET Framework 3.5 的 `Framework35`。<br /><br />此设置指定使用哪一版本的单元测试框架来查找并执行测试。 它可能与你在单元测试项目的生成属性中指定的 .NET 平台的版本不同。<br /><br />如果省略 .runsettings 文件中的 `TargetFrameworkVersion` 元素，平台会基于生成的二进制文件自动确定框架版本。|
|**TargetPlatform**|x86|x86、x64|
|**TreatTestAdapterErrorsAsWarnings**|false|false、true|
|**TestAdaptersPaths**||TestAdapters 所在目录的一个或多个路径|
|**TestSessionTimeout**||当测试会话超过给定时间，允许用户终止测试会话。 设置超时可确保资源被充分利用，并且测试会话被限制在一个设定时间内。 Visual Studio 2017 版本 15.5 及更高版本中提供了此设置。|
|**DotnetHostPath**||指定用于运行测试主机的 dotnet 主机的自定义路径。 这在生成自己的 dotnet 时非常有用，例如在生成 dotnet/运行时存储库时。 指定此选项将跳过查找 testhost.exe，并将始终使用 testhost.dll。|
|TreatNoTestsAsError|false| true 或 false <br>指定一个布尔值，它定义在未发现测试时的退出代码。 如果该值为 `true` 并且未发现测试，则返回非零退出代码。 否则返回零。|

## <a name="datacollectors-element-diagnostic-data-adapters"></a>DataCollectors 元素（诊断数据适配器）

DataCollectors 元素指定诊断数据适配器的设置。 诊断数据适配器收集有关测试环境和受测的应用程序的其他信息。 每个适配器都具有默认设置，因此如果不希望使用默认值，只需提供设置。

```xml
<DataCollectionRunSettings>
  <DataCollectors>
    <!-- data collectors -->
  </DataCollectors>
</DataCollectionRunSettings>
```

### <a name="codecoverage-data-collector"></a>CodeCoverage 数据收集器

代码覆盖率数据收集器创建应用程序代码的哪些部分已在测试中执行过的日志。 有关自定义代码覆盖率设置的详细信息，请参阅[自定义代码覆盖率分析](../test/customizing-code-coverage-analysis.md)。

```xml
<DataCollector friendlyName="Code Coverage" uri="datacollector://Microsoft/CodeCoverage/2.0" assemblyQualifiedName="Microsoft.VisualStudio.Coverage.DynamicCoverageDataCollector, Microsoft.VisualStudio.TraceCollector, Version=11.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a">
  <Configuration>
    <CodeCoverage>
      <ModulePaths>
        <Exclude>
          <ModulePath>.*CPPUnitTestFramework.*</ModulePath>
        </Exclude>
      </ModulePaths>

      <UseVerifiableInstrumentation>True</UseVerifiableInstrumentation>
      <AllowLowIntegrityProcesses>True</AllowLowIntegrityProcesses>
      <CollectFromChildProcesses>True</CollectFromChildProcesses>
      <CollectAspDotNet>False</CollectAspDotNet>
    </CodeCoverage>
  </Configuration>
</DataCollector>
```

### <a name="videorecorder-data-collector"></a>VideoRecorder 数据收集器

视频数据收集器在运行测试时捕获屏幕录制。 此录制可用于对 UI 测试进行故障排除+。 视频数据收集器在 Visual Studio 2017 版本 15.5 及更高版本中可用。 有关配置此数据收集器的示例，请参阅[示例 *.runsettings 文件](#example-runsettings-file)。

若要自定义任何其他类型的诊断数据适配器，请使用[测试设置文件](../test/collect-diagnostic-information-using-test-settings.md)。

### <a name="blame-data-collector"></a>意见数据收集器

此选项可帮助你隔离导致测试主机崩溃的有问题的测试。 运行此收集器会在 TestResults 中创建一个输出文件 (Sequence.xml)，该文件在主机崩溃之前会捕获执行测试的顺序 。

```xml
<DataCollector friendlyName="blame" enabled="True">
</DataCollector>
```

## <a name="testrunparameters"></a>TestRunParameters

```xml
<TestRunParameters>
    <Parameter name="webAppUrl" value="http://localhost" />
    <Parameter name="docsUrl" value="https://docs.microsoft.com" />
</TestRunParameters>
```

测试运行参数提供了一种可用于运行时测试的定义变量和值的方法。 使用 MSTest <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestContext.Properties%2A?displayProperty=nameWithType> 属性（或 NUnit [TestContext](https://docs.nunit.org/articles/nunit/writing-tests/TestContext.html)）访问参数：

```csharp
private string _appUrl;
public TestContext TestContext { get; set; }

[TestMethod] // [Test] for NUnit
public void HomePageTest()
{
    string _appURL = TestContext.Properties["webAppUrl"];
}
```

若要使用测试运行参数，请将公共 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestContext> 属性添加到测试类。

## <a name="loggerrunsettings-element"></a>LoggerRunSettings 元素

`LoggerRunSettings` 部分定义要用于测试运行的一个或多个记录器。 最常见的记录器为控制台、Visual Studio 测试结果文件 (trx)和 html。

```xml
<LoggerRunSettings>
    <Loggers>
      <Logger friendlyName="console" enabled="True">
        <Configuration>
            <Verbosity>quiet</Verbosity>
        </Configuration>
      </Logger>
      <Logger friendlyName="trx" enabled="True">
        <Configuration>
          <LogFileName>foo.trx</LogFileName>
        </Configuration>
      </Logger>
      <Logger friendlyName="html" enabled="True">
        <Configuration>
          <LogFileName>foo.html</LogFileName>
        </Configuration>
      </Logger>
    </Loggers>
  </LoggerRunSettings>
```

## <a name="mstest-element"></a>MSTest 元素

这些设置特定于运行具有 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestMethodAttribute> 特性的测试方法的测试适配器。

```xml
<MSTest>
    <MapInconclusiveToFailed>True</MapInconclusiveToFailed>
    <CaptureTraceOutput>false</CaptureTraceOutput>
    <DeleteDeploymentDirectoryAfterTestRunIsComplete>False</DeleteDeploymentDirectoryAfterTestRunIsComplete>
    <DeploymentEnabled>False</DeploymentEnabled>
    <AssemblyResolution>
      <Directory path="D:\myfolder\bin\" includeSubDirectories="false"/>
    </AssemblyResolution>
</MSTest>
```

|Configuration|默认|值|
|-|-|-|
|**ForcedLegacyMode**|false|在 Visual Studio 2012 中，对 MSTest 适配器进行了优化，使其变得更快且更具可伸缩性。 某些行为（如测试的运行顺序）可能不与 Visual Studio 早期版本中的完全一致。 将此值设置为 true 可使用旧测试适配器。<br /><br />例如，如果为单元测试指定 app.config 文件，可能会用到此设置。<br /><br />我们建议你考虑重构测试以便可以使用较新的适配器。|
|**IgnoreTestImpact**|false|当在 MSTest 中或从 Microsoft 测试管理器（在 Visual Studio 2017 中已弃用）运行时，测试影响功能会按这些测试受最新更改影响的程度对它们进行优先级排序。 此设置会停用该功能。 有关详细信息，请参阅[自上一个生成后应运行哪些测试？](/previous-versions/dd286589(v=vs.140))。|
|**SettingsFile**||你可以指定测试设置文件以便与此处的 MSTest 适配器配合使用。 还可以[从设置菜单](#specify-a-run-settings-file-in-the-ide)指定测试设置文件。<br /><br />如果指定此值，则还必须将 **ForcedLegacyMode** 设置为 **true**。<br /><br />`<ForcedLegacyMode>true</ForcedLegacyMode>`|
|**KeepExecutorAliveAfterLegacyRun**|false|测试运行完成后，MSTest 将关闭。 测试中启动的任何进程也将终止。 如果希望测试执行程序保持活动状态，请将此值设为 true。 例如，可使用此设置让浏览器保持在编码的 UI 测试之间运行。|
|**DeploymentEnabled**|true|如果将此值设置为 false，则不会将已在测试方法中指定的部署项目复制到部署目录中。|
|**CaptureTraceOutput**|true|你可以使用 <xref:System.Diagnostics.Trace.WriteLine%2A?displayProperty=nameWithType> 从测试方法写入调试跟踪。|
|**DeleteDeploymentDirectoryAfterTestRunIsComplete**|true|若要在测试运行后保留部署目录，请将此值设置为 false。|
|**MapInconclusiveToFailed**|false|如果测试完成返回无结论的状态，则会映射到“测试资源管理器”中的已跳过状态。 如果希望无结论的测试显示为失败，请将此值设为 true。|
|**InProcMode**|false|如果希望测试在与 MSTest 适配器相同的进程中运行，请将此值设置为 true。 此设置将提供较小的性能提升。 但是，如果测试存在异常，则剩余测试不会运行。|
|**AssemblyResolution**|false|查找和执行单元测试时，可以指定其他程序集的路径。 例如，对与测试程序集位于不同目录中的依赖程序集使用这些路径。 若要指定路径，请使用“Directory Path”元素。 路径可以包括环境变量。<br /><br />`<AssemblyResolution>  <Directory path="D:\myfolder\bin\" includeSubDirectories="false"/> </AssemblyResolution>`|

## <a name="example-runsettings-file"></a>.runsettings 文件示例

以下 XML 显示典型 .runsettings 文件的内容。 复制此代码并对其进行编辑以满足需求。

文件的每个元素都是可选的，因为它有默认值。

```xml
<?xml version="1.0" encoding="utf-8"?>
<RunSettings>
  <!-- Configurations that affect the Test Framework -->
  <RunConfiguration>
    <MaxCpuCount>1</MaxCpuCount>
    <!-- Path relative to directory that contains .runsettings file-->
    <ResultsDirectory>.\TestResults</ResultsDirectory>

    <!-- x86 or x64 -->
    <!-- You can also change it from the Test menu; choose "Processor Architecture for AnyCPU Projects" -->
    <TargetPlatform>x86</TargetPlatform>

    <!-- Framework35 | [Framework40] | Framework45 -->
    <TargetFrameworkVersion>Framework40</TargetFrameworkVersion>

    <!-- Path to Test Adapters -->
    <TestAdaptersPaths>%SystemDrive%\Temp\foo;%SystemDrive%\Temp\bar</TestAdaptersPaths>

    <!-- TestSessionTimeout was introduced in Visual Studio 2017 version 15.5 -->
    <!-- Specify timeout in milliseconds. A valid value should be greater than 0 -->
    <TestSessionTimeout>10000</TestSessionTimeout>

    <!-- true or false -->
    <!-- Value that specifies the exit code when no tests are discovered -->
    <TreatNoTestsAsError>true</TreatNoTestsAsError>
  </RunConfiguration>

  <!-- Configurations for data collectors -->
  <DataCollectionRunSettings>
    <DataCollectors>
      <DataCollector friendlyName="Code Coverage" uri="datacollector://Microsoft/CodeCoverage/2.0" assemblyQualifiedName="Microsoft.VisualStudio.Coverage.DynamicCoverageDataCollector, Microsoft.VisualStudio.TraceCollector, Version=11.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a">
        <Configuration>
          <CodeCoverage>
            <ModulePaths>
              <Exclude>
                <ModulePath>.*CPPUnitTestFramework.*</ModulePath>
              </Exclude>
            </ModulePaths>

            <!-- We recommend you do not change the following values: -->
            <UseVerifiableInstrumentation>True</UseVerifiableInstrumentation>
            <AllowLowIntegrityProcesses>True</AllowLowIntegrityProcesses>
            <CollectFromChildProcesses>True</CollectFromChildProcesses>
            <CollectAspDotNet>False</CollectAspDotNet>

          </CodeCoverage>
        </Configuration>
      </DataCollector>

      <DataCollector uri="datacollector://microsoft/VideoRecorder/1.0" assemblyQualifiedName="Microsoft.VisualStudio.TestTools.DataCollection.VideoRecorder.VideoRecorderDataCollector, Microsoft.VisualStudio.TestTools.DataCollection.VideoRecorder, Version=15.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a" friendlyName="Screen and Voice Recorder">
        <!--Video data collector was introduced in Visual Studio 2017 version 15.5 -->
        <Configuration>
          <!-- Set "sendRecordedMediaForPassedTestCase" to "false" to add video attachments to failed tests only -->
          <MediaRecorder sendRecordedMediaForPassedTestCase="true"  xmlns="">           
            <ScreenCaptureVideo bitRate="512" frameRate="2" quality="20" />
          </MediaRecorder>
        </Configuration>
      </DataCollector>

      <!-- Configuration for blame data collector -->
      <DataCollector friendlyName="blame" enabled="True">
      </DataCollector>

    </DataCollectors>
  </DataCollectionRunSettings>

  <!-- Parameters used by tests at run time -->
  <TestRunParameters>
    <Parameter name="webAppUrl" value="http://localhost" />
    <Parameter name="webAppUserName" value="Admin" />
    <Parameter name="webAppPassword" value="Password" />
  </TestRunParameters>

  <!-- Configuration for loggers -->
  <LoggerRunSettings>
    <Loggers>
      <Logger friendlyName="console" enabled="True">
        <Configuration>
            <Verbosity>quiet</Verbosity>
        </Configuration>
      </Logger>
      <Logger friendlyName="trx" enabled="True">
        <Configuration>
          <LogFileName>foo.trx</LogFileName>
        </Configuration>
      </Logger>
      <Logger friendlyName="html" enabled="True">
        <Configuration>
          <LogFileName>foo.html</LogFileName>
        </Configuration>
      </Logger>
      <Logger friendlyName="blame" enabled="True" />
    </Loggers>
  </LoggerRunSettings>

  <!-- Adapter Specific sections -->

  <!-- MSTest adapter -->
  <MSTest>
    <MapInconclusiveToFailed>True</MapInconclusiveToFailed>
    <CaptureTraceOutput>false</CaptureTraceOutput>
    <DeleteDeploymentDirectoryAfterTestRunIsComplete>False</DeleteDeploymentDirectoryAfterTestRunIsComplete>
    <DeploymentEnabled>False</DeploymentEnabled>
    <AssemblyResolution>
      <Directory path="D:\myfolder\bin\" includeSubDirectories="false"/>
    </AssemblyResolution>
  </MSTest>

</RunSettings>
```

## <a name="specify-environment-variables-in-the-runsettings-file"></a>在 .runsettings 文件中指定环境变量

可以在 .runsettings 文件中设置环境变量，该文件可直接与测试主机交互。 有必要在 .runsettings 文件中指定环境变量，以便支持需要设置环境变量（例如 DOTNET_ROOT）的重要项目 。 这些变量是在生成测试主机进程时设置的，它们在主机中可用。

### <a name="example"></a>示例

下面的代码是传递环境变量的示例 .runsettings 文件：

```xml
<?xml version="1.0" encoding="utf-8"?>
<!-- File name extension must be .runsettings -->
<RunSettings>
  <RunConfiguration>
    <EnvironmentVariables>
      <!-- List of environment variables we want to set-->
      <DOTNET_ROOT>C:\ProgramFiles\dotnet</DOTNET_ROOT>
      <SDK_PATH>C:\Codebase\Sdk</SDK_PATH>
    </EnvironmentVariables>
  </RunConfiguration>
</RunSettings>
```

RunConfiguration 节点应包含 EnvironmentVariables 节点 。 可以将环境变量指定为元素名称及其值。

> [!NOTE]
> 由于应始终在启动测试主机时设置这些环境变量，因此测试应始终在单独的进程中运行。 为此，将在存在环境变量时设置 /InIsolation 标记，以便始终调用测试主机。

## <a name="see-also"></a>请参阅

- [配置测试运行](https://github.com/microsoft/vstest-docs/blob/master/docs/configure.md)
- [自定义代码覆盖率分析](../test/customizing-code-coverage-analysis.md)
- [Visual Studio 测试任务 (Azure Test Plans)](/azure/devops/pipelines/tasks/test/vstest?view=vsts&preserve-view=true)

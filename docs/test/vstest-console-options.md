---
title: VSTest.Console.exe 命令行选项
description: 了解用于运行测试的 VSTest.Console.exe 命令行工具。 本文涵盖了常规命令行选项。
ms.custom: SEO-VS-2020
ms.date: 03/11/2022
ms.topic: reference
helpviewer_keywords:
- vstest.console.exe
- command-line tests
ms.author: mikejo
author: mikejo5000
manager: jmartens
ms.technology: vs-ide-test
ms.workload:
- multiple
ms.openlocfilehash: 9a1d096b691cffc83a21c473d76b9fa7e6dc4b3e
ms.sourcegitcommit: 596b3ec674f5848fe0711da5ccc23c01b58e508c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/12/2022
ms.locfileid: "139793178"
---
# <a name="vstestconsoleexe-command-line-options"></a>VSTest.Console.exe 命令行选项

VSTest.Console.exe 是用于运行测试的命令行工具。 可在命令行上按任意顺序指定多个选项。 这些选项在[常规命令行选项](#general-command-line-options)中列出。

> [!NOTE]
> Visual Studio 中的 MSTest 适配器在旧模式下仍有效（等效于使用 mstest.exe 运行测试），可实现兼容性。 在旧模式下，它无法利用 TestCaseFilter 功能。 在以下情况下，适配器可以切换到旧模式：指定 .testsettings 文件、在 .runsettings 文件中将 forcelegacymode 设置为 true 或使用 HostType 等特性 。
>
> 若要在基于 ARM 架构的计算机上运行自动测试，则必须使用 VSTest.Console.exe。

打开[开发人员命令提示](../ide/reference/command-prompt-powershell.md)以使用命令行工具，或者可在 %Program Files(x86)%\Microsoft Visual Studio\\<version\>\\<edition\>\common7\ide\CommonExtensions\\<Platform | Microsoft> 中找到该工具。

## <a name="general-command-line-options"></a>常规命令行选项

下表列出了 VSTest.Console.exe 的所有选项以及对应的简短说明。 在命令行上键入 `VSTest.Console/?` 可以看到类似的摘要。

| 选项 | 描述 |
|---|---|
|**[测试文件]**|从指定文件运行测试。 用空格分隔多个测试文件名。<br />示例：`mytestproject.dll`、`mytestproject.dll myothertestproject.exe`|
|**/Settings:[文件名]**|使用其他设置（如数据收集器）运行测试。 有关详细信息，请参阅[使用 .runsettings 文件配置单元测试](../test/configure-unit-tests-by-using-a-dot-runsettings-file.md)<br />示例：`/Settings:local.runsettings`|
|**/Tests:[测试名]**|运行其名称包含提供的值的测试。 若要提供多个值，请使用逗号将这些值分隔。<br />示例：`/Tests:TestMethod1,testMethod2`<br />/Tests 命令行选项不能与 /TestCaseFilter 命令行选项一起使用 。|
|**/Parallel**|指定并行执行的测试。 默认情况下，最多可使用计算机上的所有可用内核。 可在设置文件中配置要使用的内核数。|
|**/Enablecodecoverage**|在测试运行中启用数据诊断适配器 CodeCoverage。<br />如果未使用设置文件指定设置，则将使用默认设置。|
|**/InIsolation**|在隔离的进程中运行测试。<br />这种隔离使 vstest.console.exe 进程不太可能在测试出错时停止，但测试的运行速度可能较慢。|
|**/UseVsixExtensions**|此选项使 vstest.console.exe 进程使用或跳过在测试运行中安装的 VSIX 扩展（如果有）。<br />此选项已弃用。 从 Visual Studio 的下一个主版本开始，此选项可能会删除。 转为作为 NuGet 包提供的使用扩展。<br />示例：`/UseVsixExtensions:true`|
|**/TestAdapterPath:[路径]**|强制 vstest.console.exe 进程使用测试运行中指定路径（如果有）内的自定义测试适配器。<br />示例：`/TestAdapterPath:[pathToCustomAdapters]`|
|**/Platform:[平台类型]**|强制使用给定的平台，而不是根据当前运行时确定的平台。 在 Windows 上，此选项强制只能使用 x86 和 x64 平台。 ARM 选项会中断，并将导致大多数系统上使用 x64。<br />若要在有效值（例如 ARM64）的列表中未列出的运行时上运行，请勿指定此选项。<br />有效值为 x86、x64 和 ARM。<br /> 
|**/Framework: [Framework 版本]**|要用于执行测试的目标 .NET 版本。<br />示例值有 `Framework35`、`Framework40`、`Framework45`、`FrameworkUap10`、`.NETCoreApp,Version=v1.1`。<br />TargetFrameworkAttribute 用于从程序集中自动检测此选项，并在属性不存在时默认为 `Framework40`。 如果从 .NET Core 程序集删除 [TargetFrameworkAttribute](/dotnet/api/system.runtime.versioning.targetframeworkattribute)，则必须显式指定此选项。<br />如果将目标框架指定为 Framework35，则测试在 CLR 4.0“兼容模式”下运行。<br />示例：`/Framework:framework40`|
|**/TestCaseFilter:[表达式]**|运行与给定表达式匹配的测试。<br /><Expression\> 的格式为 <property\>=<value\>[\|<Expression\>]。<br />示例：`/TestCaseFilter:"Priority=1"`<br />示例：`/TestCaseFilter:"TestCategory=Nightly|FullyQualifiedName=Namespace.ClassName.MethodName"`<br />/TestCaseFilter 命令行选项不能与 /Tests 命令行选项一起使用 。 <br />有关创建和使用表达式的信息，请参阅 [TestCase 筛选](https://github.com/Microsoft/vstest-docs/blob/master/docs/filter.md)。|
|**/?**|显示使用情况信息。|
|**/Logger:[*uri/friendlyname*]**|为测试结果指定一个记录器。 多次指定参数，以启用多个记录器。<br />示例：要将结果记录到 Visual Studio 测试结果文件 (TRX)，请使用<br />/Logger:trx<br />[;LogFileName=\<Defaults to unique file name>]|
|**/ListTests:[文件名]**|列出给定测试容器中的已发现的测试。|
|**/ListDiscoverers**|列出已安装的测试发现器。|
|**/ListExecutors**|列出已安装的测试执行器。|
|**/ListLoggers**|列出已安装的测试记录器。|
|**/ListSettingsProviders**|列出已安装的测试设置提供程序。|
|**/Blame**|在意见模式中运行测试。 此选项有助于隔离导致测试主机出现故障的有问题的测试。 检测到故障时，它会在 `TestResults/<Guid>/<Guid>_Sequence.xml` 中创建一个序列文件，用于捕获在出现故障之前运行的测试的顺序。 有关详细信息，请参阅[意见数据收集器](https://github.com/Microsoft/vstest-docs/blob/master/docs/extensions/blame-datacollector.md)。|
|**/Diag:[文件名]**|将诊断跟踪日志写入指定文件。|
|**/ResultsDirectory:[*path*]**|如果不存在，则将在指定路径中创建测试结果目录。<br />示例：`/ResultsDirectory:<pathToResultsDirectory>`|
|**/ParentProcessId:[*parentProcessId*]**|负责启动当前进程的父进程的进程 ID。|
|**/Port:[*port*]**|套接字连接和接收事件消息的端口。|
|**/Collect:[*dataCollector friendlyName*]**|为测试运行启用数据收集器。 [详细信息](https://github.com/Microsoft/vstest-docs/blob/master/docs/analyze.md)。|

> [!TIP]
> 选项和值不区分大小写。

## <a name="examples"></a>示例

运行 vstest.console.exe 的语法如下：

`vstest.console.exe [TestFileNames] [Options]`

如果此命令成功，则返回 `true` 。

以下命令针对测试库 myTestProject.dll 运行 vstest.console.exe ：

```cmd
vstest.console.exe myTestProject.dll
```

以下命令运行具有多个测试文件的 vstest.console.exe。 用空格分隔测试文件名：

```cmd
vstest.console.exe myTestFile.dll myOtherTestFile.dll
```

以下命令运行具有多个选项的 vstest.console.exe。 它在隔离进程中的 myTestFile.dll 文件中运行测试，同时使用 Local.RunSettings 文件中指定的设置 。 此外，它仅运行标记为“Priority=1”的测试，并将结果记录到 .trx 文件中。

```cmd
vstest.console.exe myTestFile.dll /Settings:Local.RunSettings /InIsolation /TestCaseFilter:"Priority=1" /Logger:trx
```

以下命令针对测试库 myTestProject.dll 运行具有 `/blame` 选项的 vstest.console.exe ：

```cmd
vstest.console.exe myTestFile.dll /blame
```

如果测试主机崩溃了，则会生成 sequence.xml 文件。 此文件包含按顺序执行的测试的完全限定名称，其中包括在崩溃时正在运行的具体测试。

如果测试主机没有崩溃，则不会生成 sequence.xml 文件。

生成的 sequence.xml 文件示例： 

```xml
<?xml version="1.0"?>
<TestSequence>
  <Test Name="TestProject.UnitTest1.TestMethodB" Source="D:\repos\TestProject\TestProject\bin\Debug\TestProject.dll" />
  <Test Name="TestProject.UnitTest1.TestMethodA" Source="D:\repos\TestProject\TestProject\bin\Debug\TestProject.dll" />
</TestSequence>
```

## <a name="uwp-example"></a>UWP 示例

对于 UWP，必须引用 .appxrecipe 文件而不是 DLL。

```cmd
vstest.console.exe /Logger:trx /Platform:x64 /framework:frameworkuap10 UnitTestsUWP\bin\x64\Release\UnitTestsUWP.build.appxrecipe
```

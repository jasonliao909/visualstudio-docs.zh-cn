---
description: Visual C++项目系统用于 .vcxproj 文件。
title: Visual C++扩展性
ms.date: 04/23/2019
ms.topic: conceptual
dev_langs:
- C++
author: corob-msft
ms.author: corob
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: c57e285e939825f70762a8b9edb0dbda258acac8
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122056727"
---
# <a name="visual-studio-c-project-system-extensibility-and-toolset-integration"></a>Visual StudioC++ Project扩展性和工具集集成

Visual C++项目系统用于 .vcxproj 文件。 它基于[Visual Studio Common Project System (CPS) ，](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/Index.md)并提供其他特定于 C++ 的扩展点，方便集成新工具集、生成体系结构和目标平台。

## <a name="c-msbuild-targets-structure"></a>C++ MSBuild目标结构

所有 .vcxproj 文件都导入这些文件：

```xml
<Import Project="$(VCTargetsPath)\Microsoft.Cpp.Default.props" />
<Import Project="$(VCTargetsPath)\Microsoft.Cpp.props" />
<Import Project="$(VCTargetsPath)\Microsoft.Cpp.targets" />
```

这些文件本身定义很少。 而是根据以下属性值导入其他文件：

- `$(ApplicationType)`

   示例：Windows Store、Android、Linux

- `$(ApplicationTypeRevision)`

   它必须是有效的版本字符串，格式为 major.minor[.build[.revision]]。

   示例：1.0、10.0.0.0

- `$(Platform)`

   出于历史原因，名为"Platform"的生成体系结构。

   示例：Win32、x86、x64、ARM

- `$(PlatformToolset)`

   示例：v140、v141、v141_xp、llvm

这些属性值指定根文件夹下 `$(VCTargetsPath)` 的文件夹名称：

> `$(VCTargetsPath)`\\ \
&nbsp;&nbsp;&nbsp;&nbsp;*应用程序类型*\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(ApplicationType)`\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(ApplicationTypeRevision)`\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*平台*\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(Platform)`\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*PlatformToolsets*\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(PlatformToolset)` \
&nbsp;&nbsp;&nbsp;&nbsp;*平台*\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(Platform)`\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*PlatformToolsets*\\ \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(PlatformToolset)`

" `$(VCTargetsPath)` \\ *平台* \\ "文件夹在 `$(ApplicationType)` 为空时用于Windows项目。

### <a name="add-a-new-platform-toolset"></a>添加新的平台工具集

若要为现有 Win32 平台添加新工具集（例如"MyToolset"，请创建"平台 `$(VCTargetsPath)` *\\ \\ Win32 \\ PlatformToolsets" \\* 下的"MyToolset"文件夹，并在此文件夹中创建 *Toolset.props* 和 *Toolset.targets* 文件。

*PlatformToolsets* 下的每个文件夹名称都显示在"Project **属性**"对话框中，作为指定平台的可用平台工具集，如下所示：

![项目"属性页"对话框中的"平台工具集"属性](media/vc-project-extensibility-platform-toolset-property.png "&quot;项目属性页&quot; 对话框中的 &quot;平台工具集&quot; 属性")

在工具集支持的每个现有平台文件夹中创建类似的 *MyToolset* 文件夹和 *Toolset.props* 和 *Toolset.targets* 文件。

### <a name="add-a-new-platform"></a>添加新平台

若要添加新平台（例如"MyPlatform"，请创建"平台"下的 *MyPlatform* 文件夹，并在此创建 `$(VCTargetsPath)` *\\ \\**Platform.default.props、Platform.props* 和 *Platform.targets* 文件。 另请创建 `$(VCTargetsPath)` *\\ " \\ 平台*<strong><em>MyPlatform</em></strong>*\\ PlatformToolsets" \\* 文件夹，并至少创建一个工具集。

每个 的" *平台"* 文件夹下的所有文件夹名称，在 `$(ApplicationType)` IDE 中 `$(ApplicationTypeRevision)` 显示为项目的可用 **平台** 选项。

!["新建平台"对话框中Project平台选择](media/vc-project-extensibility-new-project-platform.png "&quot;新建 Project 平台&quot; 对话框中的新平台选项")

### <a name="add-a-new-application-type"></a>添加新的应用程序类型

若要添加新的应用程序类型，在"应用程序类型"下创建 *MyApplicationType* 文件夹，并 `$(VCTargetsPath)` *\\ \\* 在此文件夹中创建 *Defaults.props* 文件。 应用程序类型至少需要一个修订版本，因此还要创建应用程序类型 `$(VCTargetsPath)` *\\ \\ MyApplicationType \\ 1.0* 文件夹，并创建 *Defaults.props* 文件。 还应创建 `$(VCTargetsPath)` *\\ ApplicationType \\ MyApplicationType \\ 1.0 \\ Platforms* 文件夹，并至少创建一个平台。

`$(ApplicationType)``$(ApplicationTypeRevision)`和 属性在用户界面中不可见。 它们在项目模板中定义，创建项目后无法更改。

## <a name="the-vcxproj-import-tree"></a>.vcxproj 导入树

Microsoft C++ 属性和目标文件的简化导入树如下所示：

> `$(VCTargetsPath)`\\*Microsoft.Cpp.Default.props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(MSBuildExtensionsPath)`\\`$(MSBuildToolsVersion)`\\*Microsoft.Common.props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*ImportBefore* \\*默认* \\ \* 。*props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*应用程序* \\ `$(ApplicationType)` 类型 \\*Default.props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*应用程序* \\ `$(ApplicationType)` 类型 \\ `$(ApplicationTypeRevision)` \\*Default.props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*应用程序* \\ `$(ApplicationType)` 类型 \\ `$(ApplicationTypeRevision)` \\ \\ `$(Platform)` 平台 \\*Platform.default.props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*ImportAfter* \\*默认* \\ \* 。*props*

Windows桌面项目不定义 `$(ApplicationType)` ，因此它们仅导入

> `$(VCTargetsPath)`\\*Microsoft.Cpp.Default.props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(MSBuildExtensionsPath)`\\`$(MSBuildToolsVersion)`\\*Microsoft.Common.props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*ImportBefore* \\*默认* \\ \* 。*props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\ \\ `$(Platform)` 平台 \\*Platform.default.props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*ImportAfter* \\*默认* \\ \* 。*props*

我们将使用 `$(_PlatformFolder)` 属性来保存 `$(Platform)` 平台文件夹位置。 此属性为

> `$(VCTargetsPath)`\\*平台*\\`$(Platform)`

适用于Windows桌面应用，以及

> `$(VCTargetsPath)`\\*应用程序* \\ `$(ApplicationType)` 类型 \\ `$(ApplicationTypeRevision)` \\*平台*\\`$(Platform)`

对于其他所有内容。

属性文件按以下顺序导入：

> `$(VCTargetsPath)`\\*Microsoft.Cpp.props* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*Platform.props* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*Microsoft.Cpp.Platform.props* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*ImportBefore* \\ \* 。*props* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*PlatformToolsets* \\ `$(PlatformToolset)` \\*Toolset.props* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*ImportAfter* \\ \* 。*props*

目标文件按以下顺序导入：

> `$(VCTargetsPath)`\\*Microsoft.Cpp.targets* \
&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*Microsoft.Cpp.Current.targets* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*Platform.targets* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(VCTargetsPath)`\\*Microsoft.Cpp.Platform.targets* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*ImportBefore* \\ \* 。*目标* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*PlatformToolsets* \\ `$(PlatformToolset)` \\*Toolset.target* \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$(_PlatformFolder)`\\*ImportAfter* \\ \* 。*目标*

如果需要为工具集定义一些默认属性，可以将文件添加到相应的 ImportBefore 和 ImportAfter 文件夹中。

## <a name="author-toolsetprops-and-toolsettargets-files"></a>创作工具集.props 和 Toolset.targets 文件

*Toolset.props* 和 *Toolset.targets* 文件可以完全控制使用这些工具集时生成期间发生的情况。 他们还可以控制可用的调试器、某些 IDE 用户界面，例如"属性页"对话框中的内容以及项目行为的一些其他方面。

虽然工具集可以替代整个生成过程，但通常只想让工具集修改或添加一些生成步骤，或者将不同的生成工具用作现有生成过程的一部分。 为了实现此目标，工具集可以导入许多常见属性和目标文件。 根据希望工具集执行哪些操作，这些文件可能用作导入或示例：

- `$(VCTargetsPath)`\\*Microsoft.CppCommon.targets*

  此文件定义本机生成过程的主要部分，并导入：

  - `$(VCTargetsPath)`\\*Microsoft.CppBuild.targets*

  - `$(VCTargetsPath)`\\*Microsoft.BuildSteps.targets*

  - `$(MSBuildToolsPath)`\\*Microsoft.Common.Targets*

- `$(VCTargetsPath)`\\*Microsoft.Cpp.Common.props*

   为使用 Microsoft 编译器和目标函数的工具集设置Windows。

- `$(VCTargetsPath)`\\*Microsoft.Cpp.WindowsSDK.props*

   此文件确定 Windows SDK 位置，并定义面向 Windows 的应用的一Windows。

### <a name="integrate-toolset-specific-targets-with-the-default-c-build-process"></a>将特定于工具集的目标与默认 C++ 生成过程集成

默认 C++ 生成过程在 *Microsoft.CppCommon.targets 中定义*。 目标不调用任何特定的生成工具;它们指定主要生成步骤、其顺序和依赖项。

C++ 生成有三个主要步骤，这些步骤由以下目标表示：

- `BuildGenerateSources`

- `BuildCompile`

- `BuildLink`

由于每个生成步骤都可以独立执行，因此在一个步骤中运行的目标不能依赖于作为不同步骤的一部分运行的目标中定义的项组和属性。 此划分允许某些生成性能优化。 尽管默认情况下不使用，但仍建议你遵守这种分离。

在每个步骤中运行的目标由以下属性控制：

- `$(BuildGenerateSourcesTargets)`

- `$(BuildCompileTargets)`

- `$(BeforeBuildLinkTargets)`

每个步骤还具有 Before 和 After 属性。

```xml
<Target
  Name="_BuildGenerateSourcesAction"
  DependsOnTargets="$(CommonBuildOnlyTargets);$(BeforeBuildGenerateSourcesTargets);$(BuildGenerateSourcesTargets);$(AfterBuildGenerateSourcesTargets)" />

<Target
  Name="\_BuildCompileAction"
  DependsOnTargets="$(CommonBuildOnlyTargets);$(BeforeBuildCompileTargets);$(BuildCompileTargets);$(AfterBuildCompileTargets)" />

<Target
  Name="\_BuildLinkAction"
  DependsOnTargets="$(CommonBuildOnlyTargets);$(BeforeBuildLinkTargets);$(BuildLinkTargets);$(AfterBuildLinkTargets)" />
```

有关每个步骤中包含的目标的示例，请参阅 *Microsoft.CppBuild.targets* 文件：

```xml
<BuildCompileTargets Condition="'$(ConfigurationType)'\!='Utility'">
  $(BuildCompileTargets);
  _ClCompile;
  _ResGen;
  _ResourceCompile;
  $(BuildLibTargets);
</BuildCompileTargets>
```

如果查看目标（如 ），你将看到它们本身不直接执行任何任务，而是依赖于其他目标， `_ClCompile` 包括 `ClCompile` ：

```xml
<Target Name="_ClCompile"
  DependsOnTargets="$(BeforeClCompileTargets);$(ComputeCompileInputsTargets);MakeDirsForCl;ClCompile;$(AfterClCompileTargets)" >
</Target>
```

`ClCompile` 和其他特定于生成工具的目标在 *Microsoft.CppBuild.targets 中定义为空目标*：

```xml
<Target Name="ClCompile"/>
```

由于目标为空，除非由工具集重写， `ClCompile` 否则不会执行实际生成操作。 工具集目标可以重写目标，也就是说，它们在导入 `ClCompile` `ClCompile` *Microsoft.CppBuild.targets 后可以包含另一个定义*：

```xml
<Target Name="ClCompile"
  Condition="'@(ClCompile)' != ''"
  DependsOnTargets="SelectClCompile">
  <!-- call some MSBuild tasks -->
</Target>
```

尽管其名称是在实现跨Visual Studio之前创建的，但目标不必调用 `ClCompile` CL.exe。 它还可以通过使用适当的任务来调用 Clang、gcc MSBuild编译器。

目标不应具有除 目标之外的任何依赖项，这是单个文件编译命令在 `ClCompile` `SelectClCompile` IDE 中工作所需的。

## <a name="msbuild-tasks-to-use-in-toolset-targets"></a>MSBuild工具集目标中使用的任务

若要调用实际的生成工具，目标需要调用MSBuild任务。 有一个基本 [的 Exec](../msbuild/exec-task.md) 任务，可用于指定要运行的命令行。 但是，生成工具通常有许多选项和输入。 和输出，用于跟踪增量生成，因此，为它们分配特殊任务更有意义。 例如，任务会将MSBuild转换为CL.exe开关，将其写入响应文件，并 `CL` 调用CL.exe。 它还跟踪所有输入和输出文件，供以后增量生成使用。 有关详细信息，请参阅 [增量生成和最新检查](#incremental-builds-and-up-to-date-checks)。

任务Microsoft.Cpp.Common.Tasks.dll以下任务：

- `BSCMake`

- `CL`

- `ClangCompile` (clang-gcc 开关) 

- `LIB`

- `LINK`

- `MIDL`

- `Mt`

- `RC`

- `XDCMake`

- `CustomBuild` (Exec，但具有输入和输出跟踪) 

- `SetEnv`

- `GetOutOfDateItems`

如果有一个工具执行与现有工具相同的操作，并且具有与 clang-cl 和 CL (类似的命令行开关) ，则你可以对两者使用相同的任务。

如果需要为生成工具创建新任务，可以从以下选项中进行选择：

1. 如果很少使用此任务，或者几秒钟对生成并不重要，可以使用MSBuild内联"任务：

   - Xaml 任务 (自定义生成规则) 

     有关 Xaml 任务声明的一个示例，请参阅 `$(VCTargetsPath)` \\ *BuildCustomizations* masm.xml，有关其用法，请参阅 \\  `$(VCTargetsPath)` \\ *BuildCustomizations* \\ *masm.targets*。

   - [代码任务](../msbuild/msbuild-inline-tasks.md)

1. 如果希望提高任务性能或只需要更复杂的功能，请使用常规MSBuild[编写任务的过程](../msbuild/task-writing.md)。

   如果未在工具命令行上列出该工具的所有输入和输出（如 、 和 事例中一样）。如果要自动输入和输出文件跟踪和 `CL` `MIDL` `RC` .tlog 文件创建，请从 类派生任务。 `Microsoft.Build.CPPTasks.TrackedVCToolTask` 目前，虽然有基础 [ToolTask](/dotnet/api/microsoft.build.utilities.tooltask) 类的文档，但该类的详细信息没有示例或 `TrackedVCToolTask` 文档。 如果对此特别感兴趣，请通过开发人员请求将语音[Community。](https://aka.ms/feedback/suggest?space=62)

## <a name="incremental-builds-and-up-to-date-checks"></a>增量生成和最新检查

增量MSBuild目标的默认属性 `Inputs` `Outputs` 使用 和 属性。 如果指定这些MSBuild，则仅在任何输入的时间戳比所有输出都更新时调用目标。 由于源文件通常包含或导入其他文件，并且生成工具根据工具选项生成不同的输出，因此很难在目标中指定所有可能的MSBuild输出。

为了管理此问题，C++ 生成使用不同的技术来支持增量生成。 大多数目标未指定输入和输出，因此，始终在生成期间运行。 由 调用的任务将有关所有输入和输出的信息写入扩展名为 .tlog 的 *tlog* 文件中。 更高版本使用 .tlog 文件来检查已更改的内容和需要重新生成的内容以及最新内容。 .tlog 文件也是 IDE 中默认生成最新检查的唯一源。

若要确定所有输入和输出，本机工具任务使用 tracker.exe 和由 MSBuild 提供的[FileTracker](/dotnet/api/microsoft.build.utilities.filetracker)类。

Microsoft.Build.CPPTasks.Common.dll定义 `TrackedVCToolTask` 公共抽象基类。 大多数本机工具任务都派生自此类。

从 Visual Studio 2017 update 15.8 开始，可以使用 Microsoft.Cpp.Common.Tasks.dll 中实现的任务为具有已知输入和输出的自定义目标生成 `GetOutOfDateItems` .tlog 文件。
或者，可以使用 任务创建 `WriteLinesToFile` 它们。 请参阅 `_WriteMasmTlogs` `$(VCTargetsPath)` \\ *BuildCustomizations* \\ *masm.targets* 中的目标作为示例。

## <a name="tlog-files"></a>.tlog 文件

有三种类型的 .tlog 文件 *：读取*、 *写入* 和 *命令行*。 读取和写入 .tlog 文件由增量生成和 IDE 中的最新检查使用。 命令行 .tlog 文件仅用于增量生成。

MSBuild提供以下帮助程序类来读取和写入 .tlog 文件：

- [CanonicalTrackedInputFiles](/dotnet/api/microsoft.build.utilities.canonicaltrackedinputfiles)

- [CanonicalTrackedOutputFiles](/dotnet/api/microsoft.build.utilities.canonicaltrackedoutputfiles)

[FlatTrackingData](/dotnet/api/microsoft.build.utilities.flattrackingdata)类可用于访问读取和写入 .tlog 文件，并标识比输出更新的输入，或者如果缺少输出， 它在最新检查中使用。

命令行 .tlog 文件包含有关生成中使用的命令行的信息。 它们仅用于增量生成，而不是最新的检查，因此内部格式由生成MSBuild任务确定。

### <a name="read-tlog-format"></a>读取 .tlog 格式

*读取* .tlog (\* .read. \* 。tlog) 包含有关源文件及其依赖项的信息。

行 **^** () 的符号指示一个或多个源。 共享相同依赖项的源由垂直条形分隔 **\|** () 。

依赖项文件在源之后列出，每个位于其自己的行上。 所有文件名都是完整路径。

例如，假设在 F： test *\\ \\ ConsoleApplication1 \\ ConsoleApplication1* 中找到了项目源。 如果源文件 *Class1.cpp* 包含，

```cpp
#include "stdafx.h" //precompiled header
#include "Class1.h"
```

然后 *，CL.read.1.tlog* 文件包含源文件，后跟其两个依赖项：

```tlog
^F:\TEST\CONSOLEAPPLICATION1\CONSOLEAPPLICATION1\CLASS1.CPP
F:\TEST\CONSOLEAPPLICATION1\CONSOLEAPPLICATION1\DEBUG\CONSOLEAPPLICATION1.PCH
F:\TEST\CONSOLEAPPLICATION1\CONSOLEAPPLICATION1\CLASS1.H
```

无需以大写字母编写文件名，但在某些工具中，这非常方便。

### <a name="write-tlog-format"></a>编写 .tlog 格式

*将* .tlog (\* .write。 \*tlog) 连接源和输出。

行 **^** () 的符号指示一个或多个源。 多个源由竖线分隔 **\|** () 。

从源生成的输出文件应列在源之后，每个源位于其自己的行上。 所有文件名都必须是完整路径。

例如，对于具有附加源文件 *Class1.cpp* 的简单 ConsoleApplication 项目 *，link.write.1.tlog* 文件可能包含：

```tlog
^F:\TEST\CONSOLEAPPLICATION1\CONSOLEAPPLICATION1\DEBUG\CLASS1.OBJ|F:\TEST\CONSOLEAPPLICATION1\CONSOLEAPPLICATION1\DEBUG\CONSOLEAPPLICATION1.OBJ|F:\TEST\CONSOLEAPPLICATION1\CONSOLEAPPLICATION1\DEBUG\STDAFX.OBJ
F:\TEST\CONSOLEAPPLICATION1\DEBUG\CONSOLEAPPLICATION1.ILK
F:\TEST\CONSOLEAPPLICATION1\DEBUG\CONSOLEAPPLICATION1.EXE
F:\TEST\CONSOLEAPPLICATION1\DEBUG\CONSOLEAPPLICATION1.PDB
```

## <a name="design-time-build"></a>设计时生成

在 IDE 中，.vcxproj 项目使用一组MSBuild目标从项目获取其他信息并重新生成输出文件。 其中一些目标仅用于设计时生成，但其中许多目标同时用于常规生成和设计时生成。

有关设计时生成的一般信息，请参阅设计 [时生成 的](https://github.com/dotnet/project-system/blob/master/docs/design-time-builds.md)CPS 文档。 本文档仅部分适用于Visual C++项目。

设计时生成文档中提到的 和 目标 `CompileDesignTime` `Compile` 永远不会针对 .vcxproj 项目运行。 Visual C++ .vcxproj 项目使用不同的设计时目标获取 IntelliSense 信息。

### <a name="design-time-targets-for-intellisense-information"></a>IntelliSense 信息的设计时目标

.vcxproj 项目中使用的设计时目标在 `$(VCTargetsPath)` \\ *Microsoft.Cpp.DesignTime.targets 中定义*。

目标 `GetClCommandLines` 收集 IntelliSense 的编译器选项：

```xml
<Target
  Name="GetClCommandLines"
  Returns="@(ClCommandLines)"
  DependsOnTargets="$(DesignTimeBuildInitTargets);$(ComputeCompileInputsTargets)">
```

- `DesignTimeBuildInitTargets` - 设计时生成初始化所需的仅设计时目标。 除了其他功能外，这些目标会禁用一些常规生成功能以提高性能。

- `ComputeCompileInputsTargets` – 修改编译器选项和项的一组目标。 这些目标在设计时和常规生成中运行。

目标调用 `CLCommandLine` 任务以创建用于 IntelliSense 的命令行。 同样，尽管其名称正确，但它不仅可以处理 CL 选项，还可以处理 Clang 和 gcc 选项。 编译器开关的类型由 属性 `ClangMode` 控制。

目前，任务生成的命令行始终使用 CL 开关 (即使在 Clang 模式下) ，因为它们更易于 `CLCommandLine` IntelliSense 引擎分析。

如果要添加在编译之前运行的目标（无论是常规还是设计时目标），请确保它不会中断设计时生成或影响性能。 测试目标的最简单方法就是打开开发人员命令提示符并运行以下命令：

```
msbuild /p:SolutionDir=*solution-directory-with-trailing-backslash*;Configuration=Debug;Platform=Win32;BuildingInsideVisualStudio=true;DesignTimebuild=true /t:\_PerfIntellisenseInfo /v:d /fl /fileloggerparameters:PerformanceSummary \*.vcxproj
```

此命令生成详细的生成日志 *msbuild.log，* 该日志在末尾包含目标和任务的性能摘要。

请确保在所有仅对常规生成有意义的操作（而不是设计时生成 `Condition ="'$(DesignTimeBuild)' != 'true'"` ）中使用 。

### <a name="design-time-targets-that-generate-sources"></a>生成源的设计时目标

*对于桌面本机项目，此功能* 默认处于禁用状态，当前在缓存项目 上不受支持。

如果为项目项定义了元数据，则加载项目时和更改源文件时，都会 `GeneratorTarget` 自动运行目标。

::: moniker range="vs-2017"

例如，若要从 .xaml 文件自动生成 .cpp 或 .h 文件，MSBuild `$(VSInstallDir)` \\  \\ *Microsoft* \\ *WindowsXaml* \\ *v15.0* \\ \* \\ *Microsoft.Windows。Ui。Xaml.CPP.Targets* 文件定义以下实体：

::: moniker-end

::: moniker range=">=vs-2019"

例如，若要从 .xaml 文件自动生成 .cpp 或 .h 文件，MSBuild `$(VSInstallDir)` \\  \\ *Microsoft* \\ *WindowsXaml* \\ *v16.0* \\ \* \\ *Microsoft.Windows。Ui。Xaml.CPP.Targets* 文件定义以下实体：

::: moniker-end

```xml
<ItemDefinitionGroup>
  <Page>
    <GeneratorTarget>DesignTimeMarkupCompilation</GeneratorTarget>
  </Page>
  <ApplicationDefinition>
    <GeneratorTarget>DesignTimeMarkupCompilation</GeneratorTarget>
  </ApplicationDefinition>
</ItemDefinitionGroup>
<Target Name="DesignTimeMarkupCompilation">
  <!-- BuildingProject is used in Managed builds (always true in Native) -->
  <!-- DesignTimeBuild is used in Native builds (always false in Managed) -->
  <CallTarget Condition="'$(BuildingProject)' != 'true' Or $(DesignTimeBuild) == 'true'" Targets="DesignTimeMarkupCompilationCT" />
</Target>
```

若要使用 获取源文件的未保存内容，目标和任务应注册为 pkgdef 中给定项目的 `Task.HostObject` [MsbuildHostObjects：](/dotnet/api/microsoft.visualstudio.shell.interop.ivsmsbuildhostobject?view=visualstudiosdk-2017&preserve-view=true)

```reg
\[$RootKey$\\Projects\\{8BC9CEB8-8B4A-11D0-8D11-00A0C91BC942}\\MSBuildHostObjects\]
\[$RootKey$\\Projects\\{8BC9CEB8-8B4A-11D0-8D11-00A0C91BC942}\\MSBuildHostObjects\\DesignTimeMarkupCompilationCT;CompileXaml\]
@="{83046B3F-8984-444B-A5D2-8029DEE2DB70}"
```

## <a name="visual-c-project-extensibility-in-the-visual-studio-ide"></a>Visual C++ IDE 中Visual Studio扩展性

Visual C++ 项目系统基于[VS Project 系统](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/Index.md)，并使用其扩展点。 但是，项目层次结构实现特定于 Visual C++ 而不是基于 CPS，因此层次结构扩展性限制为项目项。

### <a name="project-property-pages"></a>项目属性页

有关常规设计信息，请参阅[针对 VC++ 项目的框架多目标](https://devblogs.microsoft.com/visualstudio/framework-multi-targeting-for-vc-projects/)。

简而言之，在 c + + 项目的 " **Project 属性**" 对话框中看到的属性页由 *规则* 文件定义。 规则文件指定要在属性页上显示的一组属性，以及它们在项目文件中的保存方式和位置。 规则文件是 .xml 使用 Xaml 格式的文件。 [XamlTypes](/dotnet/api/microsoft.build.framework.xamltypes)中介绍了用于对这些类型进行序列化的类型。 有关在项目中使用规则文件的详细信息，请参阅 [属性页 XML 规则文件](/cpp/build/reference/property-page-xml-files)。

规则文件必须添加到 `PropertyPageSchema` 项组：

```xml
<ItemGroup>
  <PropertyPageSchema Include="$(VCTargetsPath)$(LangID)\general.xml;"/>
  <PropertyPageSchema Include="$(VCTargetsPath)$(LangID)\general_file.xml">
    <Context>File</Context>
  </PropertyPageSchema>
</ItemGroup>
```

`Context` 元数据限制规则可见性，这也是由规则类型控制的，并且可以具有以下值之一：

`Project` | `File` | `PropertySheet`

CPS 支持上下文类型的其他值，但这些值不用于 Visual C++ 项目。

如果规则应该在多个上下文中可见，请使用分号 (**;**) 将上下文值隔开，如下所示：

```xml
<PropertyPageSchema Include="$(MyFolder)\MyRule.xml">
  <Context>Project;PropertySheet</Context>
</PropertyPageSchema>
```

#### <a name="rule-format-and-main-types"></a>规则格式和主要类型

规则格式很简单，因此本部分仅介绍影响规则在用户界面中的外观的属性。

```xml
<Rule
  Name="ConfigurationGeneral"
  DisplayName="General"
  PageTemplate="generic"
  Description="General"
  xmlns="http://schemas.microsoft.com/build/2009/properties">
```

`PageTemplate`特性定义规则在 "**属性页**" 对话框中的显示方式。 该属性可以具有以下值之一：

| Attribute | 说明 |
|------------| - |
| `generic` | 所有属性都显示在一页上的类别标题下面<br/>规则对 `Project` 和 `PropertySheet` 上下文可见，但不可见 `File` 。<br/><br/> 示例： `$(VCTargetsPath)` \\ *1033* \\ *general.xml* |
| `tool` | 类别显示为子页。<br/>此规则可在所有上下文中显示： `Project` 、 `PropertySheet` 和 `File` 。<br/>仅当项目具有中定义的项时，才会在 Project 属性中显示规则 `ItemType` `Rule.DataSource` ，除非该规则名称包含在 `ProjectTools` 项组中。<br/><br/>示例： `$(VCTargetsPath)` \\ *1033* \\ *clang.xml* |
| `debugger` | 此页显示为 "调试" 页的一部分。<br/>当前忽略类别。<br/>规则名称应与 Debug Launcher MEF 对象的属性相匹配 `ExportDebugger` 。<br/><br/>示例： `$(VCTargetsPath)` \\ *1033* \\ *调试器 \_ 本地 \_windows.xml* |
| *客户* | 自定义模板。 模板的名称应与 `ExportPropertyPageUIFactoryProvider` MEF 对象的属性相匹配 `PropertyPageUIFactoryProvider` 。 请参阅 **VisualStudio. ProjectSystem. IPropertyPageUIFactoryProvider**。<br/><br/> 示例： `$(VCTargetsPath)` \\ *1033* \\ *userMacros.xml* |

如果规则使用基于属性网格的一个模板，则可以将这些扩展点用于其属性：

- [属性值编辑器](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/property_value_editors.md)

- [动态枚举值提供程序](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/IDynamicEnumValuesProvider.md)

#### <a name="extend-a-rule"></a>扩展规则

如果要使用现有规则，但需要添加或删除 (即，隐藏仅) 几个属性，则可以创建 [扩展规则](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/extending_rules.md)。

#### <a name="override-a-rule"></a>覆盖规则

也许您希望您的工具集使用大多数项目默认规则，而只是替换其中的一个或多个默认规则。 例如，假设您只想更改 C/c + + 规则以显示不同的编译器开关。 您可以向现有规则提供名称和显示名称相同的新规则，并在 `PropertyPageSchema` 导入默认 cpp 目标后将其包含在项组中。 在项目中只使用具有给定名称的一个规则，而包含在项组中的最后一个规则 `PropertyPageSchema` 入选。

#### <a name="project-items"></a>项目项

*ProjectItemsSchema.xml* 文件 `ContentType` `ItemType` 为被视为 Project 项的项定义和值，并定义 `FileExtension` 元素以确定将新文件添加到的项组。

默认的 ProjectItemsSchema 文件位于 `$(VCTargetsPath)` \\ *1033* \\ *ProjectItemsSchema.xml* 中。 若要对其进行扩展，必须创建一个具有新名称的架构文件，如 *MyProjectItemsSchema.xml*：

```xml
<ProjectSchemaDefinitions xmlns="http://schemas.microsoft.com/build/2009/properties">

  <ItemType Name="MyItemType" DisplayName="C/C++ compiler"/>

  <ContentType
    Name="MyItems"
    DisplayName="My items"
    ItemType=" MyItemType ">
  </ContentType>

  <FileExtension Name=".abc" ContentType=" MyItems"/>

</ProjectSchemaDefinitions>
```

然后在目标文件中添加：

```xml
<ItemGroup>
  <PropertyPageSchema Include="MyProjectItemsSchema.xml"/>
</ItemGroup>
```

示例： `$(VCTargetsPath)` \\ *BuildCustomizations* \\ *masm.xml*

### <a name="debuggers"></a>调试程序

Visual Studio 中的调试服务支持调试引擎的可扩展性。 有关详细信息，请参阅以下示例：

- [支持 lldb 调试的 MIEngine 开源项目](https://github.com/Microsoft/MIEngine)

- [Visual Studio 调试引擎示例](https://code.msdn.microsoft.com/windowsdesktop/Visual-Studio-Debug-Engine-c2e21c0e)

若要为调试会话指定调试引擎和其他属性，必须实现一个[调试 Launcher](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/IDebugLaunchProvider.md) MEF 组件，并添加一 `debugger` 条规则。 有关示例，请参阅 `$(VCTargetsPath)` \\ 1033 \\ 调试器 \_ 本地 \_windows.xml 文件。

### <a name="deploy"></a>部署

。 .vcxproj 项目使用适用于[部署提供程序](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/IDeployProvider.md)的 Project 系统可扩展性 Visual Studio。

### <a name="build-up-to-date-check"></a>生成最新检查

默认情况下，"生成最新" 检查需要在 `$(TlogLocation)` 生成过程中为所有生成输入和输出在此文件夹中创建 "读取" 和 "编写 tlog" 文件。

使用自定义最新检查：

1. 通过 `NoVCDefaultBuildUpToDateCheckProvider` 在 *工具集 .targets* 文件中添加功能，禁用默认的最新检查：

   ```xml
   <ItemGroup>
     <ProjectCapability Include="NoVCDefaultBuildUpToDateCheckProvider" />
   </ItemGroup>
   ```

1. 实现自己的 [IBuildUpToDateCheckProvider](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/IBuildUpToDateCheckProvider.md)。

## <a name="project-upgrade"></a>Project 升级

### <a name="default-vcxproj-project-upgrader"></a>.Vcxproj 项目升级程序

.vcxproj 项目升级程序更改 `PlatformToolset` 、 `ApplicationTypeRevision` 、MSBuild 工具集版本和 .net framework。 最后两个将始终更改为 Visual Studio 版本默认值，但 `PlatformToolset` `ApplicationTypeRevision` 可以通过特殊的 MSBuild 属性来控制。

升级程序使用这些条件来决定是否可以升级项目：

1. 对于定义和的 `ApplicationType` 项目 `ApplicationTypeRevision` ，有一个版本号高于当前文件夹的文件夹。

1. `_UpgradePlatformToolsetFor_<safe_toolset_name>`定义当前工具集的属性，并且其值不等于当前工具集。

   在这些属性名称中， *\<safe_toolset_name>* 表示工具集名称，其中所有非字母数字字符均替换为下划线 (**\_**) 。

当项目可以升级时，它参与了 *解决方案重定目标*。 有关详细信息，请参阅 [IVsTrackProjectRetargeting2](/dotnet/api/microsoft.visualstudio.shell.interop.ivstrackprojectretargeting2)。

如果要在 **解决方案资源管理器** 项目使用特定工具集时将项目名称修饰，请定义一个 `_PlatformToolsetShortNameFor_<safe_toolset_name>` 属性。

有关 `_UpgradePlatformToolsetFor_<safe_toolset_name>` 和 `_PlatformToolsetShortNameFor_<safe_toolset_name>` 属性定义的示例，请参阅 *属性* 文件。 有关用法的示例，请参阅 " `$(VCTargetPath)` \\ *Microsoft.*

### <a name="custom-project-upgrader"></a>自定义项目升级程序

若要使用自定义项目升级程序对象，请实现 MEF 组件，如下所示：

```csharp
/// </summary>
[Export("MyProjectUpgrader", typeof(IProjectRetargetHandler))]
[Export(typeof(IProjectRetargetHandler))]
[ExportMetadata("Name", "MyProjectUpgrader")]
[OrderPrecedence(20)]
[PartMetadata(ProjectCapabilities.Requires, ProjectCapabilities.VisualC)]

internal class MyProjectUpgrader: IProjectRetargetHandler
{
    // ...
}
```

你的代码可以导入和调用 .vcxproj 升级程序对象：

```csharp
// ...
[Import("VCDefaultProjectUpgrader")]
// ...
    IProjectRetargetHandler Lazy<IProjectRetargetHandler>
    VCDefaultProjectUpgrader { get; set; }
// ...
```

`IProjectRetargetHandler` 在 *Microsoft.VisualStudio.ProjectSystem.VS.dll* 中定义，并且类似于 `IVsRetargetProjectAsync` 。

定义 `VCProjectUpgraderObjectName` 属性，告知项目系统使用您的自定义升级程序对象：

```xml
<PropertyGroup>
  <VCProjectUpgraderObjectName>MyProjectUpgrader</VCProjectUpgraderObjectName>
</PropertyGroup>
```

#### <a name="disable-project-upgrade"></a>禁用项目升级

若要禁用项目升级，请使用 `NoUpgrade` 值：

```xml
<PropertyGroup>
  <VCProjectUpgraderObjectName>NoUpgrade</VCProjectUpgraderObjectName>
</PropertyGroup>
```

## <a name="project-cache-and-extensibility"></a>Project 缓存和扩展性

为了提高使用 Visual Studio 2017 中的大型 c + + 解决方案时的性能，引入了[项目缓存](https://devblogs.microsoft.com/cppblog/faster-c-solution-load-with-vs-15/)。 它实现为以项目数据填充的 SQLite 数据库，然后用于加载项目，而无需将 MSBuild 或 CPS 项目加载到内存中。

由于从缓存中加载的 .vcxproj 项目不存在 CPS 对象，因此将导入 `UnconfiguredProject` 或无法创建扩展的 MEF 组件 `ConfiguredProject` 。 为了支持可扩展性，当 Visual Studio 检测到项目是否使用 (或可能使用) MEF 扩展时，不会使用项目缓存。

这些项目类型始终完全加载并且在内存中具有 CPS 对象，因此会为其创建所有 MEF 扩展：

- 启动项目

- 具有自定义项目升级程序的项目，即定义 `VCProjectUpgraderObjectName` 属性

- 不以桌面 Windows 为目标的项目，即定义 `ApplicationType` 属性

- 共享项项目 ( .vcxitems) 和通过导入 .vcxitems 项目引用它们的任何项目。

如果未检测到上述任何条件，则会创建项目缓存。 缓存包括对 `get` 接口上的查询进行响应所需的 MSBuild 项目的所有数据 `VCProjectEngine` 。 这意味着，扩展所完成的 MSBuild 属性和目标文件级别上的所有修改都应在从缓存加载的项目中工作。

## <a name="shipping-your-extension"></a>寄送分机

有关如何创建 VSIX 文件的信息，请参阅[装运 Visual Studio 扩展](../extensibility/shipping-visual-studio-extensions.md)。 有关如何向特定安装位置添加文件（例如，在下添加文件）的信息， `$(VCTargetsPath)` 请参阅在 [extension 文件夹外部安装](../extensibility/set-install-root.md)。

## <a name="additional-resources"></a>其他资源

Microsoft 生成系统 ([MSBuild](../msbuild/msbuild.md)) 为项目文件提供生成引擎和基于 XML 的可扩展格式。 你应该熟悉基本[MSBuild 概念](../msbuild/msbuild-concepts.md)，并了解 Visual C++ 如何[MSBuild](/cpp/build/reference/msbuild-visual-cpp-overview)来扩展 Visual C++ 项目系统。

Managed Extensibility Framework ([MEF](/dotnet/framework/mef/)) 提供了 CPS 和 Visual C++ 项目系统所使用的扩展 api。 有关 CPS 如何使用 MEF 的概述，请参阅[VSProjectSystem 概述](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/mef.md)中的[cps 和 mef](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/mef.md#cps-and-mef) 。

您可以自定义现有生成系统以添加生成步骤或新的文件类型。 有关详细信息，请参阅[MSBuild (Visual C++) 概述](/cpp/build/reference/msbuild-visual-cpp-overview)和使用[项目属性](/cpp/build/working-with-project-properties)。

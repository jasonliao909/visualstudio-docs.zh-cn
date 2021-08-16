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
ms.openlocfilehash: 96f9199cf93603b288dd5f92817349ec69a0fcddd36ebdfa21625803190849cd
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121400516"
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

" `$(VCTargetsPath)` \\ *平台* \\ "文件夹在 `$(ApplicationType)` 为空时用于Windows桌面项目。

### <a name="add-a-new-platform-toolset"></a>添加新的平台工具集

若要为现有 Win32 平台添加新工具集（例如"MyToolset"，请创建"平台 `$(VCTargetsPath)` *\\ \\ Win32 \\ PlatformToolsets" \\* 下的 MyToolset 文件夹，并在此文件夹中创建 *Toolset.props* 和 *Toolset.targets* 文件。

*PlatformToolsets* 下的每个文件夹名称都显示在"Project **属性**"对话框中，作为指定平台的可用平台工具集，如下所示：

![项目"属性页"对话框中的"平台工具集"属性](media/vc-project-extensibility-platform-toolset-property.png "项目&quot;属性页&quot;对话框中的&quot;平台工具集&quot;属性")

在工具集支持的每个现有平台文件夹中创建类似的 *MyToolset* 文件夹和 *Toolset.props* 和 *Toolset.targets* 文件。

### <a name="add-a-new-platform"></a>添加新平台

若要添加新平台（例如"MyPlatform"，请创建"平台"下的 *MyPlatform* 文件夹，并在此创建 `$(VCTargetsPath)` *\\ \\**Platform.default.props、Platform.props* 和 *Platform.targets* 文件。 另请创建 `$(VCTargetsPath)` *\\ " \\ 平台*<strong><em>MyPlatform</em></strong>*\\ PlatformToolsets" \\* 文件夹，并至少创建一个工具集。

每个 的" *平台"* 文件夹下的所有文件夹名称，在 `$(ApplicationType)` IDE 中 `$(ApplicationTypeRevision)` 显示为项目的可用 **平台** 选项。

!["新建平台"对话框中Project平台选择](media/vc-project-extensibility-new-project-platform.png "&quot;新建平台&quot;对话框中Project平台选择")

### <a name="add-a-new-application-type"></a>添加新的应用程序类型

若要添加新的应用程序类型，在"应用程序类型"下创建 *MyApplicationType* `$(VCTargetsPath)` *\\ \\* 文件夹，并在此文件夹中创建 *Defaults.props* 文件。 应用程序类型至少需要一个修订版本，因此还要创建应用程序类型 `$(VCTargetsPath)` *\\ \\ MyApplicationType \\ 1.0* 文件夹，并创建 *Defaults.props* 文件。 还应创建 `$(VCTargetsPath)` *\\ ApplicationType \\ MyApplicationType \\ 1.0 \\ Platforms* 文件夹，并至少创建一个平台。

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

虽然工具集可以替代整个生成过程，但通常只想让工具集修改或添加一些生成步骤，或者使用不同的生成工具作为现有生成过程的一部分。 为了实现此目标，工具集可以导入许多常见属性和目标文件。 根据希望工具集执行哪些操作，这些文件可能用作导入或示例：

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

若要调用实际的生成工具，目标需要调用MSBuild任务。 有一个基本 [的 Exec](../msbuild/exec-task.md) 任务，可用于指定要运行的命令行。 但是，生成工具通常有许多选项和输入。 和输出，用于跟踪增量生成，因此，为它们分配特殊任务更有意义。 例如，该任务将MSBuild转换为CL.exe开关，将它们写入响应文件，并 `CL` 调用CL.exe。 它还跟踪所有输入和输出文件，供以后增量生成使用。 有关详细信息，请参阅 [增量生成和最新检查](#incremental-builds-and-up-to-date-checks)。

该Microsoft.Cpp.Common.Tasks.dll实现以下任务：

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

   - 自定义生成 (的 Xaml 任务) 

     有关 Xaml 任务声明的一个示例，请参阅 `$(VCTargetsPath)` \\ *BuildCustomizations* \\ *masm.xml，* 有关其用法，请参阅 `$(VCTargetsPath)` \\ *BuildCustomizations* \\ *masm.targets*。

   - [代码任务](../msbuild/msbuild-inline-tasks.md)

1. 如果希望提高任务性能或只需要更复杂的功能，请使用常规MSBuild[编写任务。](../msbuild/task-writing.md)

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

行 **^** () 的符号指示一个或多个源。 共享相同依赖项的源由垂直条分隔 **\|** () 。

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

- `DesignTimeBuildInitTargets` - 设计时生成初始化所需的仅设计时目标。 除其他功能外，这些目标会禁用一些常规生成功能以提高性能。

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

Visual C++系统基于[VS Project 系统](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/Index.md)，并使用其扩展性点。 但是，项目层次结构实现特定于项目Visual C++而不是基于 CPS，因此层次结构扩展性仅限于项目项。

### <a name="project-property-pages"></a>项目属性页

有关常规设计信息，请参阅 Framework [Multi-Targeting for VC++ Projects。](https://devblogs.microsoft.com/visualstudio/framework-multi-targeting-for-vc-projects/)

简单而言，C++ 项目的"属性"对话框中Project页 *由规则文件* 定义。 规则文件指定属性页上要显示的属性集，以及如何在项目文件中保存这些属性。 规则文件.xml Xaml 格式的文件。 [Microsoft.Build.Framework.XamlTypes](/dotnet/api/microsoft.build.framework.xamltypes)中介绍了用于序列化它们的类型。 有关在项目中使用规则文件的信息，请参阅属性页 XML [规则文件](/cpp/build/reference/property-page-xml-files)。

必须将规则文件添加到 `PropertyPageSchema` 项组：

```xml
<ItemGroup>
  <PropertyPageSchema Include="$(VCTargetsPath)$(LangID)\general.xml;"/>
  <PropertyPageSchema Include="$(VCTargetsPath)$(LangID)\general_file.xml">
    <Context>File</Context>
  </PropertyPageSchema>
</ItemGroup>
```

`Context` 元数据限制规则可见性，该可见性也由规则类型控制，并且可以具有以下值之一：

`Project` | `File` | `PropertySheet`

CPS 支持上下文类型的其他值，但它们不用于Visual C++项目。

如果规则应在多个上下文中可见，请使用分号 (**;)** 分隔上下文值，如下所示：

```xml
<PropertyPageSchema Include="$(MyFolder)\MyRule.xml">
  <Context>Project;PropertySheet</Context>
</PropertyPageSchema>
```

#### <a name="rule-format-and-main-types"></a>规则格式和主要类型

规则格式非常简单，因此本部分仅介绍影响规则在用户界面中的外观的属性。

```xml
<Rule
  Name="ConfigurationGeneral"
  DisplayName="General"
  PageTemplate="generic"
  Description="General"
  xmlns="http://schemas.microsoft.com/build/2009/properties">
```

`PageTemplate`属性定义规则在"属性页"对话框中 **的显示** 方式。 属性可以具有以下值之一：

| Attribute | 说明 |
|------------| - |
| `generic` | 所有属性都显示在"类别"标题下的一页上<br/>规则对于 和 上下文 `Project` 可见 `PropertySheet` ，但不能可见 `File` 。<br/><br/> 示例 `$(VCTargetsPath)` \\ *：1033* \\ *general.xml* |
| `tool` | 类别显示为子页。<br/>规则可以在所有上下文中可见 `Project` `PropertySheet` ：、 和 `File` 。<br/>只有当项目具有在 中定义的 Project，规则才在属性中 `ItemType` `Rule.DataSource` 可见，除非规则名称包含在 `ProjectTools` 项组中。<br/><br/>示例 `$(VCTargetsPath)` \\ *：1033* \\ *clang.xml* |
| `debugger` | 页面显示为"调试"页的一部分。<br/>类别当前被忽略。<br/>规则名称应匹配"调试Launcher MEF 对象的 `ExportDebugger` 属性。<br/><br/>示例 `$(VCTargetsPath)` \\ *：1033* \\ *调试器 \_ 本地 \_windows.xml* |
| *自 定义* | 自定义模板。 模板的名称应匹配 `ExportPropertyPageUIFactoryProvider` MEF 对象的 `PropertyPageUIFactoryProvider` 属性。 请参阅 **Microsoft.VisualStudio.ProjectSystem.Designers.Properties.IPropertyPageUIFactoryProvider**。<br/><br/> 示例 `$(VCTargetsPath)` \\ *：1033* \\ *userMacros.xml* |

如果规则使用基于属性网格的模板之一，则它可以将以下扩展点用于其属性：

- [属性值编辑器](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/property_value_editors.md)

- [动态枚举值提供程序](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/IDynamicEnumValuesProvider.md)

#### <a name="extend-a-rule"></a>扩展规则

如果要使用现有规则，但需要添加 (，即隐藏) 几个属性，可以创建扩展 [规则](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/extending_rules.md)。

#### <a name="override-a-rule"></a>重写规则

你可能希望工具集使用大多数项目默认规则，但只替换其中一个或几个规则。 例如，假设只想更改 C/C++ 规则以显示不同的编译器开关。 可以提供与现有规则相同的名称和显示名称的新规则，在导入默认 cpp 目标后将其 `PropertyPageSchema` 包括在项组中。 项目中只会使用一个具有给定名称的规则，最后一个规则将包含在 `PropertyPageSchema` 项组中。

#### <a name="project-items"></a>项目项

该文件 *ProjectItemsSchema.xml* 项的 和 值，这些项被视为Project项，并定义元素以确定新文件添加到的 Item `ContentType` `ItemType` `FileExtension` 组。

默认 ProjectItemsSchema 文件位于 `$(VCTargetsPath)` \\ *1033* \\ *ProjectItemsSchema.xml。* 若要扩展它，必须使用新名称创建架构文件，例如 *MyProjectItemsSchema.xml：*

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

然后在目标文件中，添加：

```xml
<ItemGroup>
  <PropertyPageSchema Include="MyProjectItemsSchema.xml"/>
</ItemGroup>
```

示例 `$(VCTargetsPath)` \\ *：BuildCustomizations* \\ *masm.xml*

### <a name="debuggers"></a>调试程序

中的调试服务Visual Studio调试引擎的扩展性。 有关详细信息，请参阅以下示例：

- [MIEngine，支持 lldb 调试的开源项目](https://github.com/Microsoft/MIEngine)

- [Visual Studio调试引擎示例](https://code.msdn.microsoft.com/windowsdesktop/Visual-Studio-Debug-Engine-c2e21c0e)

若要为调试会话指定调试引擎和其他属性，必须在[MEF](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/IDebugLaunchProvider.md)组件Launcher调试引擎和其他属性，并添加 `debugger` 规则。 有关示例，请参阅 `$(VCTargetsPath)` \\ 1033 \\ 调试器 \_ 本地 \_windows.xml文件。

### <a name="deploy"></a>部署

.vcxproj 项目使用Visual Studio Project提供程序 的系统[扩展性](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/IDeployProvider.md)。

### <a name="build-up-to-date-check"></a>生成最新检查

默认情况下，生成最新检查要求在所有生成输入和输出的生成过程中读取 .tlog 并写入在 文件夹中创建的 .tlog `$(TlogLocation)` 文件。

若要使用自定义最新检查，请：

1. 在 Toolset.targets 文件中添加 功能，禁用默认 `NoVCDefaultBuildUpToDateCheckProvider` *最新检查* ：

   ```xml
   <ItemGroup>
     <ProjectCapability Include="NoVCDefaultBuildUpToDateCheckProvider" />
   </ItemGroup>
   ```

1. 实现自己的 [IBuildUpToDateCheckProvider](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/extensibility/IBuildUpToDateCheckProvider.md)。

## <a name="project-upgrade"></a>Project升级

### <a name="default-vcxproj-project-upgrader"></a>默认 .vcxproj 项目升级程序

默认的 .vcxproj 项目升级程序更改 `PlatformToolset` 、、MSBuild `ApplicationTypeRevision` 工具集版本和 .Net Framework。 最后两个始终更改为Visual Studio默认值，但可通过特殊属性MSBuild `PlatformToolset` `ApplicationTypeRevision` 控制。

升级程序使用这些条件来决定是否可以升级项目：

1. 对于定义 和 `ApplicationType` 的项目，有一个比当前修订号 `ApplicationTypeRevision` 更高的文件夹。

1. 属性 `_UpgradePlatformToolsetFor_<safe_toolset_name>` 为当前工具集定义，其值不等于当前工具集。

   在这些属性名称中， 表示工具集名称，所有非字母数字字符都替换为下划线 *\<safe_toolset_name>* **\_** () 。

当项目可以升级时，它将参与 *解决方案重定目标*。 有关详细信息，请参阅 [IVsTrackProjectRetargeting2](/dotnet/api/microsoft.visualstudio.shell.interop.ivstrackprojectretargeting2)。

如果要在项目使用特定工具解决方案资源管理器修饰项目名称，请定义 `_PlatformToolsetShortNameFor_<safe_toolset_name>` 属性。

有关 和 `_UpgradePlatformToolsetFor_<safe_toolset_name>` `_PlatformToolsetShortNameFor_<safe_toolset_name>` 属性定义的示例，请参阅 *Microsoft.Cpp.Default.props* 文件。 有关用法的示例，请参阅 `$(VCTargetPath)` \\ *Microsoft.Cpp.Platform.targets* 文件。

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

代码可以导入并调用默认的 .vcxproj 升级程序对象：

```csharp
// ...
[Import("VCDefaultProjectUpgrader")]
// ...
    IProjectRetargetHandler Lazy<IProjectRetargetHandler>
    VCDefaultProjectUpgrader { get; set; }
// ...
```

`IProjectRetargetHandler` 在 *Microsoft.VisualStudio.ProjectSystem.VS.dll* 中定义，类似于 `IVsRetargetProjectAsync` 。

定义 `VCProjectUpgraderObjectName` 属性以告知项目系统使用自定义升级程序对象：

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

## <a name="project-cache-and-extensibility"></a>Project缓存和扩展性

为了在 2017 Visual Studio中处理大型 C++ 解决方案时提高性能，引入了[项目](https://devblogs.microsoft.com/cppblog/faster-c-solution-load-with-vs-15/)缓存。 它作为使用项目数据填充的 SQLite 数据库实现，然后用于加载项目，而无需将MSBuild CPS 项目加载到内存中。

由于从缓存加载的 .vcxproj 项目没有 CPS 对象，因此无法创建导入或无法创建的扩展的 MEF `UnconfiguredProject` `ConfiguredProject` 组件。 为了支持扩展性，当项目检测到项目是使用 Visual Studio还是可能使用 (MEF 扩展时，) 缓存。

这些项目类型始终完全加载，内存中有 CPS 对象，因此会为它们创建所有 MEF 扩展：

- 启动项目

- 具有自定义项目升级程序的项目，即定义 `VCProjectUpgraderObjectName` 属性

- 不面向 Desktop Windows的项目，即定义 `ApplicationType` 属性

- 共享项项目 (.vcxitems) 导入 .vcxitems 项目来引用它们的任何项目。

如果未检测到这些条件，则创建项目缓存。 缓存包括响应接口MSBuild查询 `get` 所需的所有 `VCProjectEngine` 数据。 这意味着，扩展插件MSBuild属性和目标文件级别所做的所有修改都只应在从缓存加载的项目中工作。

## <a name="shipping-your-extension"></a>寄送扩展

若要了解如何创建 VSIX 文件，请参阅[Shipping Visual Studio Extensions。](../extensibility/shipping-visual-studio-extensions.md) 若要了解如何将文件添加到特殊安装位置，例如，若要在 下添加文件， `$(VCTargetsPath)` 请参阅 [在扩展文件夹 之外安装](../extensibility/set-install-root.md)。

## <a name="additional-resources"></a>其他资源

Microsoft 生成系统 (MSBuild) [](../msbuild/msbuild.md)为项目文件提供生成引擎和可扩展的基于 XML 的格式。 你应熟悉基本[MSBuild概](../msbuild/msbuild-concepts.md)念MSBuild[如何Visual C++扩展](/cpp/build/reference/msbuild-visual-cpp-overview)Visual C++ 项目系统。

MEF Managed Extensibility Framework ([MEF](/dotnet/framework/mef/)) 提供了 CPS 和项目系统使用的Visual C++ API。 有关 CPS 如何使用 MEF 的概述，请参阅[MEF 的 VSProjectSystem 概述](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/mef.md)中的[CPS](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/mef.md#cps-and-mef)和 MEF。

可以自定义现有生成系统以添加生成步骤或新文件类型。 有关详细信息，请参阅 MSBuild (Visual C++) [概述](/cpp/build/reference/msbuild-visual-cpp-overview)[和使用项目属性](/cpp/build/working-with-project-properties)。

---
title: 自定义生成 | Microsoft Docs
description: 了解多个可用于对使用标准生成过程的 MSBuild 项目进行自定义的扩展性挂钩。
ms.custom: SEO-VS-2020
ms.date: 09/13/2021
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, transforms
- transforms [MSBuild]
ms.assetid: d0bceb3b-14fb-455c-805a-63acefa4b3ed
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
ms.openlocfilehash: 3213f5aafd312c8a7e71319e9610c9456ca595ed
ms.sourcegitcommit: 2c4ca71e7711d9c4a468b1bcff026565c765952c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2022
ms.locfileid: "145172583"
---
# <a name="customize-your-build"></a>自定义生成

使用标准生成进程（导入 Microsoft.Common.props 和 Microsoft.Common.targets）的 MSBuild 项目有多个可用于自定义生成过程的扩展性挂钩 。

## <a name="add-arguments-to-command-line-msbuild-invocations-for-your-project"></a>向项目的命令行 MSBuild 调用添加参数

源目录中或之上的 Directory.Build.rsp 文件将应用到项目的命令行生成。 有关详细信息，请参阅 [MSBuild 响应文件](../msbuild/msbuild-response-files.md#directorybuildrsp)。

## <a name="directorybuildprops-and-directorybuildtargets"></a>Directory.Build.props 和 Directory.Build.targets

通过在包含源的根文件夹中名为 Directory.Build.props 的单个文件内定义一个新属性，可以向每个项目添加该属性。 在 MSBuild 运行时，Microsoft.Common.props 会搜索 Directory.Build.props 文件的目录结构（Microsoft.Common.targets 将查找 Directory.Build.targets）。 如果找到了一个文件，它将导入该文件并读取其中定义的属性。 Directory.Build.props 是用户定义文件，对目录下的项目提供自定义选项。

> [!NOTE]
> 基于 Linux 的文件系统区分大小写。 请确保 Directory.Build.props 文件名的大小写完全匹配，否则将不会在生成流程中检测到它。
>
> 有关详细信息，请参阅[此 GitHub 问题](https://github.com/dotnet/core/issues/1991#issue-368441031)。

### <a name="directorybuildprops-example"></a>Directory.Build.props 示例

例如，如果想要使所有项目都可以访问新的 Roslyn /deterministic 功能（属性 `$(Deterministic)` 在 Roslyn `CoreCompile` 目标中公开了此功能），可以执行以下操作。

1. 在存储库根目录中创建一个名为 Directory.Build.props 的新文件。
2. 将以下 XML 添加到此文件。

   ```xml
   <Project>
    <PropertyGroup>
      <Deterministic>true</Deterministic>
    </PropertyGroup>
   </Project>
   ```

3. 运行 MSBuild。 项目现有的 Microsoft.Common.props 和 Microsoft.Common.targets 导入会找到该文件并将其导入。

### <a name="search-scope"></a>搜索范围

搜索 Directory.Build.props 文件时，MSBuild 将从项目位置 (`$(MSBuildProjectFullPath)`) 向上搜索目录结构，找到 Directory.Build.props 文件后停止。 例如，如果 `$(MSBuildProjectFullPath)` 为 c:\users\username\code\test\case1，MSBuild 将从该位置开始搜索，然后向上搜索目录结构，直到找到 Directory.Build.props 文件，如以下目录结构中所示。

```
c:\users\username\code\test\case1
c:\users\username\code\test
c:\users\username\code
c:\users\username
c:\users
c:\
```

解决方案文件的位置与 Directory.Build.props 无关。

### <a name="import-order"></a>导入顺序

Directory.Build.props 很早便已导入 Microsoft.Common.props，因此它无法使用后来定义的属性 。 因此，请避免引用尚未定义的属性（否则计算结果将为空）。

Directory.Build.props 中设置的属性可能会在项目文件或导入文件中的其他位置被覆盖，因此，应考虑将 Directory.Build.props 中的设置指定为项目的默认值 。

从 NuGet 包导入 .targets 文件后，会从 Microsoft.Common.targets 导入 Directory.Build.targets。 因此，它可以覆盖大多数生成逻辑中定义的属性和目标，或者为所有项目设置属性，而不考虑各个项目的设置。

如果需要为单个项目设置覆盖先前所有设置的属性和目标，请在最终导入后将该逻辑放在项目文件中。 要在 SDK 样式的项目中执行此操作，必须先将 SDK 样式的属性替换为等效的导入项。 查看[如何使用 MSBuild 项目 SDK](how-to-use-project-sdk.md)。

> [!NOTE]
> MSBuild 引擎在评估期间读取所有导入文件，然后才开始对特定项目（包括任何 `PreBuildEvent`）执行生成操作，以此确保 `PreBuildEvent` 或生成过程的任何其他部分都不会修改这些文件。 在下次调用 Msbuild.exe 或 Visual Studio 下次生成之后，修改才会生效。 此外，如果生成过程包含许多项目生成（如多定向或生成依赖项目），则会在针对各项目生成进行计算时读取导入的文件（包括 Directory.build.props）。

### <a name="use-case-multi-level-merging"></a>用例：多级别合并

假设你具有此标准解决方案结构：

```
\
  MySolution.sln
  Directory.Build.props     (1)
  \src
    Directory.Build.props   (2-src)
    \Project1
    \Project2
  \test
    Directory.Build.props   (2-test)
    \Project1Tests
    \Project2Tests
```

则可能需要具有所有项目 (1) 的通用属性、src 项目 (2-src) 的通用属性，以及 test 项目 (2-test) 的通用属性。

若要 MSBuild 正确地合并“内部”文件（2-src 和 2-test）和“外部”文件 (1)，必须考虑到 MSBuild 找到 Directory.Build.props 文件后会立即停止进一步的扫描   。 要继续扫描并合并到外部文件，请将此代码置于这两个内部文件中：

`<Import Project="$([MSBuild]::GetPathOfFileAbove('Directory.Build.props', '$(MSBuildThisFileDirectory)../'))" />`

MSBuild 的常规方法汇总如下：

- 对于任何给定的项目，MSBuild 将在解决方案结构中向上查找第一个 Directory.Build.props，将其与默认项合并，然后停止扫描。
- 如果你要查找并合并多个级别，请从“内部”文件 [`<Import...>`](../msbuild/property-functions.md#msbuild-getpathoffileabove)（如上所示）“外部”文件。
- 如果“外部”文件本身不会再导入其上的内容，则扫描在此处停止。
- 若要控制扫描/合并过程，请使用 `$(DirectoryBuildPropsPath)` 和 `$(ImportDirectoryBuildProps)`。

或再简单点：不能导入任何内容的第一个 Directory.Build.props 即为 MSBuild 停止的位置。

### <a name="choose-between-adding-properties-to-a-props-or-targets-file"></a>选择将属性添加到 .props 文件或 .targets 文件

MSBuild 依赖于导入顺序，属性（或 `UsingTask` 或目标）的最后一个定义是使用的定义。

使用显式导入时，可以随时从 .props 或 .targets 文件导入。 下面介绍广泛使用的约定：

- .props 文件在导入顺序的早期导入。

- .targets 文件在生成顺序的后期导入。

此约定由 `<Project Sdk="SdkName">` 导入强制执行（即，在文件的所有内容之前首先导入 Sdk.props，然后在文件的所有内容之后最后导入 Sdk.targets）。

在决定在何处放置属性后，使用以下通用原则：

- 对于许多属性，在何处定义它们并不重要，因为它们不会被覆盖，只能在执行时读取。

- 对于可能在单个项目中自定义的行为，请在 .props 文件中设置默认值。

- 通过读取可能自定义属性的值，避免在 .props 文件中设置依赖属性，因为在 MSBuild 读取用户项目之前不会进行自定义。

- 在 .targets 文件中设置依赖属性，因为它们将从单个项目中提取自定义项。

- 如果需要覆盖属性，请在所有用户项目自定义项生效后，在 .targets 文件中执行此操作。 使用派生属性时务必小心；还可能需要覆盖派生属性。

- 包括 .props 文件中的项目（以属性为条件）。 在任何项目之前都要考虑所有属性，因此可以提取用户项目属性自定义项，这使用户的项目有机会 `Remove` 或 `Update` 导入所引入的任何项目。

- 定义 .targets 文件中的目标。 但是，如果 SDK 导入了 .targets 文件，请记住此方案使得覆盖目标更加困难，因为默认情况下用户的项目没有可以覆盖它的地方。

- 如果可能，宁可在评估时自定义属性，也不更改目标内的属性。 此原则可以更轻松地加载项目并了解正在执行的操作。

## <a name="msbuildprojectextensionspath"></a>MSBuildProjectExtensionsPath

默认情况下，Microsoft.Common.props 导入 `$(MSBuildProjectExtensionsPath)$(MSBuildProjectFile).*.props`，Microsoft.Common.targets 导入 `$(MSBuildProjectExtensionsPath)$(MSBuildProjectFile).*.targets` 。 `MSBuildProjectExtensionsPath` 的默认值是 `$(BaseIntermediateOutputPath)`、`obj/`。 NuGet 用此机制来引用随包提供的生成逻辑，也就是说，在还原时，它会创建引用包内容的 `{project}.nuget.g.props` 文件。

可以通过在 Directory.Build.props 中或者在导入 Microsoft.Common.props 前将属性 `ImportProjectExtensionProps` 设为 `false` 来禁用此扩展性机制 。

> [!NOTE]
> 禁用 MSBuildProjectExtensionsPath 导入将阻止在 NuGet 包中提供的生成逻辑应用到你的项目。 一些 NuGet 包需要生成逻辑来执行其功能，并且在禁用该功能时会呈现不可用。

## <a name="user-file"></a>.user 文件

Microsoft.Common.CurrentVersion.targets 会导入 `$(MSBuildProjectFullPath).user`（如果存在），因此可以使用其他文件扩展名在你的项目旁创建一个文件。 对于计划签入源代码管理的长期更改，最好更改项目本身，以便将来的维护人员不必了解此扩展机制。

## <a name="msbuildextensionspath-and-msbuilduserextensionspath"></a>MSBuildExtensionsPath 和 MSBuildUserExtensionsPath

> [!WARNING]
> 如果使用这些扩展机制，则较难获取计算机上的可重复生成。 尝试使用可以签入源代码管理系统并在基本代码的所有开发人员之间共享的配置。

按照惯例，许多核心生成逻辑文件

```xml
$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\{TargetFileName}\ImportBefore\*.targets
```

会在其内容前后各导入一次

```xml
$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\{TargetFileName}\ImportAfter\*.targets
```

。 这一约定使已安装的 SDK 可以增强常见项目类型的生成逻辑。

在 `$(MSBuildUserExtensionsPath)` 中搜索相同的目录结构，即按用户文件夹 %LOCALAPPDATA%\Microsoft\MSBuild。 放置在该文件夹中的文件将被导入该用户凭据下运行的相应项目类型的所有生成。 通过在模式 `ImportUserLocationsByWildcardBefore{ImportingFileNameWithNoDots}` 中设置以导入文件命名的属性，可以禁用用户扩展。 例如，将 `ImportUserLocationsByWildcardBeforeMicrosoftCommonProps` 设置为 `false` 会阻止导入 `$(MSBuildUserExtensionsPath)\$(MSBuildToolsVersion)\Imports\Microsoft.Common.props\ImportBefore\*`。

## <a name="custom-configuration-based-on-project-language"></a>基于项目语言的自定义配置

如果需要根据 .NET 语言 (C#、Visual Basic 或 F#) 的不同行为，可以添加属性组，这些属性组的条件取决于项目文件扩展名`$(MSBuildProjectExtension)`来定义特定于语言的属性及其值。

```xml
<PropertyGroup Condition="'$(MSBuildProjectExtension)' == '.vbproj'">
   <!-- Put VB-only property definitions here -->
</PropertyGroup>
<PropertyGroup Condition="'$(MSBuildProjectExtension)' == '.fsproj'">
   <!-- Put F#-only property definitions here -->
</PropertyGroup>
<PropertyGroup Condition="'$(MSBuildProjectExtension)' == '.csproj'">
   <!-- Put C#-only property definitions here -->
</PropertyGroup>
```

## <a name="customize-the-solution-build"></a>自定义解决方案生成

> [!IMPORTANT]
> 以这种方式自定义解决方案生成将仅适用于带有 MSBuild.exe 的命令行生成。 它不适用于 Visual Studio 中的生成。 出于此原因，不建议将自定义项置于解决方案级别。 自定义一个解决方案中所有项目的更好方法是在解决方案文件夹中使用 Directory.Build.props 和 Directory.build.targets 文件，如本文其他部分所述。

当 MSBuild 生成解决方案文件时，它首先在内部转换为项目文件，然后再生成它。 已生成的项目文件在定义任何目标前导入 `before.{solutionname}.sln.targets`，在导入目标后导入 `after.{solutionname}.sln.targets` ，其中包括安装到 `$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\SolutionFile\ImportBefore` 和 `$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\SolutionFile\ImportAfter` 目录的目标。

例如，可以在包含以下内容的名为 after.MyCustomizedSolution.sln.targets 的相同目录中创建文件，从而定义在生成 MyCustomizedSolution.sln 后写自定义日志消息的新目标 

```xml
<Project>
 <Target Name="EmitCustomMessage" AfterTargets="Build">
   <Message Importance="High" Text="The solution has completed the Build target" />
 </Target>
</Project>
```

解决方案生成与项目生成分开进行，因此，此处的设置不会影响项目生成。

## <a name="customize-all-net-builds"></a>自定义所有 .NET 生成

维护生成服务器时，可能需要为服务器上的所有生成全局配置 MSBuild 设置。  原则上，可以修改全局 Microsoft.Common.Targets 或 Microsoft.Common.Props 文件，但有一种更好的方法。 可以通过使用特定的 MSBuild 属性并添加某些自定义 `.targets` 和 `.props` 文件，来影响特定项目类型的所有生成（如所有 C# 项目）。

若要影响通过安装 MSBuild 或 Visual Studio 控制的所有 C# 或 Visual Basic 的生成，请创建 Custom.Before.Microsoft.Common.Targets 或 Custom.After.Microsoft.Common.Targets文件（其目标将在 Microsoft.Common.targets 之前或之后运行），或创建 Custom.Before.Microsoft.Common.Props 或 Custom.After.Microsoft.Common.Props 文件  （将在 Microsoft.Common.props 之前或之后进行处理其属性）。

可以使用以下 MSBuild 属性指定这些文件的位置：

- CustomBeforeMicrosoftCommonProps
- CustomBeforeMicrosoftCommonTargets
- CustomAfterMicrosoftCommonProps
- CustomAfterMicrosoftCommonTargets
- CustomBeforeMicrosoftCSharpTargets
- CustomBeforeMicrosoftVisualBasicTargets
- CustomAfterMicrosoftCSharpTargets
- CustomAfterMicrosoftVisualBasicTargets

这些属性的通用版本都会影响 C# 和 Visual Basic 项目。 可以在 MSBuild 命令行中设置这些属性。

```cmd
msbuild /p:CustomBeforeMicrosoftCommonTargets="C:\build\config\Custom.Before.Microsoft.Common.Targets" MyProject.csproj
```

可以针对不同的应用场景使用最适合的方法。 凭借 Visual Studio 扩展性，你可以自定义生成系统，并提供安装和管理自定义项的机制。

如果你有一个专用的生成服务器，并且需要确保特定目标始终在该服务器上执行的相应项目类型的所有生成上执行，则适合使用全局自定义 `.targets` 或 `.props` 文件。  如果需要让自定义目标仅在某些条件适用时执行，可使用其他文件位置，并（仅在需要时）通过在 MSBuild 命令行中设置相应的 MSBuild 属性设置该文件的路径。

> [!WARNING]
> 每当 Visual Studio 生成匹配类型的任何项目时，只要它能在 MSBuild 文件夹中找到自定义文件 `.targets` 或 `.props`，就能使用它们。 这可能会带来意想不到的后果，如果操作不正确，可能会导致 Visual Studio 无法在你的计算机上进行生成。

## <a name="customize-c-builds"></a>自定义 C++ 生成

对于 C++ 项目，无法按相同的方式使用前面提到的自定义 .targets 和 .props 文件来覆盖默认设置 。 Directory.Build.props 由 Microsoft.Common.props 导入 `Microsoft.Cpp.Default.props`，而大多数默认设置都在 Microsoft.Cpp.props 中定义；并且，由于已经定义，许多属性都不能使用“如果尚未定义”条件，但是对于在 `PropertyGroup` 中使用 `Label="Configuration"` 定义的特殊项目属性，默认设置必须不同（请参阅 [.vcxproj 和 .props 文件结构](/cpp/build/reference/vcxproj-file-structure)）  。

但是，你可以使用以下属性来指定要在 Microsoft.Cpp.\* 文件之前/之后自动导入的 .props 文件 ：

- ForceImportAfterCppDefaultProps
- ForceImportBeforeCppProps
- ForceImportAfterCppProps
- ForceImportBeforeCppTargets
- ForceImportAfterCppTargets

要自定义所有 C++ 生成的默认属性值，请创建另一个 .props 文件（例如 MyProps.props），然后在指向该文件的 `Directory.Build.props` 中定义 `ForceImportAfterCppProps` 属性 ：

```xml
<PropertyGroup>
  <ForceImportAfterCppProps>$(MsbuildThisFileDirectory)\MyProps.props</ForceImportAfterCppProps>
</PropertyGroup>
```

MyProps.props 会自动导入到 Microsoft.Cpp.props 的最末尾 。

## <a name="customize-all-c-builds"></a>自定义所有 C++ 生成

不建议自定义 Visual Studio 安装，因为无法轻松跟踪此类自定义项，但如果要扩展 Visual Studio 以自定义特定平台的 C++ 生成，则可以为每个平台创建 `.targets` 文件，并将这些文件作为 Visual Studio 扩展的一部分放在适用于这些平台的相应导入文件夹中。

Win32 平台的 `.targets` 文件 (Microsoft.Cpp.Win32.targets) 包含以下 `Import` 元素：

```xml
<Import Project="$(VCTargetsPath)\Platforms\Win32\ImportBefore\*.targets"
        Condition="Exists('$(VCTargetsPath)\Platforms\Win32\ImportBefore')"
/>
```

同一文件的末尾附近有一个相似的元素：

```xml
<Import Project="$(VCTargetsPath)\Platforms\Win32\ImportAfter\*.targets"
        Condition="Exists('$(VCTargetsPath)\Platforms\Win32\ImportAfter')"
/>
```

*%ProgramFiles32%\MSBuild\Microsoft.Cpp\v{version}\Platforms\* 中的其他目标平台也存在类似的导入元素。

根据平台将 `.targets` 文件放在适当的 `ImportAfter` 文件夹中后，MSBuild 会将文件导入到该平台的每个 C++ 生成中。 如果需要，可以将多个 `.targets` 文件放在那里。 

使用 Visual Studio 扩展性可以进行进一步的自定义，例如定义新平台。 有关详细信息，请参阅 [C++ 项目扩展性](../extensibility/visual-cpp-project-extensibility.md)。

### <a name="specify-a-custom-import-on-the-command-line"></a>在命令行上指定自定义导入

对于要针对某个 C++ 项目的特定生成加入的自定义 `.targets`，请在命令行上设置 `ForceImportBeforeCppTargets` 和/或 `ForceImportAfterCppTargets` 属性。

```cmd
msbuild /p:ForceImportBeforeCppTargets="C:\build\config\Custom.Before.Microsoft.Cpp.Targets" MyCppProject.vcxproj
```

对于全局设置（例如，要影响生成服务器上某个平台的所有 C++ 生成），有两种方法。 首先，可以使用始终设置的系统环境变量来设置这些属性。 之所以可行，是因为 MSBuild 始终读取环境并为所有环境变量创建（或覆盖）属性。

## <a name="see-also"></a>请参阅

- [MSBuild 概念](../msbuild/msbuild-concepts.md)

- [MSBuild 参考](../msbuild/msbuild-reference.md)

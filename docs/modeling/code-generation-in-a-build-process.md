---
title: 生成过程中的代码生成
description: 了解文本转换如何可以作为 Visual Studio 解决方案的生成进程的一部分调用。
ms.custom: SEO-VS-2020
ms.date: 03/22/2018
ms.topic: how-to
helpviewer_keywords:
- text templates, build tasks
- text templates, transforming by using msbuild
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: bb628f967f9d56f954c2c639951f9317fa8efed9
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600677"
---
# <a name="invoke-text-transformation-in-the-build-process"></a>在生成过程中调用文本转换

[文本转换](../modeling/code-generation-and-t4-text-templates.md)可以作为 Visual Studio 解决方案的[生成进程](/azure/devops/pipelines/index)的一部分调用。 有一些专用于文本转换的生成任务。 T4 生成任务运行设计时文本模板，它们还编译运行时（已预处理的）文本模板。

根据你使用的引擎，生成任务可完成的操作之间是有一些差异的。 在 Visual Studio 中生成解决方案时，如果设置了 [hostspecific="true"](../modeling/t4-template-directive.md) 特性，则文本模板可访问 Visual Studio API (EnvDTE)。 但当你从命令行生成解决方案时，或者当你通过 Visual Studio 启动服务器生成时，此操作无效。 在这些情况下，生成由 MSBuild 执行，并且使用不同的 T4 主机。 这意味着当你在 MSBuild 中生成文本模板时，无法以相同的方式访问项目文件名等内容。 但是，可以[使用生成参数将环境信息传递到文本模板和指令处理器](#parameters)。

## <a name="configure-your-machines"></a><a name="buildserver"></a> 配置计算机

若要在开发计算机上启用生成任务，请安装适用于 Visual Studio 的建模 SDK。

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

如果[生成服务器](/azure/devops/pipelines/agents/agents)在未安装 Visual Studio 的计算机上运行，则将下列文件从开发计算机复制到生成计算机：

- %ProgramFiles(x86)%\Microsoft Visual Studio\2019\Community\MSBuild\Microsoft\VisualStudio\v16.0\TextTemplating

  - Microsoft.VisualStudio.TextTemplating.Sdk.Host.15.0.dll
  - Microsoft.TextTemplating.Build.Tasks.dll
  - Microsoft.TextTemplating.targets

- %ProgramFiles(x86)%\Microsoft Visual Studio\2019\Community\VSSDK\VisualStudioIntegration\Common\Assemblies\v4.0

  - Microsoft.VisualStudio.TextTemplating.15.0.dll
  - Microsoft.VisualStudio.TextTemplating.Interfaces.15.0.dll
  - Microsoft.VisualStudio.TextTemplating.Interfaces.15.0.dll

- %ProgramFiles(x86)%\Microsoft Visual Studio\2019\Community\Common7\IDE\PublicAssemblies

  - Microsoft.VisualStudio.TextTemplating.Modeling.15.0.dll

> [!TIP]
> 如果在生成服务器上运行 TextTemplating 生成目标时获得 Microsoft.CodeAnalysis 方法的 `MissingMethodException`，请确保 Roslyn 程序集位于与生成可执行文件（例如，msbuild.exe）的目录相同的名为 Roslyn 的目录中。 

## <a name="edit-the-project-file"></a>编辑项目文件

编辑项目文件以便在 MSBuild 中配置功能，例如，导入文本转换目标。

在“解决方案资源管理器”中，从项目的右键单击菜单，选择“上传”。  这允许你在 XML 编辑器中编辑 .csproj 或 .vbproj 文件。 完成编辑后，请选择“重新加载”。

## <a name="import-the-text-transformation-targets"></a>导入文本转换目标

在 .vbproj 或 .csproj 文件中，查找与下类似的行：

`<Import Project="$(MSBuildToolsPath)\Microsoft.CSharp.targets" />`

\- 或 -

`<Import Project="$(MSBuildToolsPath)\Microsoft.VisualBasic.targets" />`

在该行之后插入文本模板化导入：

::: moniker range=">=vs-2019"

```xml
<Import Project="$(MSBuildExtensionsPath)\Microsoft\VisualStudio\v16.0\TextTemplating\Microsoft.TextTemplating.targets" />
```

::: moniker-end

::: moniker range="vs-2017"

```xml
<Import Project="$(MSBuildExtensionsPath)\Microsoft\VisualStudio\v15.0\TextTemplating\Microsoft.TextTemplating.targets" />
```

::: moniker-end

## <a name="transform-templates-in-a-build"></a>在生成中转换模板

有一些属性你可插入项目文件以控制转换任务：

- 在每次生成开始时运行转换任务：

    ```xml
    <PropertyGroup>
        <TransformOnBuild>true</TransformOnBuild>
    </PropertyGroup>
    ```

- 例如，覆盖只读文件，因为不会签出这些文件：

    ```xml
    <PropertyGroup>
        <OverwriteReadOnlyOutputFiles>true</OverwriteReadOnlyOutputFiles>
    </PropertyGroup>
    ```

- 每次转换所有模板：

    ```xml
    <PropertyGroup>
        <TransformOutOfDateOnly>false</TransformOutOfDateOnly>
    </PropertyGroup>
    ```

     默认情况下，如果文件低于以下版本，T4 MSBuild 任务会重新生成输出文件：

     - 其模板文件
     - 包含的任何文件
     - 模板或其使用的指令处理器以前读取过的任何文件

     这是一个依赖项测试，其功能比 Visual Studio 中的“转换所有模板”命令使用的测试强大得多，后者仅比较模板和输出文件的日期。

若要在项目中仅执行文本转换，请调用 TransformAll 任务：

`msbuild myProject.csproj /t:TransformAll`

转换特定文本模板：

`msbuild myProject.csproj /t:Transform /p:TransformFile="Template1.tt"`

你可以在 TransformFile 中使用通配符：

`msbuild dsl.csproj /t:Transform /p:TransformFile="GeneratedCode\**\*.tt"`

## <a name="source-control"></a>源代码管理

没有针对源代码管理系统的特定内置集成。 但是，可以添加自己的扩展以便在生成的文件中签出和签入。 默认情况下，文本转换任务可避免覆盖标记为只读的文件。 遇到此类文件时，将会在 Visual Studio 错误列表中记录错误，任务将失败。

若要指定应覆盖只读文件，请插入此属性：

`<OverwriteReadOnlyOutputFiles>true</OverwriteReadOnlyOutputFiles>`

除非自定义后续处理步骤，否则会在覆盖文件时，在错误列表中记录相应的警告。

## <a name="customize-the-build-process"></a>自定义生成过程

文本转换发生在生成过程中的其他任务之前。 你可以通过设置 `$(BeforeTransform)` 属性和 `$(AfterTransform)` 属性来定义在转换前后调用的任务：

```xml
<PropertyGroup>
    <BeforeTransform>CustomPreTransform</BeforeTransform>
    <AfterTransform>CustomPostTransform</AfterTransform>
</PropertyGroup>
<Target Name="CustomPreTransform">
    <Message Text="In CustomPreTransform..." Importance="High" />
</Target>
<Target Name="CustomPostTransform">
    <Message Text="In CustomPostTransform..." Importance="High" />
</Target>
```

在 `AfterTransform` 中，你可以引用文件列表：

- GeneratedFiles - 由过程写入的文件的列表。 对于覆盖现有只读文件的文件，`%(GeneratedFiles.ReadOnlyFileOverwritten)` 将为 true。 可将这些文件签出源代码管理。

- NonGeneratedFiles - 未覆盖的只读文件的列表。

例如，定义任务以签出 GeneratedFiles。

## <a name="outputfilepath-and-outputfilename"></a>OutputFilePath 和 OutputFileName

这些属性仅由 MSBuild 使用。 它们不影响 Visual Studio 中的代码生成。 它们将生成的输出文件重定向到不同的文件夹或文件。 目标文件夹必须已存在。

```xml
<ItemGroup>
  <None Include="MyTemplate.tt">
    <Generator>TextTemplatingFileGenerator</Generator>
    <OutputFilePath>MyFolder</OutputFilePath>
    <LastGenOutput>MyTemplate.cs</LastGenOutput>
  </None>
</ItemGroup>
```

要重定向到的一个有用的文件夹是 `$(IntermediateOutputPath)`。

如果指定输出文件名，则它会优先于在模板的输出指令中指定的扩展。

```xml
<ItemGroup>
  <None Include="MyTemplate.tt">
    <Generator>TextTemplatingFileGenerator</Generator>
    <OutputFileName>MyOutputFileName.cs</OutputFileName>
    <LastGenOutput>MyTemplate.cs</LastGenOutput>
  </None>
</ItemGroup>
```

如果你还要使用“全部转换”命令或运行单个文件生成器来转换 Visual Studio 内的模板，则不建议指定 OutputFileName 或 OutputFilePath。 最终将得到不同的文件路径，具体取决于你触发转换的方式。 这可能会造成混淆。

## <a name="add-reference-and-include-paths"></a>添加引用和包括路径

主机有一个默认的路径集，主机将在这些路径中搜索模板中引用的程序集。 添加到此路径集：

```xml
<ItemGroup>
    <T4ReferencePath Include="$(VsIdePath)PublicAssemblies\" />
    <!-- Add more T4ReferencePath items here -->
</ItemGroup>
```

若要设置将在其中搜索包含文件的文件夹，请提供以分号分隔的列表。 通常将添加到现有文件夹列表。

```xml
<PropertyGroup>
    <IncludeFolders>
$(IncludeFolders);$(MSBuildProjectDirectory)\Include;AnotherFolder;And\Another</IncludeFolders>
</PropertyGroup>
```

## <a name="pass-build-context-data-into-the-templates"></a><a name="parameters"></a> 将生成上下文数据传递到模板

你可以在项目文件中设置参数值。 例如，你可以传递[生成](../msbuild/msbuild-properties.md)属性和[环境变量](../msbuild/how-to-use-environment-variables-in-a-build.md)：

```xml
<ItemGroup>
  <T4ParameterValues Include="ProjectFolder">
    <Value>$(ProjectDir)</Value>
    <Visible>false</Visible>
  </T4ParameterValues>
</ItemGroup>
```

在文本模板的 Template 指令中设置 `hostspecific`。 使用 [parameter](../modeling/t4-parameter-directive.md) 指令获取值：

```
<#@template language="c#" hostspecific="true"#>
<#@ parameter type="System.String" name="ProjectFolder" #>
The project folder is: <#= ProjectFolder #>
```

在指令处理器中，可以调用 [ITextTemplatingEngineHost.ResolveParameterValue](/previous-versions/visualstudio/visual-studio-2012/bb126369\(v\=vs.110\))：

```csharp
string value = Host.ResolveParameterValue("-", "-", "parameterName");
```

```vb
Dim value = Host.ResolveParameterValue("-", "-", "parameterName")
```

> [!NOTE]
> 仅当使用 MSBuild 时，`ResolveParameterValue` 才会通过 `T4ParameterValues` 获取数据。 当使用 Visual Studio 转换模板时，参数会具有默认值。

## <a name="use-project-properties-in-assembly-and-include-directives"></a><a name="msbuild"></a> 在 Assembly 和 Include 指令中使用项目属性

Visual Studio 宏（如 $(SolutionDir）在 MSBuild 中不起作用。 你可以改用项目属性。

编辑 .csproj 或 .vbproj 文件以定义项目属性。  此示例定义一个名为 myLibFolder 的属性：

```xml
<!-- Define a project property, myLibFolder: -->
<PropertyGroup>
    <myLibFolder>$(MSBuildProjectDirectory)\..\libs</myLibFolder>
</PropertyGroup>

<!-- Tell the MSBuild T4 task to make the property available: -->
<ItemGroup>
    <T4ParameterValues Include="myLibFolder">
      <Value>$(myLibFolder)</Value>
    </T4ParameterValues>
  </ItemGroup>
```

现在，你可以在 Assembly 和 Include 指令中使用项目属性：

```
<#@ assembly name="$(myLibFolder)\MyLib.dll" #>
<#@ include file="$(myLibFolder)\MyIncludeFile.t4" #>
```

这些指令在 MSBuild 和 Visual Studio 主机中都通过 T4parameterValues 获取值。

## <a name="q--a"></a>问题解答

为什么要在生成服务器中转换模板？我已在签入代码之前，在 Visual Studio 中转换了模板。

如果你更新一个包含的文件或模板读取的其他文件，则 Visual Studio 将不会自动转换相应文件。 作为生成的一部分的模板转换操作将确保所有内容保持最新状态。

**还有哪些其他选项适用于转换文本模板？**

- [TextTransform 实用工具](../modeling/generating-files-with-the-texttransform-utility.md)可在命令脚本中使用。 在大多数情况下，使用 MSBuild 更为方便。

- [在 Visual Studio 扩展中调用文本转换](../modeling/invoking-text-transformation-in-a-vs-extension.md)。

- [设计时文本模板](../modeling/design-time-code-generation-by-using-t4-text-templates.md)由 Visual Studio 转换。

- [运行时文本模板](../modeling/run-time-text-generation-with-t4-text-templates.md)在应用程序运行时转换。

## <a name="see-also"></a>另请参阅

::: moniker range="vs-2017"

- 有关 T4 MSbuild 模板的详细指南，请参阅 `%ProgramFiles(x86)%\Microsoft Visual Studio\2017\Enterprise\msbuild\Microsoft\VisualStudio\v15.0\TextTemplating\Microsoft.TextTemplating.targets`

::: moniker-end

::: moniker range=">=vs-2019"

- 有关 T4 MSbuild 模板的详细指南，请参阅 `%ProgramFiles(x86)%\Microsoft Visual Studio\2019\Enterprise\msbuild\Microsoft\VisualStudio\v16.0\TextTemplating\Microsoft.TextTemplating.targets`

::: moniker-end

- [编写 T4 文本模板](../modeling/writing-a-t4-text-template.md)

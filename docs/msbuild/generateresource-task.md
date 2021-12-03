---
title: GenerateResource 任务 | Microsoft Docs
description: 使用 MSBuild GenerateResource 任务可在 .txt 或 .resx 文件与公共语言运行时二进制 .resources 文件之间进行转换。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#GenerateResource
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, GenerateResource task
- GenerateResource task [MSBuild]
ms.assetid: c0aff32f-f2cc-46f6-9c3e-a5c9f8f912b1
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
ms.openlocfilehash: 1d0054ab1520bc021cc37ddd51220593e7ce627b
ms.sourcegitcommit: a149b3a034bb555ad217656c0ec8bc1672b1e215
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2021
ms.locfileid: "133514475"
---
# <a name="generateresource-task"></a>GenerateResource 任务

在 和 (基于 XML 的资源格式) 文件以及可嵌入运行时二进制可执行文件或编译到附属程序集中的公共语言运行时二进制文件 `.txt` `.resx` `.resources` 。 此任务通常用于将 或 `.txt` `.resx` 文件转换为 `.resources` 文件。 `GenerateResource` 任务在功能上类似于 [resgen.exe](/dotnet/framework/tools/resgen-exe-resource-file-generator)。

## <a name="parameters"></a>参数

下表描述了 `GenerateResource` 任务的参数。

|参数|描述|
|---------------|-----------------|
|`AdditionalInputs`|可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 包含此任务完成的依赖项检查的其他输入。 例如，项目和目标通常应该为输入，以便在对它们进行更新时，所有资源都重新生成。|
|`EnvironmentVariables`|可选 `String[]` 参数。<br /><br /> 除（或选择性替代）常规环境块外，还指定应传递到生成的 resgen.exe 中的环境变量的名称/值对数组。 |
|`ExcludedInputPaths`|可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定一个项数组，这些项指定在最新检查过程中将忽略跟踪输入的路径。|
|`ExecuteAsTool`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，请于进程外从适当的目标框架运行 tlbimp.exe 和 aximp.exe 来生成所需的包装器程序集。   此参数允许多目标的 `ResolveComReferences`。|
|`FilesWritten`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 输出参数。<br /><br /> 包含写入磁盘的所有文件的名称。 其中包含缓存文件（如果存在）。 此参数对实现 Clean 非常有用。|
|`MinimalRebuildFromTracking`|可选 `Boolean` 参数。<br /><br /> 获取或设置一个开关，用于指定是否使用跟踪的增量生成。 如果为 `true`，则启用增量生成；否则，将强制执行重新生成。|
|`NeverLockTypeAssemblies`|可选 `Boolean` 参数。<br /><br /> 获取或设置一个布尔值，该值指定是创建新的 [AppDomain](/dotnet/api/system.appdomain) 来计算资源 (.resx) 文件 (true) 还是仅当资源文件引用用户的程序集时才创建新的 [AppDomain](/dotnet/api/system.appdomain) (false)。|
|`OutputResources`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 输出参数。<br /><br /> 指定生成的文件的名称，例如 `.resources` 文件。 如果未指定名称，则使用匹配输入文件的名称，并且创建的文件将放置在包含输入文件的 `.resources` 目录中。|
|`PublicClass`|可选 `Boolean` 参数。<br /><br /> 如果 `true` 为 ，则创建强类型资源类作为公共类。|
|`References`|可选 `String[]` 参数。<br /><br /> 从 加载文件中 `.resx` 类型的引用。 `.resx` 文件数据元素可能具有 .NET 类型。 读取 *.resx* 文件时，必须解析此类型。 通常，使用标准类型加载规则可成功解析。 如果在 `References` 中提供程序集，则它们具有优先级。<br /><br /> 强类型资源不需要此参数。|
|`SdkToolsPath`|可选 `String` 参数。<br /><br /> 指定 SDK 工具（例如 resgen.exe）的路径  。|
|`Sources`|必选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定要转换的项。 传递到此参数的项必须具有以下文件扩展名之一：<br /><br /> -   `.txt`：指定要转换的文本文件的扩展名。 文本文件只能包含字符串资源。<br />-   .resx  ：指定要转换的基于 XML 的资源文件的扩展名。<br />-   .restext  ：指定与 .txt 相同的格式  。 如果要在生成过程中明确区分包含资源的源文件与其他源文件，则这个不相同的扩展名非常有用。<br />-   .resources  ：指定要转换的资源文件的扩展名。|
|`StateFile`|可选 <xref:Microsoft.Build.Framework.ITaskItem> 参数。<br /><br /> 指定用于加速 .resx 输入文件中链接的依赖项检查的可选缓存文件的路径  。|
|`StronglyTypedClassName`|可选 `String` 参数。<br /><br /> 指定强类型资源类的类名。 如果未指定此参数，则使用资源文件的基名称。|
|`StronglyTypedFilename`|可选 <xref:Microsoft.Build.Framework.ITaskItem> 参数。<br /><br /> 指定源文件的文件名。 如果未指定此参数，则会将类的名称用作基文件名，其扩展名取决于语言。 例如：MyClass.cs  。|
|`StronglyTypedLanguage`|可选 `String` 参数。<br /><br /> 指定为强类型资源生成类源时使用的语言。 此参数必须与 CodeDomProvider 所使用的其中一种语言完全匹配。 例如 `VB` 或 `C#`。<br /><br /> 通过向此参数传递值，可指示任务生成强类型资源。|
|`StronglyTypedManifestPrefix`|可选 `String` 参数。<br /><br /> 指定要用于强类型资源的生成的类源中的资源命名空间或清单前缀。|
|`StronglyTypedNamespace`|可选 `String` 参数。<br /><br /> 指定要用于强类型资源的生成的类源的命名空间。 如果未指定此参数，则任何强类型资源都位于全局命名空间中。|
|`TLogReadFiles`|可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 只读参数。<br /><br /> 获取表示读取跟踪日志的项的数组。|
|`TLogWriteFiles`|可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 只读参数。<br /><br /> 获取表示写入跟踪日志的项的数组。|
|`ToolArchitecture`|可选 <xref:System.String?displayProperty=fullName> 参数。<br /><br /> 用于确定是否需要使用 Tracker.exe 来生成 ResGen.exe。  <br /><br /> 应解析为 <xref:Microsoft.Build.Utilities.ExecutableType> 枚举的成员。 如果为 `String.Empty`，请使用启发式方法来确定默认体系结构。 应对 Microsoft.Build.Utilities.ExecutableType 枚举的成员可解析。|
|`TrackerFrameworkPath`|可选 `String` 参数。<br /><br /> 指定其中包含 FileTracker.dll 的适当 .NET Framework 位置的路径  。<br /><br /> 如果设置此参数，则用户应负责确保其传递的 FileTracker.dll 的位数与其要使用的 ResGen.exe 的位数相匹配   。 如果未设置，则任务会基于当前的 .NET Framework 版本决定合适的位置。|
|`TrackerLogDirectory`|可选 `String` 参数。<br /><br /> 指定用于放置运行此任务生成的跟踪日志的中间目录。|
|`TrackerSdkPath`|可选 `String` 参数。<br /><br /> 指定包含 Tracker.exe 的适当 Windows SDK 位置的路径  。<br /><br /> 如果设置此参数，则用户应负责确保其传递的 Tracker.exe 的位数与其要使用的 ResGen.exe 的位数相匹配   。 如果未设置，则任务会基于当前的 Windows SDK 决定合适的位置。|
|`TrackFileAccess`|可选 <xref:System.Boolean> 参数。<br /><br /> 如果为 true，则使用输入文件的目录来解析相对文件路径。|
|`UsePreserializedResources`|可选 `Boolean` 参数。<br /><br /> 如果为 ，则指定使用 （而不是 ）对非字符串资源进行序列化，而 .NET Core 或 `true` <xref:System.Resources.Extensions.PreserializedResourceWriter> <xref:System.Resources.ResourceWriter> .NET 5 或更高版本不支持。 
|`UseSourcePath`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则指定使用输入文件的目录来解析相对文件路径。|

## <a name="remarks"></a>备注

由于 `.resx` 文件可能包含指向其他资源文件的链接，因此只需比较和文件时间戳来查看输出是否最新 `.resx` `.resources` 是不够的。 相反， `GenerateResource` 任务会跟随文件中 `.resx` 的链接，并检查链接文件的时间戳。 这意味着通常不应对包含 `GenerateResource` 任务的目标使用 `Inputs` 和 `Outputs` 属性，因为这样会导致在实际上应运行该任务时跳过此任务。

除上面列出的参数外，此任务还从 <xref:Microsoft.Build.Tasks.TaskExtension> 类继承参数，后者自身继承自 <xref:Microsoft.Build.Utilities.Task> 类。 有关这些其他参数的列表及其说明的信息，请参阅 [TaskExtension 基类](../msbuild/taskextension-base-class.md)。

使用 MSBuild 4.0 生成 .NET 3.5 项目时，x86 资源生成可能会失败。 若要解决此问题，可将目标生成为 AnyCPU 程序集。

参数 `UsePreserializedResources` 从常规 .NET 生成 `$(GenerateResourceUsePreserializedResources)` 进程中的 属性获取其值。 在使用 .NET 5 或更高版本的 .NET Core 项目和项目中，此属性 `true` 默认设置为 。 可以将 设置为 以允许 .NET SDK 生成面向 `$(GenerateResourceUsePreserializedResources)` `true` 4.6.1 .NET Framework 4.6.1 或更高版本的项目，这些项目使用非字符串资源。 程序集 `System.Resources.Extensions` 必须在运行时可用。 它可在 .NET Core 3.0 及更高版本和 .NET 5 及更高版本中提供，并且可通过 PackageReference.| 在 .NET Framework 4.6.1 或更高版本中|

## <a name="example"></a>示例

以下示例使用 任务 `GenerateResource` 从 `.resources` 项集合指定的文件生成 `Resx` 文件。

```xml
<GenerateResource
    Sources="@(Resx)"
    OutputResources="@(Resx->'$(IntermediateOutputPath)%(Identity).resources')">
    <Output
        TaskParameter="OutputResources"
        ItemName="Resources"/>
</GenerateResource>
```

`GenerateResource` 任务使用 `<EmbeddedResource>` 项的 `<LogicalName>` 元数据来命名嵌入程序集中的资源。

假设程序集名为 myAssembly，则以下代码将生成名为 的嵌入资源 `someQualifier.someResource.resources` ：

```xml
<ItemGroup>
    <EmbeddedResource Include="myResource.resx">
        <LogicalName>someQualifier.someResource.resources</LogicalName>
    </EmbeddedResource>
</ItemGroup>
```

如果没有 `<LogicalName>` 元数据，资源将命名为 `myAssembly.myResource.resources` 。  此示例仅适用于 Visual Basic 和 Visual C# 生成过程。

## <a name="see-also"></a>请参阅

- [任务](../msbuild/msbuild-tasks.md)
- [任务参考](../msbuild/msbuild-task-reference.md)

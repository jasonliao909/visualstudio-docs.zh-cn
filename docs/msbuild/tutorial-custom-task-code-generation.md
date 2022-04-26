---
title: 创建自定义任务 | Microsoft Docs
description: 了解如何使用 MSBuild 创建用于代码生成的自定义任务（用于正确处理增量生成和清理操作）。
ms.date: 02/17/2022
ms.topic: tutorial
helpviewer_keywords:
- tasks
- MSBuild, tasks
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
ms.openlocfilehash: 1d599b3856158f8f46e9a3448f21ddb49f66f7e9
ms.sourcegitcommit: 8abe4a92b9d45e653c895787c69215c50a534529
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2022
ms.locfileid: "143998117"
---
# <a name="tutorial-create-a-custom-task-for-code-generation"></a>教程：创建用于代码生成的自定义任务

在本教程中，你将在 C# 中使用 MSBuild 创建自定义任务（用于处理代码生成），然后将在生成中使用该任务。 此示例演示如何使用 MSBuild 处理清理和重新生成操作。 该示例还演示如何支持增量生成，以便仅在输入文件发生更改时生成代码。 演示的技术适用于各种代码生成方案。 这些步骤还演示了如何使用 NuGet 打包任务以进行分发，并且本教程包含使用 BinLog 查看器改进故障排除体验的可选步骤。

## <a name="prerequisites"></a>先决条件

你应了解任务、目标和属性等 MSBuild 概念。 请参阅 [MSBuild 概念](msbuild-concepts.md)。

这些示例需要 MSBuild，它随 Visual Studio 一起安装，但也可以单独安装。 请参阅[下载 MSBuild 而不下载 Visual Studio](https://visualstudio.microsoft.com/downloads/?q=build+tools)。

## <a name="introduction-to-the-code-example"></a>代码示例简介

该示例采用包含要设置的值的输入文本文件，并创建包含用于创建这些值的代码的 C# 代码文件。 虽然这是一个简单的示例，但相同的基本技术适用于更复杂的代码生成方案。 

在本教程中，你将创建名为 AppSettingStronglyTyped 的 MSBuild 自定义任务。 该任务将读取一组文本文件，并且每个文件的各个行采用以下格式：

```
propertyName:type:defaultValue
```

代码生成包含所有常量的 C# 类。 问题应停止生成，并为用户提供足够的信息来诊断问题。

本教程的完整示例代码位于 GitHub 上的 .NET 示例存储库中的[自定义任务 - 代码生成](https://github.com/dotnet/samples/tree/main/msbuild/custom-task-code-generation)。

## <a name="create-the-appsettingstronglytyped-project"></a>创建 AppSettingStronglyTyped 项目

创建 .NET Standard 类库。 框架应为 .NET Standard 2.0。

请注意完整 MSBuild（Visual Studio 使用的那个 MSBuild）和可移植的 MSBuild（.NET Core 命令行中捆绑的那个 MSBuild）之间的差异。

- 完整 MSBuild：此版本的 MSBuild 通常位于 Visual Studio 中。 在 .NET Framework 上运行。 在解决方案或项目上执行“生成”时，Visual Studio 会使用此 MSBuild。 此版本也可从命令行环境（如 Visual Studio 开发人员命令提示符或 PowerShell）获得。
- .NET MSBuild：此版本的 MSBuild 捆绑在 .NET Core 命令行中。 它在 .NET Core 上运行。 Visual Studio 不会直接调用此版本的 MSBuild。 它仅支持使用 Microsoft .NET.Sdk 生成的项目。

如果要在 .NET Framework 和其他任何 .NET 实现（例如 .NET Core）之间共享代码，则库必须面向 [.NET Standard 2.0](/dotnet/standard/net-standard)，并且你希望在 Visual Studio 内部运行（在 .NET Framework 上运行）。 .NET Framework 不支持 .NET Standard 2.1。

## <a name="create-the-appsettingstronglytyped-msbuild-custom-task"></a>创建 AppSettingStronglyTyped MSBuild 自定义任务

第一步是创建 MSBuild 自定义任务。 有关如何[编写 MSBuild 自定义任务](task-writing.md)的信息可帮助你了解以下步骤。 MSBuild 自定义任务是一个实现 <xref:Microsoft.Build.Framework.ITask> 接口的类。

1. 添加对 _Microsoft.Build.Utilities.Core_ NuGet 包的引用，然后创建一个名为 AppSettingStronglyTyped 且派生自 Microsoft.Build.Utilities.Task 的类。

1. 添加三个属性。 这些属性定义用户在客户端项目中使用该任务时设置的参数：

    ```csharp
    //The name of the class which is going to be generated
    [Required]
    public string SettingClassName { get; set; }

    //The name of the namespace where the class is going to be generated
    [Required]
    public string SettingNamespaceName { get; set; }

    //List of files which we need to read with the defined format: 'propertyName:type:defaultValue' per line
    [Required]
    public ITaskItem[] SettingFiles { get; set; }
    ```

    该任务处理 SettingFiles 并生成类 `SettingNamespaceName.SettingClassName`。 生成的类将具有一组基于文本文件内容的常量。

    任务输出应为一个字符串，该字符串提供生成的代码的文件名：

    ```csharp
    // The filename where the class was generated
    [Output]
    public string ClassNameFile { get; set; }
    ```

1. 创建自定义任务时，继承自 <xref:Microsoft.Build.Utilities.Task?displayProperty=fullName>。 若要实现任务，请重写 <xref:Microsoft.Build.Utilities.Task.Execute> 方法。 如果任务成功，则 `Execute` 方法返回 `true`，否则返回 `false`。 `Task` 实现 <xref:Microsoft.Build.Framework.ITask?displayProperty=nameWithType>，并提供了一些 `ITask` 成员的默认实现，此外还提供了一些日志记录功能。 必须将状态输出到日志以诊断和排查任务问题，尤其是在出现问题且任务必须返回错误结果 (`false`) 时。 出错时，类通过调用 <xref:Microsoft.Build.Utilities.TaskLoggingHelper.LogError%2A?displayProperty=nameWithType> 来发出错误信号。

    ```csharp
    public override bool Execute()
    {
        //Read the input files and return a IDictionary<string, object> with the properties to be created. 
        //Any format error it will return false and log an error
        var (success, settings) = ReadProjectSettingFiles();
        if (!success)
        {
                return !Log.HasLoggedErrors;
        }
        //Create the class based on the Dictionary
        success = CreateSettingClass(settings);

        return !Log.HasLoggedErrors;
    }
    ```

    任务 API 允许返回 false，指示失败，而不向用户指示错误。 最好返回 `!Log.HasLoggedErrors` 而不是布尔代码，并在出错时记录错误。

### <a name="log-errors"></a>日志错误

记录错误时的最佳做法是在记录错误时提供详细信息（例如行号和不同的错误代码）。 以下代码分析文本输入文件，并结合使用 <xref:Microsoft.Build.Utilities.TaskLoggingHelper.LogError%2A?displayProperty=nameWithType> 方法和文本文件中生成错误的行号。

```csharp
private (bool, IDictionary<string, object>) ReadProjectSettingFiles()
{
    var values = new Dictionary<string, object>();
    foreach (var item in SettingFiles)
    {
        int lineNumber = 0;

        var settingFile = item.GetMetadata("FullPath");
        foreach (string line in File.ReadLines(settingFile))
        {
            lineNumber++;

            var lineParse = line.Split(':');
            if (lineParse.Length != 3)
            {
                Log.LogError(subcategory: null,
                             errorCode: "APPS0001",
                             helpKeyword: null,
                             file: settingFile,
                             lineNumber: lineNumber,
                             columnNumber: 0,
                             endLineNumber: 0,
                             endColumnNumber: 0,
                             message: "Incorrect line format. Valid format prop:type:defaultvalue");
                             return (false, null);
            }
            var value = GetValue(lineParse[1], lineParse[2]);
            if (!value.Item1)
            {
                return (value.Item1, null);
            }

            values[lineParse[0]] = value.Item2;
        }
    }
    return (true, values);
}
```

使用前面代码中所示的技术，文本输入文件的语法中的错误显示为生成错误，并包含有用的诊断信息：

```output
Microsoft (R) Build Engine version 17.2.0 for .NET Framework
Copyright (C) Microsoft Corporation. All rights reserved.

Build started 2/16/2022 10:23:24 AM.
Project "S:\work\msbuild-examples\custom-task-code-generation\AppSettingStronglyTyped\AppSettingStronglyTyped.Test\bin\Debug\net6.0\Resources\testscript-fail.msbuild" on node 1 (default targets).
S:\work\msbuild-examples\custom-task-code-generation\AppSettingStronglyTyped\AppSettingStronglyTyped.Test\bin\Debug\net6.0\Resources\error-prop.setting(1): error APPS0001: Incorrect line format. Valid format prop:type:defaultvalue [S:\work\msbuild-examples\custom-task-code-generation\AppSettingStronglyTyped\AppSettingStronglyTyped.Test\bin\Debug\net6.0\Resources\testscript-fail.msbuild]
Done Building Project "S:\work\msbuild-examples\custom-task-code-generation\AppSettingStronglyTyped\AppSettingStronglyTyped.Test\bin\Debug\net6.0\Resources\testscript-fail.msbuild" (default targets) -- FAILED.


Build FAILED.

"S:\work\msbuild-examples\custom-task-code-generation\AppSettingStronglyTyped\AppSettingStronglyTyped.Test\bin\Debug\net6.0\Resources\testscript-fail.msbuild" (default target) (1) ->
(generateSettingClass target) ->
  S:\work\msbuild-examples\custom-task-code-generation\AppSettingStronglyTyped\AppSettingStronglyTyped.Test\bin\Debug\net6.0\Resources\error-prop.setting(1): error APPS0001: Incorrect line format. Valid format prop:type:defaultvalue [S:\work\msbuild-examples\custom-task-code-generation\AppSettingStronglyTyped\AppSettingStronglyTyped.Test\bin\Debug\net6.0\Resources\testscript-fail.msbuild]

     0 Warning(s)
     1 Error(s)
```

捕获任务中的异常时，请使用 <xref:Microsoft.Build.Utilities.TaskLoggingHelper.LogErrorFromException%2A?displayProperty=nameWithType> 方法。 这将改进错误输出，例如通过获取引发异常的调用堆栈。

```csharp
    catch (Exception ex)
    {
        // This logging helper method is designed to capture and display information
        // from arbitrary exceptions in a standard way.
        Log.LogErrorFromException(ex, showStackTrace: true);
        return false;
    }
```

此处未显示使用这些输入为已生成的代码文件生成文本的其他方法的实现；请参阅示例存储库中的 [AppSettingStronglyTyped.cs](https://github.com/v-fearam/msbuild-examples/blob/main/custom-task-code-generation/AppSettingStronglyTyped/AppSettingStronglyTyped/AppSettingStronglyTyped.cs)。

示例代码在生成过程中生成 C# 代码。 任务与任何其他 C# 类类似，因此完成本教程后，可以对其进行自定义并添加自己的方案所需的任何功能。

## <a name="generate-a-console-app-and-use-the-custom-task"></a>生成控制台应用并使用自定义任务

在本部分中，你将创建一个使用该任务的标准 .NET Core 控制台应用。

> [!IMPORTANT]
> 避免在将要使用 MSBuild 的同一个 MSBuild 任务中生成 MSBuild 自定义任务非常重要。 新项目应位于完全不同的 Visual Studio 解决方案中，或者新项目使用从标准输出预生成并重定位的 dll。

1. 在新的 Visual Studio 解决方案中创建 .NET 控制台项目 MSBuildConsoleExample。

    分发任务的正常方式是通过 NuGet 包，但在开发和调试期间，你可以直接在应用程序的项目文件中包括有关 `.props` 和 `.targets` 的所有信息，然后在将任务分发给其他人时转为 NuGet 格式。

1. 修改项目文件以使用代码生成任务。 本部分中的代码列表显示引用任务、设置任务的输入参数以及编写用于处理清理和重新生成操作的目标后修改的项目文件，以便按预期删除生成的代码文件。

    任务是使用 [UsingTask 元素 (MSBuild)](usingtask-element-msbuild.md) 注册的。  `UsingTask` 元素注册任务；它告知 MSBuild 任务的名称以及如何查找和运行包含任务类的程序集。 程序集路径是项目文件的相对路径。  

    `PropertyGroup` 包含与任务中定义的属性相对应的属性定义。 这些属性是使用特性设置的，并且任务名称用作元素名称。

    `TaskName` 是要从程序集中引用的任务的名称。 此特性应始终使用完全指定的命名空间。 `AssemblyFile` 是程序集的文件路径。

    若要调用任务，请将任务添加到相应的目标（本例中为 `GenerateSetting`）。

    目标 `ForceGenerateOnRebuild` 通过删除生成的文件来处理清理和重新生成操作。 它设置为通过将 `AfterTargets` 特性设置为 `CoreClean` 在 `CoreClean` 目标后运行。

    ```xml
    <Project Sdk="Microsoft.NET.Sdk">
        <UsingTask TaskName="AppSettingStronglyTyped.AppSettingStronglyTyped" AssemblyFile="..\.   .\AppSettingStronglyTyped\AppSettingStronglyTyped\bin\Debug\netstandard2.0\AppSettingStronglyTyped.dll"/>

        <PropertyGroup>
            <OutputType>Exe</OutputType>
            <TargetFramework>net6.0</TargetFramework>
            <RootFolder>$(MSBuildProjectDirectory)</RootFolder>
            <SettingClass>MySetting</SettingClass>
            <SettingNamespace>MSBuildConsoleExample</SettingNamespace>
            <SettingExtensionFile>mysettings</SettingExtensionFile>
     </PropertyGroup>

     <ItemGroup>
         <SettingFiles Include="$(RootFolder)\*.mysettings" />
     </ItemGroup>`

     <Target Name="GenerateSetting" BeforeTargets="CoreCompile" Inputs="@(SettingFiles)" Outputs="$(RootFolder)\$(SettingClass).generated.cs">
         <AppSettingStronglyTyped SettingClassName="$(SettingClass)" SettingNamespaceName="$(SettingNamespace)" SettingFiles="@(SettingFiles)">
             <Output TaskParameter="ClassNameFile" PropertyName="SettingClassFileName" />
         </AppSettingStronglyTyped>
         <ItemGroup>
             <Compile Remove="$(SettingClassFileName)" />
             <Compile Include="$(SettingClassFileName)" />
         </ItemGroup>
     </Target>

     <Target Name="ForceReGenerateOnRebuild" AfterTargets="CoreClean">
         <Delete Files="$(RootFolder)\$(SettingClass).generated.cs" />
     </Target>
    </Project>
    ```

    > [!NOTE]
    > 此代码使用对目标[（BeforeTarget 和 AfterTarget）](target-build-order.md#beforetargets-and-aftertargets)进行排序的另一种方法，而不是重写目标（如 `CoreClean`）。 SDK 样式的项目在项目文件的最后一行后会隐式导入目标；这意味着无法重写默认目标，除非手动指定导入。 请参阅[重写预定义目标](how-to-extend-the-visual-studio-build-process.md#override-predefined-targets)。

    `Inputs` 和 `Outputs` 特性提供增量生成的信息，从而帮助 MSBuild 提高效率。 输入的日期与输出进行比较，以查看是否需要运行目标，或者是否可以重复使用上一个生成的输出。

1. 使用定义为已发现的扩展名创建输入文本文件。 使用默认扩展名，在根目录上创建 `MyValues.mysettings`，其中包含以下内容：

    ```
    Greeting:string:Hello World!
    ```

1. 再次生成，应创建并生成已生成的文件。 检查 MySetting.generated.cs 文件的项目文件夹。

1. 类 MySetting 位于错误的命名空间中，因此现在更改为使用应用命名空间。 打开项目文件并添加以下代码：

    ```xml
    <PropertyGroup>
        <SettingNamespace>MSBuildConsoleExample</SettingNamespace>
    </PropertyGroup>
    ```

1. 再次重新生成，并观察类是否位于 `MSBuildConsoleExample` 命名空间中。 通过这种方式，可以根据你的喜好重新定义生成的类名 (`SettingClass`)、要用作输入的文本扩展文件 (`SettingExtensionFile`) 及其位置 (`RootFolder`)。

1. 打开 Program.cs 并将硬编码的“Hello World!!” 更改为用户定义的常量：

    ```csharp
          static void Main(string[] args)
          {
                Console.WriteLine(MySetting.Greeting);
          }
    ```

执行程序；将打印生成的类中的问候语。

### <a name="optional-log-events-during-the-build-process"></a>（可选）在生成过程中记录事件

可以使用命令行命令进行编译。 导航到项目文件夹。 你将使用 `-bl`（二进制日志）选项生成二进制日志。 二进制日志会包含有用的信息，以了解生成过程中将发生的情况。

```dotnetcli
# Using dotnet MSBuild (run core environment)
dotnet build -bl

# or full MSBuild (run on net framework environment; this is used by Visual Studio)
msbuild -bl
```

这两个命令都生成日志文件 `msbuild.binlog`，可以使用 [MSBuild 二进制文件和结构化日志查看器](https://msbuildlog.com/)打开该文件。 选项 `/t:rebuild` 表示运行重新生成目标。 它将强制重新生成生成的代码文件。

恭喜！ 你已经生成了一个任务，该任务生成代码，并在生成中使用它。

## <a name="package-the-task-for-distribution"></a>打包任务以进行分发

如果只需在几个项目或单个解决方案中使用自定义任务，则只需将该任务用作原始程序集，但准备任务以将其用于其他位置或与他人共享的最佳方法就是作为 NuGet 包。

MSBuild 任务包与库 NuGet 包的一些主要区别如下：

- 它们必须捆绑自己的程序集依赖项，而不是将这些依赖项向使用的项目公开
- 它们不会将任何必需的程序集打包到 `lib/<target framework>` 文件夹中，因为这会导致 NuGet 将程序集包含在使用任务的任何包中
- 它们只需要针对 Microsoft.Build 程序集进行编译 - 在运行时，这些程序集将由实际的 MSBuild 引擎提供，因此无需包含在包中
- 它们会生成一个特殊的 `.deps.json` 文件，用于帮助 MSBuild 以一致的方式加载任务依赖项（尤其是本机依赖项）

若要实现所有这些目标，必须对上述和超出可能熟悉领域的标准项目文件进行一些更改。

### <a name="create-a-nuget-package"></a>创建 NuGet 包

推荐采用创建 NuGet 包这种方式将自定义任务分发给其他人。

#### <a name="prepare-to-generate-the-package"></a>准备生成包

若要准备生成 NuGet 包，请对项目文件进行一些更改，以指定描述包的详细信息。 你创建的初始项目文件类似于以下代码：

```xml
<Project Sdk="Microsoft.NET.Sdk">

    <PropertyGroup>
        <TargetFramework>netstandard2.0</TargetFramework>
    </PropertyGroup>

    <ItemGroup>
        <PackageReference Include="Microsoft.Build.Utilities.Core" Version="17.0.0" />
    </ItemGroup>

</Project>
```

若要生成 NuGet 包，请添加以下代码以设置包的属性。 可以在[包文档](/nuget/reference/msbuild-targets#pack-target)中查看受支持的 MSBuild 属性的完整列表：

```xml
<PropertyGroup>
    ... 
    <IsPackable>true</IsPackable>
    <Version>1.0.0</Version>
    <Title>AppSettingStronglyTyped</Title>
    <Authors>Your author name</Authors>
    <Description>Generates a strongly typed setting class base on a text file.</Description>
    <PackageTags>MyTags</PackageTags>
    <Copyright>Copyright ©Contoso 2022</Copyright>
    ...
</PropertyGroup>
```

#### <a name="mark-dependencies-as-private"></a>将依赖项标记为专用

MSBuild 任务的依赖项必须打包在包内；不能将其表示为普通的包引用。 包不会向外部用户公开任何常规依赖项。 这需要执行两个步骤来完成：将程序集标记为私有程序集，并将其实际嵌入到生成的包中。 对于此示例，我们将假设你的任务依赖于 `Microsoft.Extensions.DependencyInjection` 才能工作，因此请在版本 `6.0.0` 中将 `PackageReference` 添加到 `Microsoft.Extensions.DependencyInjection`。

```xml
<ItemGroup>
    <PackageReference 
        Include="Microsoft.Build.Utilities.Core"
        Version="17.0.0" />
    <PackageReference
        Include="Microsoft.Extensions.DependencyInjection"
        Version="6.0.0" />
</ItemGroup>
```

现在，请标记此任务项目的每个依赖项，`PackageReference` 和 `ProjectReference` 均标有 `PrivateAssets="all"` 特性。 这会告知 NuGet 完全不向使用的项目公开这些依赖项。 有关控制依赖项资产的详细信息，请参阅 [NuGet 文档](/nuget/consume-packages/package-references-in-project-files#controlling-dependency-assets)。

```xml
<ItemGroup>
    <PackageReference 
        Include="Microsoft.Build.Utilities.Core"
        Version="17.0.0"
        PrivateAssets="all"
    />
    <PackageReference
        Include="Microsoft.Extensions.DependencyInjection"
        Version="6.0.0"
        PrivateAssets="all"
    />
</ItemGroup>
```

#### <a name="bundle-dependencies-into-the-package"></a>将依赖项捆绑到包中

还必须将依赖项的运行时资产嵌入到任务包中。 这分为两个部分：一个 MSBuild 目标（用于将依赖项添加到 `BuildOutputInPackage` ItemGroup）和几个属性（用于控制这些 `BuildOutputInPackage` 项的布局）。 [NuGet 文档](/nuget/reference/msbuild-targets#targetsfortfmspecificbuildoutput)对此过程进行了详细介绍。

```xml
<PropertyGroup>
    ...
    <!-- This target will run when MSBuild is collecting the files to be packaged, and we'll implement it below. This property controls the dependency list for this packaging process, so by adding our custom property we hook ourselves into the process in a supported way. -->
    <TargetsForTfmSpecificBuildOutput>
        $(TargetsForTfmSpecificBuildOutput);CopyProjectReferencesToPackage
    </TargetsForTfmSpecificBuildOutput>
    <!-- This property tells MSBuild where the root folder of the package's build assets should be. Because we are not a library package, we should not pack to 'lib'. Instead, we choose 'tasks' by convention. -->
    <BuildOutputTargetFolder>tasks</BuildOutputTargetFolder>
    <!-- NuGet does validation that libraries in a package are exposed as dependencies, but we _explicitly_ do not want that behavior for MSBuild tasks. They are isolated by design. Therefore we ignore this specific warning. -->
    <NoWarn>NU5100</NoWarn>
    ...
</PropertyGroup>

...
<!-- This is the target we defined above. It's purpose is to add all of our PackageReference and ProjectReference's runtime assets to our package output.  -->
<Target
    Name="CopyProjectReferencesToPackage"
    DependsOnTargets="ResolveReferences">
    <ItemGroup>
        <!-- The TargetPath is the path inside the package that the source file will be placed. This is already precomputed in the ReferenceCopyLocalPaths items' DestinationSubPath, so reuse it here. -->
        <BuildOutputInPackage
            Include="@(ReferenceCopyLocalPaths)"
            TargetPath="%(ReferenceCopyLocalPaths.DestinationSubPath)" />
    </ItemGroup>
</Target>
```

#### <a name="dont-bundle-the-microsoftbuildutilitiescore-assembly"></a>不要捆绑 Microsoft.Build.Utilities.Core 程序集

如上所述，此依赖项将在运行时由 MSBuild 本身提供，因此我们不需要将其捆绑到包中。 为此，请将 `ExcludeAssets="Runtime"` 特性添加到它的 `PackageReference`

```xml
...
<PackageReference 
    Include="Microsoft.Build.Utilities.Core"
    Version="17.0.0"
    PrivateAssets="all"
    ExcludeAssets="Runtime"
/>
...
```

#### <a name="generate-and-embed-a-depsjson-file"></a>生成并嵌入 deps.json 文件

deps.json 文件可由 MSBuild 使用，以确保加载正确的依赖项版本。 需要添加一些 MSBuild 属性，以便生成文件，因为默认情况下不会为库生成该文件。 然后，添加一个目标以将其包含在包输出中，这与对包依赖项所执行的操作类似。

```xml
<PropertyGroup>
    ...
    <!-- Tell the SDK to generate a deps.json file -->
    <GenerateDependencyFile>true</GenerateDependencyFile>
    ...
</PropertyGroup>

...
<!-- This target adds the generated deps.json file to our package output -->
<Target
        Name="AddBuildDependencyFileToBuiltProjectOutputGroupOutput"
        BeforeTargets="BuiltProjectOutputGroup"
        Condition=" '$(GenerateDependencyFile)' == 'true'">

     <ItemGroup>
        <BuiltProjectOutputGroupOutput
            Include="$(ProjectDepsFilePath)"
            TargetPath="$(ProjectDepsFileName)"
            FinalOutputPath="$(ProjectDepsFilePath)" />
    </ItemGroup>
</Target>
```

### <a name="include-msbuild-properties-and-targets-in-a-package"></a>将 MSBuild 属性和目标包含到包中

有关此部分的背景信息，请阅读[属性和目标](customize-your-build.md)，然后了解如何[将属性和目标包含到 NuGet 包中](/nuget/create-packages/creating-a-package#include-msbuild-props-and-targets-in-a-package)。

在某些情况下，可能需要在使用包的项目中添加自定义生成目标或属性，例如生成期间运行自定义工具或进程。 通过将文件置于项目的 `build` 文件夹中的窗体 `<package_id>.targets` 或 `<package_id>.props` 中执行此操作。

项目根 build 文件夹中的文件被视为适用于所有目标框架。

在本部分中，你将关联 `.props` 和 `.targets` 文件中的任务实现，这些文件将包含在 NuGet 包中，并自动从引用项目加载。

1. 在任务的项目文件 AppSettingStronglyTyped.csproj 中，添加以下代码：

    ```xml
    <ItemGroup>
        <!-- these lines pack the build props/targets files to the `build` folder in the generated package.
            by convention, the .NET SDK will look for build\<Package Id>.props and build\<Package Id>.targets
            for automatic inclusion in the build. -->
        <Content Include="build\AppSettingStronglyTyped.props" PackagePath="build\" />
        <Content Include="build\AppSettingStronglyTyped.targets" PackagePath="build\" />
    </ItemGroup>
    ```

1. 创建 build 文件夹，在该文件夹中，添加两个文本文件：AppSettingStronglyTyped.props 和 AppSettingStronglyTyped.targets。 AppSettingStronglyTyped.props 很早便已导入 Microsoft.Common.props，因此它无法使用后来定义的属性。 因此，请避免引用尚未定义的属性；否则计算结果将为空。

    从 NuGet 包导入 `.targets` 文件后，会从 Microsoft.Common.targets 导入 Directory.Build.targets。 因此，它可以覆盖大多数生成逻辑中定义的属性和目标，或者为所有项目设置属性，而不考虑各个项目的设置。 请参阅[导入顺序](customize-your-build.md#import-order)。

    AppSettingStronglyTyped.props 包含任务并定义一些具有默认值的属性：

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <!--defining properties interesting for my task-->
    <PropertyGroup>
        <!--default directory where the .dll was publich inside a nuget package-->
        <taskForldername>lib</taskForldername>
        <taskFramework>netstandard2.0</taskFramework>
        <!--The folder where the custom task will be present. It points to inside the nuget package. -->
        <CustomTasksFolder>$(MSBuildThisFileDirectory)..\$(taskForldername)\$(taskFramework)</CustomTasksFolder>
        <!--Reference to the assembly which contains the MSBuild Task-->
        <CustomTasksAssembly>$(CustomTasksFolder)\$(MSBuildThisFileName).dll</CustomTasksAssembly>
    </PropertyGroup>

    <!--Register our custom task-->
    <UsingTask TaskName="$(MSBuildThisFileName).$(MSBuildThisFileName)" AssemblyFile="$(CustomTasksAssembly)"/>

    <!--Task parameters default values, this can be overridden-->
    <PropertyGroup>
        <RootFolder Condition="'$(RootFolder)' == ''">$(MSBuildProjectDirectory)</RootFolder>
        <SettingClass Condition="'$(SettingClass)' == ''">MySetting</SettingClass>
        <SettingNamespace Condition="'$(SettingNamespace)' == ''">example</SettingNamespace>
        <SettingExtensionFile Condition="'$(SettingExtensionFile)' == ''">mysettings</SettingExtensionFile>
    </PropertyGroup>
    </Project>
    ```

1. 安装包时，将自动包含 AppSettingStronglyTyped.props 文件。 然后，客户端具有可用的任务和一些默认值。 但从未使用过。 为了使此代码处于活动状态，请在 AppSettingStronglyTyped.targets 文件中定义一些目标，安装包时也会自动包含这些目标：

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <!--Defining all the text files input parameters-->
    <ItemGroup>
        <SettingFiles Include="$(RootFolder)\*.$(SettingExtensionFile)" />
    </ItemGroup>

    <!--A target that generates code, which is executed before the compilation-->
    <Target Name="BeforeCompile" Inputs="@(SettingFiles)" Outputs="$(RootFolder)\$(SettingClass).generated.cs">
        <!--Calling our custom task-->
        <AppSettingStronglyTyped SettingClassName="$(SettingClass)" SettingNamespaceName="$(SettingNamespace)" SettingFiles="@(SettingFiles)">
            <Output TaskParameter="ClassNameFile" PropertyName="SettingClassFileName" />
        </AppSettingStronglyTyped>
        <!--Our generated file is included to be compiled-->
        <ItemGroup>
            <Compile Remove="$(SettingClassFileName)" />
            <Compile Include="$(SettingClassFileName)" />
        </ItemGroup>
    </Target>

    <!--The generated file is deleted after a general clean. It will force the regeneration on rebuild-->
    <Target Name="AfterClean">
        <Delete Files="$(RootFolder)\$(SettingClass).generated.cs" />
    </Target>
    </Project>
    ```

    第一步是创建 [InputGroup](msbuild-items.md)，它表示要读取的文本文件（可以是多个），并且它将是我们的一些任务参数。 查找位置和扩展名存在默认值，但可以在客户端 MSBuild 项目文件中重写定义属性的值。

    然后，定义两个 [MSBuild 目标](msbuild-targets.md)。 我们将[扩展 MSBuild 过程](how-to-extend-the-visual-studio-build-process.md)，从而重写预定义的目标：

    - `BeforeCompile`：目标是调用自定义任务来生成类并包含要编译的类。 在完成核心编译之前，将插入此目标中的任务。 输入和输出字段与[增量生成](incremental-builds.md)相关。 如果所有输出项均为最新，MSBuild 就跳过目标。 目标的这种增量生成可以显著提高生成的性能。 如果某项的输出文件的时间戳与该项的一个或多个输入文件相同，或与之相比较新，则将该项视为最新。

    - `AfterClean`：目标是在发生常规清理之后删除生成的类文件。 调用核心清理功能后，将插入此目标中的任务。 在重新生成目标执行时强制重复执行代码生成步骤。

### <a name="generate-the-nuget-package"></a>生成 NuGet 包

若要生成 NuGet 包，可以使用 Visual Studio（右键单击“解决方案资源管理器”中的项目节点，然后选择“包”）。 还可以使用命令行执行此操作。 导航到任务项目文件 AppSettingStronglyTyped.csproj 所在的文件夹，然后执行以下命令：

```dotnetcli
// -o is to define the output; the following command chooses the current folder.
dotnet pack -o .
```

恭喜！ 已生成名为 \AppSettingStronglyTyped\AppSettingStronglyTyped\AppSettingStronglyTyped.1.0.0.nupkg 的 NuGet 包。

包具有扩展名 `.nupkg`，并且是压缩的 zip 文件。 可以使用 zip 工具打开它。 `.target` 和 `.props` 文件位于 `build` 文件夹中。 `.dll` 文件位于 `lib\netstandard2.0\` 文件夹中。 `AppSettingStronglyTyped.nuspec` 文件位于根级别。

## <a name="next-steps"></a>后续步骤

许多任务涉及调用可执行文件。 在某些情况下，可以使用 Exec 任务，但如果 Exec 任务的限制是一个问题，也可以创建自定义任务。 以下教程使用更真实的代码生成方案演示这两个选项：创建自定义任务以为 REST API 生成客户端代码。

> [!div class="nextstepaction"]
> [在生成中使用代码生成](tutorial-rest-api-client-msbuild.md)

或者，了解如何测试自定义任务。

> [!div class="nextstepaction"]
> [测试自定义 MSBuild 任务](tutorial-test-custom-task.md)
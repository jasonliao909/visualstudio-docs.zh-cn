---
title: T4 包含指令
description: 了解在 Visual Studio 的文本模板中，通过使用 <#@include#> 指令可包括来自另一个文件的文本。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: b8c88e1c6bcffda9c6bde4c740d233e4166787c9
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126663883"
---
# <a name="t4-include-directive"></a>T4 包含指令

在 Visual Studio 的文本模板中，通过使用 `<#@include#>` 指令可包括来自另一个文件的文本。 可以将 `include` 指令放置在文本模板中第一个类功能块 `<#+ ... #>` 前面的任何位置。 包含文件还可以包含 `include` 指令和其他指令。 这将允许你在模板之间共享模板代码和样本文本。

## <a name="using-include-directives"></a>使用 Include 指令

```
<#@ include file="filePath" [once="true"] #>
```

- `filePath` 可以是绝对的，或相对于当前模板文件。

   另外，特定 Visual Studio 扩展可以指定其自己的目录以便搜索包含文件。 例如，安装了可视化和建模 SDK（DSL 工具）后，以下文件夹将添加到包含列表：`Program Files\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft\DSL SDK\DSL Designer\11.0\TextTemplates`。

   这些附加包含文件夹可能取决于包含文件的文件扩展名。 例如，DSL 工具包含仅具有文件扩展名 `.tt` 的包含文件可访问的文件夹。

- `filePath` 可以包括用“%”分隔的环境变量。 例如：

  ```
  <#@ include file="%HOMEPATH%\MyIncludeFile.t4" #>
  ```

- 包含的文件的名称将不必使用扩展名 `".tt"`。

   你可能需要对包含的文件使用其他扩展名，例如，`".t4"`。 这是因为，在你将 `.tt` 文件添加到项目中时，Visual Studio 会自动将其“自定义工具”属性设置为 `TextTemplatingFileGenerator`。 你通常不希望单独转换包含的文件。

   另一方面，在某种情况下应注意，文件扩展名会影响将要搜索哪些附加文件夹来获得包含文件。 您具有包括其他文件的已包含文件时，这可能会很重要。

- 在处理时，被包含内容就像是包含文本模板的组成部分一样。 不过，即使 `<#+...#>` 指令后为普通文本块和标准控制块，也可以包括含有类功能块 `include` 的文件。

- 使用 `once="true"` 以确保一个模板只包括一次，即使从多个其他包含文件对其进行调用也是如此。

   使用此功能可轻松创建可重复使用的 T4 代码片段的库，你可以任意包括这些代码片段，而无需担心某些其他代码片段已包括了这些内容。  例如，假设你的库具有非常细小的代码片段，可用来进行模板处理和 C# 生成。  这些代码片段又由某些更专注于任务的实用工具使用（例如生成异常），而你又可以从任何更专注于应用程序的模板使用这些实用工具。 如果绘制依赖项关系图，则你会看到将会多次包含某些代码片段。 但 `once` 参数阻止后续包含。

  **MyTextTemplate.tt：**

```
<#@ output extension=".txt" #>
Output message 1 (from top template).
<#@ include file="TextFile1.t4"#>
Output message 5 (from top template).
<#
   GenerateMessage(6); // defined in TextFile1.t4
   AnotherGenerateMessage(7); // defined in TextFile2.t4
#>
```

 **TextFile1.t4：**

```
   Output Message 2 (from included file).
<#@ include file="TextFile2.t4" #>
   Output Message 4 (from included file).
<#+ // Start of class feature control block.
void GenerateMessage(int n)
{
#>
   Output Message <#= n #> (from GenerateMessage method).
<#+
}
#>
```

 **TextFile2.t4：**

```
        Output Message 3 (from included file 2).
<#+ // Start of class feature control block.
void AnotherGenerateMessage(int n)
{
#>
       Output Message <#= n #> (from AnotherGenerateMessage method).
<#+
}
#>
```

 **得到的已生成文件，MyTextTemplate.txt：**

```
Output message 1 (from top template).
   Output Message 2 (from included file).
        Output Message 3 (from included file 2).

   Output Message 4 (from included file).

Output message 5 (from top template).
   Output Message 6 (from GenerateMessage method).
       Output Message 7 (from AnotherGenerateMessage method).
```

## <a name="using-project-properties-in-msbuild-and-visual-studio"></a><a name="msbuild"></a> 在 MSBuild 和 Visual Studio 中使用项目属性
 虽然你可在 Include 指令中使用 Visual Studio 宏（如 $(SolutionDir)），但它们在 MSBuild 中不起作用。 如果你想要在生成计算机中转换模板，则必须改用项目属性。

 编辑 .csproj 或 .vbproj 文件以定义项目属性。 此示例定义一个名为 `myIncludeFolder` 的属性：

```xml
<!-- Define a project property, myIncludeFolder: -->
<PropertyGroup>
    <myIncludeFolder>$(MSBuildProjectDirectory)\..\libs</myIncludeFolder>
</PropertyGroup>

<!-- Tell the MSBuild T4 task to make the property available: -->
<ItemGroup>
    <T4ParameterValues Include="myIncludeFolder">
      <Value>$(myIncludeFolder)</Value>
    </T4ParameterValues>
  </ItemGroup>
```

 现在你可在文本模板中使用项目属性，此类模板将在 Visual Studio 和 MSBuild 中正确转换：

```
<#@ include file="$(myIncludeFolder)\defs.tt" #>
```

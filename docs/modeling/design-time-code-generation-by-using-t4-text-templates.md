---
title: 使用 T4 文本模板生成设计时代码
description: 了解如何使用设计时 T4 文本模板在 Visual Studio 项目中生成程序代码和其他文件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- text templates, guidelines for code generation
- text templates, data source model
- TextTemplatingFileGenerator custom tool
- Transform All Templates
- text templates, getting started
- Text Template project item
- text templates, generating code for your application
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: af199c1db5acafdf02139a652a13091547d7063e
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126671874"
---
# <a name="design-time-code-generation-by-using-t4-text-templates"></a>使用 T4 文本模板生成设计时代码

使用设计时 T4 文本模板，你可以在 Visual Studio 项目中生成程序代码和其他文件。 通常，你编写一些模板，以便它们根据来自模型的数据来改变所生成的代码。 模型是包含有关应用程序需求的关键信息的文件或数据库。

例如，你可能具有一个将工作流定义为表或关系图的模型。 可以从该模型生成执行工作流的软件。 当用户的需求变化时，可以很容易地与用户讨论新的工作流。 从工作流重新生成代码比手动更新代码更可靠。

> [!NOTE]
> 模型是描述应用程序特定方面的数据源。 它可以是任何形式、任何类型的文件或数据库。 它不必是任何特定形式，例如 UML 模型或域特定语言模型。 典型的模型是表或 XML 文件形式。

你可能已熟悉代码生成。 在 Visual Studio 解决方案中的 .resx 文件内定义资源时，将自动生成一组类和方法。 通过资源文件编辑资源比必须编辑类和方法要更加容易和可靠。 通过文本模板，可以使用相同的方式从自己设计的源中生成代码。

文本模板包含你要生成的文本以及用于生成文本的变量部分的程序代码。 程序代码允许你重复或有条件地省略部分已生成的文本。 生成的文本本身可以是将组成应用程序一部分的程序代码。

## <a name="create-a-design-time-t4-text-template"></a>创建设计时 T4 文本模板

1. 创建新的 Visual Studio 项目，或打开现有项目。

2. 向你的项目添加文本模板文件，并给予其带有扩展名 .tt 的名称。

    若要执行此操作，在“解决方案资源管理器”中，在你的项目的快捷菜单上，选择“添加” > “新建项目” 。 在“添加新项”对话框的中间窗格选择“文本模板”。

    请注意，该文件的“自定义工具”属性为“TextTemplatingFileGenerator”。

3. 打开 文件。 该文件中已包含下列指令：

   ```
   <#@ template hostspecific="false" language="C#" #>
   <#@ output extension=".txt" #>
   ```

    如果已将模板添加到 [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] 项目，则语言特性将为“`VB`”。

4. 在文件末尾添加一些文本。 例如：

   ```
   Hello, world!
   ```

5. 保存文件。

    你可能会看到一个“安全警告”消息框，要求确认要运行该模板。 单击 **“确定”** 。

6. 在“解决方案资源管理器”中，展开模板文件节点，你将找到带有扩展名 .txt 的文件。 该文件包含从该模板生成的文本。

   > [!NOTE]
   > 如果项目为 Visual Basic 项目，则必须单击“显示所有文件”才能看到输出文件。

### <a name="regenerate-the-code"></a>重新生成代码

在下列任何一种情况下，将执行模板，同时生成附属文件：

- 编辑该模板，然后将焦点更改到其他 Visual Studio 窗口。

- 保存模板。

- 单击“生成”菜单中的“转换所有模板”。 这将转换 Visual Studio 解决方案中的所有模板。

- 在“解决方案资源管理器”中，在任何文件的快捷菜单上，选择“运行自定义工具”。 使用此方法可以转换选定的模板子集。

还可以设置 Visual Studio 项目，以便在模板读取的数据文件更改时执行这些模板。 有关详细信息，请参阅[自动重新生成代码](#Regenerating)。

## <a name="generate-variable-text"></a>生成变量文本

通过文本模板，可以使用程序代码更改已生成文件的内容。

1. 更改 `.tt` 文件的内容：

   ```csharp
   <#@ template hostspecific="false" language="C#" #>
   <#@ output extension=".txt" #>
   <#int top = 10;

   for (int i = 0; i<=top; i++)
   { #>
      The square of <#= i #> is <#= i*i #>
   <# } #>
   ```

   ```vb
   <#@ template hostspecific="false" language="VB" #>
   <#@ output extension=".txt" #>
   <#Dim top As Integer = 10

   For i As Integer = 0 To top
   #>
       The square of <#= i #> is <#= i*i #>
   <#
   Next
   #>
   ```

2. 保存 .tt 文件，然后重新检查已生成的 .txt 文件。 该文件列出数字 0 到 10 的平方。

   请注意，语句括在 `<#...#>` 内，单个表达式括在 `<#=...#>` 内。 有关详细信息，请参阅[编写 T4 文本模板](../modeling/writing-a-t4-text-template.md)。

   如果在 [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] 中编写生成代码，则 `template` 指令应包含 `language="VB"`。 `"C#"` 为默认值。

## <a name="debugging-a-design-time-t4-text-template"></a>调试设计时 T4 文本模板

创建文本模板：

- 将 `debug="true"` 插入 `template` 指令。 例如：

   `<#@ template debug="true" hostspecific="false" language="C#" #>`

- 在模板中使用为普通代码设置断点的相同方式设置断点。

- 在“解决方案资源管理器”中，从文本模板文件的快捷菜单选择“调试 T4 模板”。

   模板在断点处运行和停止。 你可以以常用方式检查变量并逐步执行代码。

> [!TIP]
> `debug="true"` 使生成的代码图更精确地映射到文本模板，方法是在生成的代码中插入更多行号指令。 如果不使用它，断点可能在错误状态下停止运行。
>
> 但是，即使不在进行调试，你仍可将该子句留在模板指令中。 这仅会使性能下降一点点。

## <a name="generating-code-or-resources-for-your-solution"></a>生成解决方案的代码或资源

可以根据模型生成不同的程序文件。 模型是输入源，如数据库、配置文件、UML 模型、DSL 模型或其他源。 通常从同一模型生成多个程序文件。 为此，可为生成的每个程序文件创建一个模板文件，然后让所有模板读取同一模型。

### <a name="to-generate-program-code-or-resources"></a>生成程序代码或资源

1. 更改输出指令以生成相应类型（如 .cs、.vb、.resx 或 .xml）的文件。

2. 插入将生成所需解决方案代码的代码。 例如，如果要在一个类中生成三个整数字段声明，则插入以下代码：

    ```csharp

    <#@ template debug="false" hostspecific="false" language="C#" #>
    <#@ output extension=".cs" #>
    <# var properties = new string [] {"P1", "P2", "P3"}; #>
    // This is generated code:
    class MyGeneratedClass {
    <# // This code runs in the text template:
      foreach (string propertyName in properties)  { #>
      // Generated code:
      private int <#= propertyName #> = 0;
    <# } #>
    }
    ```

    ```vb
    <#@ template debug="false" hostspecific="false" language="VB" #>
    <#@ output extension=".cs" #>
    <# Dim properties = {"P1", "P2", "P3"} #>
    class MyGeneratedClass {
    <#
       For Each propertyName As String In properties
    #>
      private int <#= propertyName #> = 0;
    <#
       Next
    #>
    }

    ```

3. 保存该文件并检查生成的文件，生成的文件现在包含以下代码：

    ```csharp
    class MyGeneratedClass {
      private int P1 = 0;
      private int P2 = 0;
      private int P3 = 0;
    }
    ```

### <a name="generating-code-and-generated-text"></a>生成代码和生成的文本

生成程序代码时，最重要的是避免混淆以下代码：在模板中执行的生成代码，以及随之生成的将成为解决方案一部分的代码。 这两种语言不必相同。

上一个示例具有两个版本。 在一个版本中，生成代码采用 C#。 在另一个版本中，生成代码采用 Visual Basic。 但是这两个版本生成的文本是相同的，都是 C# 类。

通过相同方式，可以使用 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] 模板生成任何语言的代码。 生成的文本不必采用任何特定语言，并且不必是程序代码。

### <a name="structuring-text-templates"></a>结构化文本模板

作为一种良好做法，我们往往将模板代码分成两部分：

- 配置或数据收集部分，它在变量中设置值，但不包含文本块。 在上一个示例中，此部分是 `properties` 的初始化。

   此部分有时称为“模型”部分，因为它会构造一个存储内模型，并且通常读取模型文件。

- 文本生成部分（示例中的 `foreach(...){...}`），它使用变量的值。

   虽然这不是必要的分离，但是通过这种方式可以降低包括文本的部分的复杂性，从而更便于读取模板。

## <a name="reading-files-or-other-sources"></a>读取文件或其他源

若要访问模型文件或数据库，模板代码可以使用诸如 System.XML 之类的程序集。 若要获取对这些程序集的访问权限，必须插入如下指令：

```
<#@ assembly name="System.Xml.dll" #>
<#@ import namespace="System.Xml" #>
<#@ import namespace="System.IO" #>
```

`assembly` 指令使指定的程序集可供模板代码使用，方式与 Visual Studio 项目中的“引用”部分相同。 你无需包括对 System.dll 的引用，它是自动引用的。 `import` 指令允许你使用类型而不使用其完全限定名，方式与普通程序文件中的 `using` 指令相同。

例如，导入 System.IO 之后，可以编写：

```csharp

<# var properties = File.ReadLines("C:\\propertyList.txt");#>
...
<# foreach (string propertyName in properties) { #>
...
```

```vb
<# For Each propertyName As String In
             File.ReadLines("C:\\propertyList.txt")
#>
```

### <a name="opening-a-file-with-a-relative-pathname"></a>通过相对路径名打开文件

若要从相对于文本模板的位置加载文件，可以使用 `this.Host.ResolvePath()`。 若要使用 this.Host，你必须在 `hostspecific="true"` 中设置 `template`：

```
<#@ template debug="false" hostspecific="true" language="C#" #>
```

然后你可以进行编写，例如：

```csharp
<# string filename = this.Host.ResolvePath("filename.txt");
  string [] properties = File.ReadLines(filename);
#>
...
<#  foreach (string propertyName in properties { #>
...
```

```vb
<# Dim filename = Me.Host.ResolvePath("propertyList.txt")
   Dim properties = File.ReadLines(filename)
#>
...
<#   For Each propertyName As String In properties
...
#>
```

还可以使用 `this.Host.TemplateFile`，它标识当前模板文件的名称。

`this.Host` 的类型（在 VB 中是 `Me.Host`）是 `Microsoft.VisualStudio.TextTemplating.ITextTemplatingEngineHost`。

### <a name="getting-data-from-visual-studio"></a>从 Visual Studio 获取数据

若要使用 Visual Studio 中提供的服务，请设置 `hostSpecific` 属性并加载 `EnvDTE` 程序集。 导入 `Microsoft.VisualStudio.TextTemplating`，其中包含 `GetCOMService()` 扩展方法。  然后，你可以使用 IServiceProvider.GetCOMService() 访问 DTE 和其他服务。 例如：

```src
<#@ template hostspecific="true" language="C#" #>
<#@ output extension=".txt" #>
<#@ assembly name="EnvDTE" #>
<#@ import namespace="Microsoft.VisualStudio.TextTemplating" #>
<#
  IServiceProvider serviceProvider = (IServiceProvider)this.Host;
  EnvDTE.DTE dte = (EnvDTE.DTE) serviceProvider.GetCOMService(typeof(EnvDTE.DTE));
#>

Number of projects in this VS solution:  <#= dte.Solution.Projects.Count #>
```

> [!TIP]
> 文本模板在它自己的应用域中运行，并通过封送访问服务。 在此情况下，GetCOMService() 比 GetService() 更可靠。

## <a name="regenerating-the-code-automatically"></a><a name="Regenerating"></a> 自动重新生成代码

通常，Visual Studio 解决方案中的多个文件都使用一个输入模型生成。 每个文件从其自己的模板生成，但这些模板全都引用同一个模型。

如果源模型发生更改，则应重新运行该解决方案中的所有模板。 若要手动执行此操作，请选择“生成”菜单上的“转换所有模板”。

如果已安装 Visual Studio 建模 SDK，则可以在每次执行生成时自动转换所有模板。 为此，可在文本编辑器中编辑项目文件（.csproj 或 .vbproj），然后在文件末尾附近（其他任何 `<import>` 语句之后）添加以下行：

> [!NOTE]
> 安装 Visual Studio 的特定功能时，会自动安装文本模板转换 SDK 和 Visual Studio 建模 SDK。 有关更多详细信息，请参阅[这篇博客文章](https://devblogs.microsoft.com/devops/the-visual-studio-modeling-sdk-is-now-available-with-visual-studio-2017/)。

::: moniker range="vs-2017"

```xml
<Import Project="$(MSBuildExtensionsPath)\Microsoft\VisualStudio\v15.0\TextTemplating\Microsoft.TextTemplating.targets" />
<PropertyGroup>
   <TransformOnBuild>true</TransformOnBuild>
   <!-- Other properties can be inserted here -->
</PropertyGroup>
```

::: moniker-end

::: moniker range=">=vs-2019"

```xml
<Import Project="$(MSBuildExtensionsPath)\Microsoft\VisualStudio\v16.0\TextTemplating\Microsoft.TextTemplating.targets" />
<PropertyGroup>
   <TransformOnBuild>true</TransformOnBuild>
   <!-- Other properties can be inserted here -->
</PropertyGroup>
```

::: moniker-end

有关详细信息，请参阅[生成过程中的代码生成](../modeling/code-generation-in-a-build-process.md)。

## <a name="error-reporting"></a>错误报告

若要在 Visual Studio 错误窗口中放置错误消息和警告消息，可以使用以下方法：

```
Error("An error message");
Warning("A warning message");
```

## <a name="converting-an-existing-file-to-a-template"></a><a name="Converting"></a> 将现有文件转换为模板

模板的一个非常有用的功能是：它们看起来与其生成的文件（加上一些插入的程序代码）非常相似。 这暗示了创建模板的一种有用方法。 首先，创建一个普通的文件（如 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] 文件）作为原型，然后逐步引入可更改所生成文件的生成代码。

### <a name="to-convert-an-existing-file-to-a-design-time-template"></a>将现有文件转换为设计时模板

1. 对于你的 Visual Studio 项目，添加要生成的类型的文件，例如 `.cs`、`.vb` 或 `.resx` 文件。

2. 测试新文件以确保其工作。

3. 在解决方案资源管理器中，将文件扩展名更改为 .tt。

4. 验证 .tt 文件的以下属性：

   |Property |设置 |
   |-|-|
   | **自定义工具 =** | **TextTemplatingFileGenerator** |
   | **生成操作 =** | **无** |

5. 在文件开头插入以下行：

   ```
   <#@ template debug="false" hostspecific="false" language="C#" #>
   <#@ output extension=".cs" #>
   ```

    如果要以 [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] 编写模板的生成代码，请将 `language` 特性设置为 `"VB"`，而不是 `"C#"`。

    将 `extension` 特性设置为要生成的文件类型的文件扩展名，例如 `.cs`、`.resx` 或 `.xml`。

6. 保存文件。

    将使用指定扩展名创建一个附属文件。 该文件对于相应文件类型具有正确的属性。 例如，.cs 文件的“生成操作”属性将为“编译”。

    验证生成的文件是否包含与原始文件相同的内容。

7. 确定要更改的文件部分。 例如，一个仅在特定条件下显示的部分、一个重复的部分或特定值会有所变化的部分。 插入生成代码。 保存该文件，然后验证附属文件是否正确生成。 重复此步骤。

## <a name="guidelines-for-code-generation"></a>代码生成的准则

请参阅 [T4 文本模板编写准则](../modeling/guidelines-for-writing-t4-text-templates.md)。

## <a name="next-steps"></a>后续步骤

|后续步骤|主题|
|-|-|
|编写并调试更高级的文本模板，其中的代码使用辅助函数、包含的文件和外部数据。|[编写 T4 文本模板](../modeling/writing-a-t4-text-template.md)|
|在运行时从模板生成文档。|[使用 T4 文本模板的运行时文本生成](../modeling/run-time-text-generation-with-t4-text-templates.md)|
|在 Visual Studio 外运行文本生成。|[使用 TextTransform 实用工具生成文件](../modeling/generating-files-with-the-texttransform-utility.md)|
|以域特定语言的形式转换数据。|[从域特定语言生成代码](../modeling/generating-code-from-a-domain-specific-language.md)|
|编写指令处理器转换自己的数据源。|[自定义 T4 文本转换](../modeling/customizing-t4-text-transformation.md)|

## <a name="see-also"></a>另请参阅

- [T4 文本模板编写准则](../modeling/guidelines-for-writing-t4-text-templates.md)

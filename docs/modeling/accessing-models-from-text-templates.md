---
title: 从文本模板访问模型
description: 了解如何使用文本模板来创建基于域特定语言模型的报表文件、源代码文件和其他文本文件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- text templates, accessing models
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 451f9963b61d213b8aa95fe83ab68806d6c88bdc
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664792"
---
# <a name="access-models-from-text-templates"></a>从文本模板访问模型

使用文本模板，可以创建基于域特定语言模型的报表文件、源代码文件和其他文本文件。 有关文本模板的基本信息，请参阅[代码生成和 T4 文本模板](../modeling/code-generation-and-t4-text-templates.md)。 调试 DSL 时，文本模板将在实验模式下工作，并且还可在已部署 DSL 的计算机上工作。

> [!NOTE]
> 创建 DSL 解决方案时，调试项目中会生成示例文本模板 \*.tt 文件。 更改域类的名称时，这些模板将不再工作。 尽管如此，它们包括你需要的基本指令，并提供可更新以匹配 DSL 的示例。

 从文本模板访问模型：

- 将模板指令的 inherit 属性设置为 [Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation](/previous-versions/bb893209(v=vs.140))。 这将提供对 Store 的访问。

- 为要访问的 DSL 指定指令处理器。 这会加载 DSL 程序集，以便在文本模板的代码中使用其域类、属性和关系。 它还会加载你指定的模型文件。

  从 DSL 最小语言模板创建新 Visual Studio 解决方案时，将在调试项目中创建类似于以下示例的 `.tt` 文件。

```
<#@ template inherits="Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation" #>
<#@ output extension=".txt" #>
<#@ MyLanguage processor="MyLanguageDirectiveProcessor" requires="fileName='Sample.myDsl1'" #>

This text will be output directly.

This is the name of the model: <#= this.ModelRoot.Name #>

Here is a list of elements in the model:
<#
  // When you change the DSL Definition, some of the code below may not work.
  foreach (ExampleElement element in this.ExampleModel.Elements)
  {#>
<#= element.Name #>
<#
  }
#>
```

 请注意有关此模板的以下几点：

- 模板可以使用在 DSL 定义中定义的域类、属性和关系。

- 模板加载你在 `requires` 属性中指定的模型文件。

- `this` 中的属性包含根元素。 代码可以在其中导航到模型的其他元素。 属性名称通常与 DSL 的根域类相同。 在此示例中，它是 `this.ExampleModel`。

- 虽然编写代码片段的语言是 C#，但你可以生成任何类型的文本。 或者，可以通过将 `language="VB"` 属性添加到 `template` 指令，在 [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] 中编写代码。

- 若要调试模板，请将 `debug="true"` 添加到 `template` 指令。 如果发生异常，则模板将在 Visual Studio 的另一个实例中打开。 如果希望在代码中的特定点中断调试器，请插入语句 `System.Diagnostics.Debugger.Break();`

   有关详细信息，请参阅[调试 T4 文本模板](../modeling/debugging-a-t4-text-template.md)。

## <a name="about-the-dsl-directive-processor"></a>关于 DSL 指令处理器
 模板可以使用在 DSL 定义中定义的域类。 这是通过通常出现在模板开头附近的指令来进行的。 在上面的示例中，它如下所示。

```
<#@ MyLanguage processor="MyLanguageDirectiveProcessor" requires="fileName='Sample.myDsl1'" #>
```

 指令名称（在本例中为 `MyLanguage`）派生自 DSL 名称。 它调用作为 DSL 的一部分生成的指令处理器。 可以在 Dsl\GeneratedCode\DirectiveProcessor.cs 中找到它的源代码。

 DSL 指令处理器执行两个主要任务：

- 它有效地将程序集和导入指令插入到引用 DSL 的模板中。 这允许你在模板代码中使用域类。

- 它加载你在 `requires` 参数中指定的文件，并在 `this` 中设置一个引用所加载模型的根元素的属性。

## <a name="validating-the-model-before-running-the-template"></a>在运行模板之前验证模型
 可以在执行模板之前对模型进行验证。

```
<#@ MyLanguage processor="MyLanguageDirectiveProcessor" requires="fileName='Sample.myDsl1';validation='open|load|save|menu'" #>
```

 请注意：

1. `filename` 和 `validation` 参数用“;”分隔，并且不能有其他分隔符或空格。

2. 验证类别的列表确定将执行哪些验证方法。 应该用“&#124;”分隔多个类别，并且不得有其他分隔符或空格。

   如果发现错误，将在错误窗口中报告该错误，结果文件将包含错误消息。

## <a name="accessing-multiple-models-from-a-text-template"></a><a name="Multiple"></a> 从文本模板访问多个模型

> [!NOTE]
> 此方法使你可以读取同一模板中的多个模型，但不支持 ModelBus 引用。 若要读取由 ModelBus 引用链接的模型，请参阅[在文本模板中使用 Visual Studio ModelBus](../modeling/using-visual-studio-modelbus-in-a-text-template.md)。

 如果要从同一文本模板访问多个模型，则必须为每个模型调用一次生成的指令处理器。 必须在 `requires` 参数中指定每个模型的文件名。 必须在 `provides` 参数中指定要用于根域类的名称。 必须为每个指令调用中的 `provides` 参数指定不同值。 例如，假设有三个名为 Library.xyz、School.xyz 和 Work.xyz 的模型文件。 若要从同一文本模板访问它们，必须编写三个类似于下面的指令调用。

```
<#@ ExampleModel processor="<YourLanguageName>DirectiveProcessor" requires="fileName='Library.xyz'" provides="ExampleModel=LibraryModel" #>
<#@ ExampleModel processor="<YourLanguageName>DirectiveProcessor" requires="fileName='School.xyz'" provides="ExampleModel=SchoolModel" #>
<#@ ExampleModel processor="<YourLanguageName>DirectiveProcessor" requires="fileName='Work.xyz'" provides="ExampleModel=WorkModel" #>
```

> [!NOTE]
> 此代码示例适用于基于最小语言解决方案模板的语言。

 若要访问文本模板中的模型，你现在可以编写类似于以下示例代码的代码。

```csharp
<#
foreach (ExampleElement element in this.LibraryModel.Elements)
...
foreach (ExampleElement element in this.SchoolModel.Elements)
...
foreach (ExampleElement element in this.WorkModel.Elements)
...
#>
```

```vb
<#
For Each element As ExampleElement In Me.LibraryModel.Elements
...
For Each element As ExampleElement In Me.SchoolModel.Elements
...
For Each element As ExampleElement In Me.WorkModel.Elements
...
#>
```

## <a name="loading-models-dynamically"></a>动态加载模型
 如果要在运行时确定要加载的模型，可以在程序代码中动态加载模型文件，而不是使用特定于 DSL 的指令。

 但是，特定于 DSL 的指令的功能之一是导入 DSL 命名空间，以便模板代码可以使用该 DSL 中定义的域类。 由于未使用指令，因此必须为可能加载的所有模型添加 \<assembly> 和 \<import> 指令。 如果可以加载的不同模型都是同一 DSL 的所有实例，那么这很简单。

 若要加载该文件，最有效的方法是使用 Visual Studio ModelBus。 在典型场景中，文本模板将使用特定于 DSL 的指令以常规方式加载第一个模型。 该模型将包含对另一个模型的 ModelBus 引用。 可以使用 ModelBus 打开引用的模型并访问特定元素。 有关详细信息，请参阅[在文本模板中使用 Visual Studio ModelBus](../modeling/using-visual-studio-modelbus-in-a-text-template.md)。

 在不太常见的情况下，你可能想要打开一个只具有文件名且不在当前 Visual Studio 项目中的模型文件。 在这种情况下，可以使用[操作说明：在程序代码中从文件打开模型](../modeling/how-to-open-a-model-from-file-in-program-code.md)中所述的方法来打开文件。

## <a name="generating-multiple-files-from-a-template"></a>从模板生成多个文件
 如果要生成几个文件（例如，为模型中的每个元素生成一个单独的文件），则有几种可能的方法。 默认情况下，每个模板文件仅生成一个文件。

### <a name="splitting-a-long-file"></a>拆分长文件
 在此方法中，你将使用一个模板生成单个文件，并用分隔符分隔。 然后，将文件拆分为其各个部分。 有两个模板，一个用于生成单个文件，另一个用于拆分。

 LoopTemplate.t4 生成单个长文件。 请注意，其文件扩展名为“.t4”，因为当你单击“转换所有模板”时不应直接处理。 此模板采用参数，该参数指定分隔段的分隔符字符串：

```
<#@ template ninherits="Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation" #>
<#@ parameter name="delimiter" type="System.String" #>
<#@ output extension=".txt" #>
<#@ MyDSL processor="MyDSLDirectiveProcessor" requires="fileName='SampleModel.mydsl1';validation='open|load|save|menu'" #>
<#
  // Create a file segment for each element:
  foreach (ExampleElement element in this.ExampleModel.Elements)
  {
    // First item is the delimiter:
#>
<#= string.Format(delimiter, element.Id) #>

   Element: <#= element.Name #>
<#
   // Here you generate more content derived from the element.
  }
#>
```

 `LoopSplitter.tt` 调用 `LoopTemplate.t4`，然后将生成的文件拆分为其各个段。 请注意，此模板不必是建模模板，因为它不会读取模型。

```
<#@ template hostspecific="true" language="C#" #>
<#@ output extension=".txt" #>
<#@ import namespace="Microsoft.VisualStudio.TextTemplating" #>
<#@ import namespace="System.Runtime.Remoting.Messaging" #>
<#@ import namespace="System.IO" #>

<#
  // Get the local path:
  string itemTemplatePath = this.Host.ResolvePath("LoopTemplate.t4");
  string dir = Path.GetDirectoryName(itemTemplatePath);

  // Get the template for generating each file:
  string loopTemplate = File.ReadAllText(itemTemplatePath);

  Engine engine = new Engine();

  // Pass parameter to new template:
  string delimiterGuid = Guid.NewGuid().ToString();
  string delimiter = "::::" + delimiterGuid + ":::";
  CallContext.LogicalSetData("delimiter", delimiter + "{0}:::");
  string joinedFiles = engine.ProcessTemplate(loopTemplate, this.Host);

  string [] separateFiles = joinedFiles.Split(new string [] {delimiter}, StringSplitOptions.None);

  foreach (string nameAndFile in separateFiles)
  {
     if (string.IsNullOrWhiteSpace(nameAndFile)) continue;
     string[] parts = nameAndFile.Split(new string[]{":::"}, 2, StringSplitOptions.None);
     if (parts.Length < 2) continue;
#>
 Generate: [<#= dir #>] [<#= parts[0] #>]
<#
     // Generate a file from this item:
     File.WriteAllText(Path.Combine(dir, parts[0] + ".txt"), parts[1]);
  }
#>
```

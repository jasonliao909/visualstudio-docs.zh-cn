---
title: 代码生成和 T4 文本模板
description: 了解 T4 文本模板如何成为文本块与可生成文本文件的控制逻辑的混合体。
ms.custom: SEO-VS-2020, devdivchpfy22
ms.date: 12/28/2021
ms.topic: overview
f1_keywords:
- VS.ToolsOptionsPages.TextTemplating.TextTemplating
helpviewer_keywords:
- generating text
- .tt files
- code generation
- text templates
- generating code
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 950cadad3444fa62f272bb6ea64eb8317fe43a62
ms.sourcegitcommit: 965372ad0d75f015403c1af508080bf799914ce3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2022
ms.locfileid: "135803877"
---
# <a name="code-generation-and-t4-text-templates"></a>代码生成和 T4 文本模板

在 Visual Studio 中，T4 文本模板是文本块与可生成文本文件的控制逻辑的混合体。 控制逻辑被编写为 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] 或 [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]中的程序代码的片段。 使用 Visual Studio 2015 Update 2 及更高版本时，可在 T4 模板指令中使用 C# 6.0 版功能。 生成的文件可以是文本，例如网页、资源文件或任何语言的程序源代码。

对于特定于域 (DSL) ，旨在表达特定问题空间中的语句，了解如何从特定语言生成 [Domain-Specific代码](../modeling/generating-code-from-a-domain-specific-language.md)

有两种类型的 T4 文本模板[：运行时和](#run-time-t4-text-templates)[设计时间](#design-time-t4-text-templates)

## <a name="run-time-t4-text-templates"></a>运行时 T4 文本模板

运行时模板也称为"预处理"模板。 在应用程序中运行模板，以在其输出中生成文本字符串。 例如，可以创建一个模板来定义 HTML 页面：

```
<html><body>
 The date and time now is: <#= DateTime.Now #>
</body></html>
```

注意：该模板与生成的输出类似。 该模版与生成的输出的相似性有助于避免在想要更改时出现错误。

此外，该模板包含程序代码的片段。 你可使用这些片段来重复文本节、创建条件节以及显示应用程序数据。

若要生成输出，应用程序将调用由此模板生成的函数。 例如：

```csharp
string webResponseText = new MyTemplate().TransformText();
```

应用程序可以在未安装Visual Studio运行。

若要创建运行时模板，将“预处理过的文本模板”  文件添加到你的项目中。 还可以添加纯文本文件， **将其自定义工具** 属性设置为 **TextTemplatingFilePreprocessor**。

有关详细信息，请参阅[使用 T4 文本模板的运行时文本生成](../modeling/run-time-text-generation-with-t4-text-templates.md)。 有关模板语法的详细信息，请参阅[编写 T4 文本模板](../modeling/writing-a-t4-text-template.md)。

## <a name="design-time-t4-text-templates"></a>设计时 T4 文本模板

设计时模板用于定义部分源代码以及应用程序的其他资源。 通常，可以使用多个模板读取单个输入文件或数据库中的数据，并生成一些 *.cs、.vb* 或其他源文件。 每个模板都会生成一个文件，并生成Visual Studio或MSBuild。

例如，输入数据可能是配置数据的 XML 文件。 每当在开发过程中编辑 XML 文件时，文本模板都会重新生成部分应用程序代码。 其中一个模板可能类似于以下示例：

```
<#@ output extension=".cs" #>
<#@ assembly name="System.Xml" #>
<#
 System.Xml.XmlDocument configurationData = ...; // Read a data file here.
#>
namespace Fabrikam.<#= configurationData.SelectSingleNode("jobName").Value #>
{
  ... // More code here.
}
```

生成的 *.cs* 文件基于 XML 文件值采用以下格式：

```
namespace Fabrikam.FirstJob
{
  ... // More code here.
}
```

再如，该输入可能是业务活动中的工作流关系图。 当用户更改其业务工作流时，或者当你开始与工作流不同的新用户合作时，可以轻松重新生成代码以适应新模型。

> [!NOTE]
> 术语 *“模型”* 有时用来描述由一个或多个模板所读取的数据。 该模型可以是任何格式、任何类型的文件或数据库。 而不必是 UML 模型或域特定语言模型。 “模型”仅表示可以业务概念的形式定义的数据，而不是类似的代码。
当需求发生变化时，更改配置时，设计时模板更快、更可靠。 通常，输入是按照业务需求定义的，如工作流示例中所示。 设计时模板是敏捷开发过程中有用的工具。

若要创建运行时模板，请将“文本模版”  文件添加到你的项目中。 或者，你也可以添加一个纯文本文件，并将其“自定义工具”  属性设置为 **TextTemplatingFileGenerator**。

有关详细信息，请参阅[使用 T4 文本模板生成设计时代码](../modeling/design-time-code-generation-by-using-t4-text-templates.md)。 有关模板语法的详细信息，请参阅[编写 T4 文本模板](../modeling/writing-a-t4-text-template.md)。

文本模板转换功能命名为 *T4*。

## <a name="see-also"></a>另请参阅

- [从域特定语言生成代码](../modeling/generating-code-from-a-domain-specific-language.md)

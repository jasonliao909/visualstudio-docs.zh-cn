---
title: '如何：使用文本模板 ... '
description: 了解使用文本模板生成文本时遇到的常见问题的解答。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: ab0aa917f79845b7baaad4c65583a5a5a07853f4feec28cab7de9646751aaf3b
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121429142"
---
# <a name="how-to--with-text-templates"></a>如何：使用文本模板 ... 
文本模板Visual Studio生成任何类型的文本的有用方法。 可以使用文本模板在应用程序的一部分运行时生成文本，在设计时生成一些项目代码。 本主题汇总了最常询问的"如何实现 ...？" 问题。

 在本主题中，前面带有项目符号的多个答案是替代建议。

 有关文本模板的一般介绍，请阅读 [代码生成和 T4 文本模板](../modeling/code-generation-and-t4-text-templates.md)。

## <a name="how-to-"></a>如何。。。

### <a name="generate-part-of-my-application-code"></a>生成部分应用程序代码
 文件或数据库中 *有* 一个配置或模型。 代码的一个或多个部分依赖于该模型。

- 从文本模板生成一些代码文件。 有关详细信息，请参阅使用[T4](../modeling/design-time-code-generation-by-using-t4-text-templates.md)文本模板设计时代码生成和开始编写模板[的最佳方法是什么？。](#starting)

### <a name="generate-files-at-run-time-passing-data-into-the-template"></a>运行时生成文件，将数据传递到模板
 运行时，我的应用程序会生成包含标准文本和数据混合的文本文件，例如报表。 我想要避免编写数百个 `write` 语句。

- 将运行时文本模板添加到项目。 此模板在代码中创建一个类，可以实例化该类并使用它来生成文本。 可以在构造函数参数中将数据传递给它。 有关详细信息，请参阅[使用 T4 文本模板的运行时文本生成](../modeling/run-time-text-generation-with-t4-text-templates.md)。

- 如果要从仅运行时可用的模板生成 ，可以使用标准文本模板。 如果要编写一个Visual Studio扩展，可以调用文本模板化服务。 有关详细信息，请参阅调用 [VS 扩展中的文本转换](../modeling/invoking-text-transformation-in-a-vs-extension.md)。 在其他上下文中，可以使用文本模板化引擎。 有关详细信息，请参阅 <xref:Microsoft.VisualStudio.TextTemplating.Engine?displayProperty=fullName>。

     使用 \<#@parameter#> 指令将参数传递给这些模板。 有关详细信息，请参阅 [T4 参数指令](../modeling/t4-parameter-directive.md)。

### <a name="read-another-project-file-from-a-template"></a>从模板中读取另一个项目文件
 从模板的同一Visual Studio读取文件：

- 将 `hostSpecific="true"` 插入 `<#@template#>` 指令。

     在代码中，使用 `this.Host.ResolvePath(filename)` 获取文件的完整路径。

### <a name="invoke-methods-from-a-template"></a>从模板调用方法

如果方法已存在，例如，在 .NET 类中：

- 使用 \<#@assembly#> 指令加载程序集，并使用 \<#@import#> 设置命名空间上下文。 有关详细信息，请参阅 [T4 Import 指令](../modeling/t4-import-directive.md)。

   如果经常使用同一组程序集和导入指令，请考虑编写指令处理器。 在每个模板中，可以调用指令处理器，该处理器可以加载程序集和模型文件并设置命名空间上下文。 有关详细信息，请参阅创建自定义 [T4 文本模板指令处理器](../modeling/creating-custom-t4-text-template-directive-processors.md)。

如果正在自己编写方法：

- 如果要编写运行时文本模板，请编写与运行时文本模板同名的分部类定义。 将其他方法添加到此类中。

- 编写类功能控制块 `<#+ ... #>` ，可在其中声明方法、属性和私有类。 编译文本模板时，该模板将转换为类。 标准控制块 `<#...#>` 和文本转换为单个方法，类功能块作为单独的成员插入。 有关详细信息，请参阅 [文本模板控件块](../modeling/text-template-control-blocks.md)。

   定义为类功能的方法还可以包括嵌入的文本块。

   请考虑将类功能放在一个单独的文件中，你可以将其 `<#@include#>` 放入一个或多个模板文件中。

- 将方法写入类库 (程序集中) ，然后从模板调用这些方法。 使用 `<#@assembly#>` 指令加载程序集，并 `<#@import#>` 设置命名空间上下文。 请注意，若要在调试程序集时重新生成程序集，可能需要停止并重启Visual Studio。 有关详细信息，请参阅 [T4 文本模板指令](../modeling/t4-text-template-directives.md)。

### <a name="generate-many-files-from-one-model-schema"></a>从一个模型架构生成多个文件
 如果经常从具有相同的 XML 或数据库架构的模型生成文件：

- 请考虑编写指令处理器。 这使你可以将每个模板中的多个程序集语句和导入语句替换为单个自定义指令。 指令处理器还可以加载和分析模型文件。 有关详细信息，请参阅创建自定义 [T4 文本模板指令处理器](../modeling/creating-custom-t4-text-template-directive-processors.md)。

### <a name="generate-files-from-a-complex-model"></a>从复杂模型生成文件

- 请考虑使用 DSL (域) 语言来表示模型。 这样，可以更轻松地编写模板，因为使用反映模型中元素名称的类型和属性。 不需要分析文件或导航 XML 节点。 例如：

     `foreach (Book book in this.Library) { ... }`

     有关详细信息，请参阅 入门 [语言Domain-Specific](../modeling/getting-started-with-domain-specific-languages.md) 语言和从语言生成 [Domain-Specific代码](../modeling/generating-code-from-a-domain-specific-language.md)。

### <a name="get-data-from-visual-studio"></a>从数据Visual Studio
 若要使用 Visual Studio 中提供的服务，请设置 `hostSpecific` 属性并加载 `EnvDTE` 程序集。 例如：

```csharp
<#@ template hostspecific="true" language="C#" #>
<#@ output extension=".txt" #>
<#@ assembly name="EnvDTE" #>
<#
  IServiceProvider serviceProvider = (IServiceProvider)this.Host;
  EnvDTE.DTE dte = (EnvDTE.DTE) serviceProvider.GetService(typeof(EnvDTE.DTE));
#>

Number of projects in this VS solution:  <#= dte.Solution.Projects.Count #>
```

### <a name="execute-text-templates-in-the-build-process"></a>在生成过程中执行文本模板

- 有关详细信息，请参阅生成 [过程中的代码生成](../modeling/code-generation-in-a-build-process.md)。

## <a name="more-general-questions"></a>更多常规问题

### <a name="what-is-the-best-way-to-start-writing-a-text-template"></a><a name="starting"></a> 开始编写文本模板的最佳方法是什么？

1. 编写生成的文件的特定示例。

2. 通过插入 指令以及加载输入文件或模型所需的指令和代码，将其转换为 `<#@template #>` 文本模板。

3. 以渐进方式将文件的某些部分替换为表达式和代码块。

### <a name="what-is-a-model"></a>什么是“模型”？

- 模板读取的输入。 它可以在文件或数据库中。 它可以是 XML、Visio图形、特定于域的语言 (DSL) 或 UML 模型，或者可能是纯文本。 它可以分布在多个文件中。 通常，多个模板读取一个模型。

     术语"模型"的含义是，它比生成的程序代码或其他文件更直接地表示业务某些方面。 例如，它可能表示生成的软件将监督的通信网络的计划。

### <a name="what-is-the-benefit-of-using-text-templates"></a>使用文本模板的好处是什么？
 通常，从一个模型生成多个代码或其他文件。 模型比生成的代码更直接地表示要求。 它省略实现详细信息，并按要求而不是代码编写。 当需求发生变化时（就像它们通常一样）可以比程序代码的不同部分更轻松、更可靠地更新模型。

 因此，从敏捷开发方法的角度来看，代码生成是一种有价值的工具。

### <a name="what-best-practices-are-there-for-text-templates"></a>文本模板有什么"最佳做法"？

- 有关详细信息，请参阅编写 [T4 文本模板的准则](../modeling/guidelines-for-writing-t4-text-templates.md)。

### <a name="what-is-t4"></a>什么是"T4"？

- 此处所述的Visual Studio模板功能的另一个名称。 以前的版本未发布，是"文本模板转换"的缩写。

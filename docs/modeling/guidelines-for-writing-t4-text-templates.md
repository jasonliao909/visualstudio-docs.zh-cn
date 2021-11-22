---
title: T4 文本模板编写准则
description: 了解在 Visual Studio 中生成程序代码或其他应用程序资源时可能有用的一般准则。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: b0cb319b488bf080b95ce2651ccf21bad3c33d6a
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664169"
---
# <a name="guidelines-for-writing-t4-text-templates"></a>T4 文本模板编写准则

如果要在 Visual Studio 中生成程序代码或其他应用程序资源，这些一般准则可能有用。 它们不是固定规则。

## <a name="guidelines-for-design-time-t4-templates"></a>设计时 T4 模板准则

设计时 T4 模板是指在设计时在 Visual Studio 项目中生成代码的模板。 有关详细信息，请参阅[使用 T4 文本模板生成设计时代码](../modeling/design-time-code-generation-by-using-t4-text-templates.md)。

生成应用程序的可变方面。

对于可能在项目期间更改或者将在应用程序的不同版本之间更改的应用程序方面，代码生成最有用。 将这些可变方面与更多固定方面分开，以便更轻松地确定必须生成的内容。 例如，如果应用程序提供网站，则将提供标准页面的功能与定义从一个页面到另一个页面的导航路径的逻辑分离。

在一个或多个源模型中对可变方面进行编码。

模型是每个模板读取以获取要生成的代码可变部分的特定值的文件或数据库。 模型可以是数据库、你自己设计的 XML 文件、关系图或域特定语言。 通常，一个模型用于在一个 Visual Studio 项目中生成多个文件。 每个文件都是从单独的模板生成的。

可以在项目中使用多个模型。 例如，可以定义一个在网页之间导航的模型，以及一个单独的页面布局模型。

将模型聚焦于用户需求和词汇上，而不是实现上。

例如，在网站应用程序中，模型应引用网页和超链接。

理想情况下，选择适合模型表示的信息类型的表示形式。 例如，在网站中导航的路径模型可以是框和箭头的关系图。

测试生成的代码。

使用手动或自动测试验证生成的代码是否按用户需求运行。 避免从生成代码的同一模型生成测试。

在某些情况下，可以直接对模型执行常规测试。 例如，可以编写一个测试，确保可以通过从任何其他页面导航来访问网站的每个页面。

允许自定义代码：生成分部类。

除生成的代码外，还允许手动编写的代码。 代码生成方案无法考虑到可能出现的所有可能的变体。 因此，应该会添加或替代某些生成的代码。 当生成的材料采用 .NET 语言（如 C# 或 Visual Basic）时，两种策略特别有用：

- 生成的类应为分部类。 这样，你可以将内容添加到生成的代码中。

- 类应成对生成，一个继承自另一个。 基类应包含所有生成的方法和属性，派生类应仅包含构造函数。 这允许手动编写的代码替代任何生成的方法。

在其他生成的语言（如 XML）中，请使用 `<#@include#>` 指令进行手动编写和生成内容的简单组合。 在更复杂的情况下，可能需要编写一个后处理步骤，将生成的文件与任何手动编写的文件组合在一起。

将常用材料移动到包含文件或运行时模板中。

为了避免在多个模板中重复类似的文本块和代码块，请使用 `<#@ include #>` 指令。 有关详细信息，请参阅 [T4 包含指令](../modeling/t4-include-directive.md)。

还可以在单独的项目中生成运行时文本模板，然后从设计时模板调用它们。 为此，请使用 `<#@ assembly #>` 指令访问单独的项目。

请考虑将大型代码块移动到单独的程序集中。

如果具有大型代码块和类功能块，将其中一些代码移动到在单独的项目中编译的方法可能很有用。 可以使用 `<#@ assembly #>` 指令访问模板中的代码。 有关详细信息，请参阅 [T4 程序集指令](../modeling/t4-assembly-directive.md)。

可以将方法放在模板可以继承的抽象类中。 抽象类必须从 <xref:Microsoft.VisualStudio.TextTemplating.TextTransformation?displayProperty=fullName> 继承。 有关详细信息，请参阅 [T4 模板指令](../modeling/t4-template-directive.md)。

生成代码，而非配置文件。

编写可变应用程序的一个方法是编写接受配置文件的通用程序代码。 采用这种方式编写的应用程序非常灵活，可以在业务需求更改时重新配置，而无需重新生成应用程序。 但是，此方法的缺点是应用程序的执行性能不如更特定的应用程序。 此外，其程序代码将更难读取和维护，部分原因在于它始终必须处理大多数泛型类型。

相比之下，在编译之前生成其可变部分的应用程序可以进行强类型化。 这使得编写手动编写的代码并将其与软件生成的部分集成变得更加简单且更可靠。

若要获得代码生成的全部优势，请尝试生成程序代码而不是配置文件。

使用“生成的代码”文件夹。

将模板和生成的文件放在名为“生成的代码”的项目文件夹中，以表明这些文件不应直接编辑。 如果创建自定义代码以替代或添加到生成的类，请将这些类放在名为“自定义代码”的文件夹中。 典型项目的结构如下所示：

```
MyProject
   Custom Code
      Class1.cs
      Class2.cs
   Generated Code
      Class1.tt
          Class1.cs
      Class2.tt
          Class2.cs
   AnotherClass.cs
```

## <a name="guidelines-for-run-time-preprocessed-t4-templates"></a>运行时（已预处理）T4 模板准则

将常用材料移动到继承的模板中。

可以使用继承在 T4 文本模板之间共享方法和文本块。 有关详细信息，请参阅 [T4 模板指令](../modeling/t4-template-directive.md)。

还可使用具有运行时模板的包含文件。

将大型代码正文移动到分部类中。

每个运行时模板都会生成一个与模板同名的分部类定义。 可以编写包含同一类的另一分部定义的代码文件。 可以采用此方式向类中添加方法、字段和构造函数。 可以从模板中的代码块调用这些成员。

这样做的一个优点是代码更易于编写，因为 IntelliSense 可用。 此外，还可以在表示与基础逻辑之间实现更好的分离。

例如，在 MyReportText.tt 中：

`The total is: <#= ComputeTotal() #>`

在 MyReportText-Methods.cs 中：

`private string ComputeTotal() { ... }`

允许自定义代码：提供扩展点。

请考虑在 \<#+ class feature blocks #> 中生成虚拟方法。 这允许在多个上下文中使用单个模板，而无需修改。 可以构造提供最小附加逻辑的派生类，而不是修改模板。 派生类可以是常规代码，也可以是运行时模板。

例如，在 MyStandardRunTimeTemplate.tt 中：

```
This page is copyright <#= CompanyName() #>.
<#+ protected virtual string CompanyName() { return ""; } #>
```

在应用程序的代码中：

```
class FabrikamTemplate : MyStandardRunTimeTemplate
{
  protected override string CompanyName() { return "Fabrikam"; }
}
...
  string PageToDisplay = new FabrikamTemplate().TextTransform();
```

## <a name="guidelines-for-all-t4-templates"></a>所有 T4 模板准则

将数据收集与文本生成分开。

尝试避免混合计算和文本块。 在每个文本模板中，使用第一个 \<# code block #> 来设置变量并执行复杂的计算。 从第一个文本块直到模板的末尾或第一个 \<#+ class feature block #>，避免使用长表达式，并避免循环和条件，除非它们包含文本块。 这种做法使模板更易于读取和维护。

请勿将 `.tt` 用于包含文件。

对包含文件使用不同的文件扩展名，例如 `.ttinclude`。 `.tt` 仅用于要作为运行时或设计时文本模板处理的文件。 在某些情况下，Visual Studio 会识别 `.tt` 文件并自动设置其属性以进行处理。

将每个模板作为固定原型启动。

编写要生成的代码或文本的示例，并确保正确。 然后将其扩展名更改为 .tt，并增量插入通过读取模型修改内容的代码。

请考虑使用类型化模型。

尽管你可以为模型创建 XML 或数据库架构，但创建域特定语言 (DSL) 可能很有用。 DSL 的优点是，它生成一个类来表示架构中的每个节点，并生成属性来表示特性。 这意味着你可以根据业务模型进行编程。 例如：

```
Team Members:
<# foreach (Person p in team.Members)
 { #>
    <#= p.Name #>
<# } #>
```

请考虑对模型使用关系图。

许多模型只作为文本表进行最有效地表示和管理，尤其是在它们非常大时。

但是，对于某些类型的业务要求，必须阐明复杂的关系和数据流集，而关系图是最适合的介质。 关系图的一个优点是，可以轻松与用户和其他利益干系人进行讨论。 通过从业务要求级别的模型生成代码，使代码在需求发生变化时更加灵活。

还可以将自己的关系图类型设计为域特定语言 (DSL)。 可以从 UML 和 DSL 生成代码。 有关详细信息，请参阅[体系结构分析和建模](../modeling/analyze-and-model-your-architecture.md)。

## <a name="see-also"></a>另请参阅

- [使用 T4 文本模板生成设计时代码](../modeling/design-time-code-generation-by-using-t4-text-templates.md)
- [使用 T4 文本模板的运行时文本生成](../modeling/run-time-text-generation-with-t4-text-templates.md)

---
title: 创建自定义 T4 文本模板指令处理器
description: 了解文本模板转换过程以及如何创建自定义 T4 文本模板指令处理器。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, custom directive processors
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 9441a0525a4e01b99f6b43ef696b97f7d1a9b6d3
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665029"
---
# <a name="create-custom-t4-text-template-directive-processors"></a>创建自定义 T4 文本模板指令处理器

文本模板转换过程将文本模板文件作为输入，并生成一个文本文件作为输出 。 文本模板转换引擎控制转换过程，该引擎与文本模板转换主机和一个或多个文本模板指令处理器交互以完成该过程 。 有关详细信息，请参阅[文本模板转换过程](../modeling/the-text-template-transformation-process.md)。

若要创建自定义指令处理器，需要创建一个从 <xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor> 或 <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> 继承的类。

这两者之间的区别在于，<xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor> 可实现从用户获取参数和生成用于生成模板输出文件的代码所需的最小接口。 <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> 可实现“需要/提供”设计模式。 <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> 处理两个特殊参数：`requires` 和 `provides`。  例如，自定义指令处理器可以接受用户的文件名，打开并读取文件，然后将文件的文本存储在名为 `fileText` 的变量中。 <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> 类的子类可以将用户的文件名作为 `requires` 参数的值，并将用于存储文本的变量的名称作为 `provides` 参数的值。 该处理器将打开并读取文件，然后将文件的文本存储在指定的变量中。

必须先注册自定义指令处理器，然后才能在 Visual Studio 中从文本模板调用它。

有关如何添加注册表项的详细信息，请参阅[部署自定义指令处理器](../modeling/deploying-a-custom-directive-processor.md)。

## <a name="custom-directives"></a>自定义指令

自定义指令如下所示：

`<#@ MyDirective Processor="MyDirectiveProcessor" parameter1="value1" ... #>`

当你想要从文本模板访问外部数据或资源时，可以使用自定义指令处理器。

不同的文本模板可以共享单个指令处理器提供的功能，因此指令处理器提供了一种考虑重用代码的方法。 内置的 `include` 指令提供的功能类似，因为你可以使用该指令来分解代码，并在不同的文本模板之间共享。 不同之处在于，`include` 指令提供的任何功能都是固定的，不接受参数。 如果要为文本模板提供通用功能并允许模板传递参数，则必须创建自定义指令处理器。

自定义指令处理器的一些示例可以是：

- 一个指令处理器，用于从接受用户名和密码作为参数的数据库返回数据。

- 一个指令处理器，用于打开和读取接受文件名称作为参数的文件。

### <a name="principal-parts-of-a-custom-directive-processor"></a>自定义指令处理器的主体部分

若要开发指令处理器，必须创建一个从 <xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor> 或 <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> 继承的类。

必须实现的最重要的 `DirectiveProcessor` 方法如下所示。

- `bool IsDirectiveSupported(string directiveName)` - 如果指令处理器可以处理指定的指令，则返回 `true`。

- `void ProcessDirective (string directiveName, IDictionary<string, string> arguments)` - 模板引擎将在模板中每次出现指令时调用此方法。 处理器应保存结果。

在对 ProcessDirective() 的所有调用之后，模板引擎将调用这些方法：

- `string[] GetReferencesForProcessingRun()` - 返回模板代码所需的程序集名称。

- `string[] GetImportsForProcessingRun()` - 返回可在模板代码中使用的命名空间。

- `string GetClassCodeForProcessingRun()` - 返回模板代码可使用的方法、属性和其他声明的代码。 最简单的方法是生成一个包含 C# 或 Visual Basic 代码的字符串。 若要让指令处理器可以从使用任何 CLR 语言的模板进行调用，可以将语句构造为 CodeDom 树，然后以模板所使用的语言返回序列化树的结果。

- 有关详细信息，请参阅[演练：创建自定义指令处理器](../modeling/walkthrough-creating-a-custom-directive-processor.md)。

## <a name="see-also"></a>另请参阅

- [部署自定义指令处理器](../modeling/deploying-a-custom-directive-processor.md)介绍如何注册自定义指令处理器。
- [演练：创建自定义指令处理器](../modeling/walkthrough-creating-a-custom-directive-processor.md)介绍如何创建自定义指令处理器、如何注册和测试指令处理器以及如何将输出文件格式化为 HTML。

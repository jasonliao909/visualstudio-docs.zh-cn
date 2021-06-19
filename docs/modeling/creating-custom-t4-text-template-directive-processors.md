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
ms.workload:
- multiple
ms.openlocfilehash: 59644275f17eac197074351a777959bb1826a5de
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2021
ms.locfileid: "112389496"
---
# <a name="create-custom-t4-text-template-directive-processors"></a>创建自定义 T4 文本模板指令处理器

*文本模板转换过程* 采用 *文本模板* 文件作为输入，并生成文本文件作为输出。 文本 *模板转换引擎* 控制进程，引擎与文本模板转换主机和一个或多个文本模板指令处理器交互以完成该过程。  有关详细信息，请参阅文本 [模板转换过程](../modeling/the-text-template-transformation-process.md)。

若要创建自定义指令处理器，需要创建一个从 <xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor> 或 <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> 继承的类。

这两者的区别是，实现从用户获取参数和生成生成模板输出文件的代码所需的 <xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor> 最小接口。 <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> 实现 requires/provides 设计模式。 <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> 处理两个特殊参数： `requires` 和 `provides` 。  例如，自定义指令处理器可以接受用户的文件名，打开并读取该文件，然后将文件的文本存储在名为 的变量中 `fileText` 。 类的子类可能使用用户的文件名作为 参数的值，以及将文本存储为参数值的变量 <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> `requires` `provides` 的名称。 此处理器将打开并读取文件，然后将文件的文本存储在指定的变量中。

必须先注册自定义指令处理器，然后才能从 Visual Studio模板调用自定义指令处理器。

若要详细了解如何添加注册表项，请参阅 [部署自定义指令处理器](../modeling/deploying-a-custom-directive-processor.md)。

## <a name="custom-directives"></a>自定义指令

自定义指令如下所示：

`<#@ MyDirective Processor="MyDirectiveProcessor" parameter1="value1" ... #>`

若要从文本模板访问外部数据或资源，可以使用自定义指令处理器。

不同的文本模板可以共享单个指令处理器提供的功能，因此指令处理器提供了一种对代码进行因素处理以便重复使用的方法。 内置指令类似，因为可以使用它来对代码进行条理，并在不同的 `include` 文本模板之间共享它。 不同之处在于，指令提供的任何功能都是 `include` 固定的，不接受参数。 如果要向文本模板提供常见功能并允许模板传递参数，则必须创建自定义指令处理器。

自定义指令处理器的一些示例可能是：

- 一个指令处理器，用于从接受用户名和密码作为参数的数据库返回数据。

- 一个指令处理器，用于打开和读取接受文件名称作为参数的文件。

### <a name="principal-parts-of-a-custom-directive-processor"></a>自定义指令处理器的主体部分

若要开发指令处理器，必须创建从 或 继承的 <xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor> 类 <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> 。

必须 `DirectiveProcessor` 实现最重要的方法如下所示。

- `bool IsDirectiveSupported(string directiveName)` - `true` 如果指令处理器可以处理命名指令，返回 。

- `void ProcessDirective (string directiveName, IDictionary<string, string> arguments)` - 模板引擎针对模板中出现的每个指令调用此方法。 处理器应保存结果。

对 ProcessDirective 的所有调用 () 模板化引擎将调用以下方法：

- `string[] GetReferencesForProcessingRun()` - 返回模板代码所需的程序集的名称。

- `string[] GetImportsForProcessingRun()` - 返回可在模板代码中使用的命名空间。

- `string GetClassCodeForProcessingRun()` - 返回模板代码可以使用的方法、属性和其他声明的代码。 执行此操作的最简单方法是生成包含 C# 或代码Visual Basic字符串。 若要使指令处理器能够从使用任何 CLR 语言的模板调用，可以将语句构造为 CodeDom 树，然后返回以模板使用的语言序列化树的结果。

- 有关详细信息，请参阅 [演练：创建自定义指令处理器](../modeling/walkthrough-creating-a-custom-directive-processor.md)。

## <a name="see-also"></a>另请参阅

- [部署自定义指令处理器](../modeling/deploying-a-custom-directive-processor.md) 介绍了如何注册自定义指令处理器。
- [演练：创建自定义指令](../modeling/walkthrough-creating-a-custom-directive-processor.md) 处理器介绍了如何创建自定义指令处理器、如何注册和测试指令处理器，以及如何将输出文件格式化为 HTML。

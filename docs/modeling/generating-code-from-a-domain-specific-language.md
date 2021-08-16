---
title: 从域特定语言生成代码
description: 了解Domain-Specific工具如何提供一种强大的方法，用于从模型中表示的数据生成代码、文档和其他项目。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 57dc7ca55bcc0508cd3b78f5ea334b848322d17dd8e666ff051c25f6a7695ae3
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121288706"
---
# <a name="generating-code-from-a-domain-specific-language"></a>从域特定语言生成代码

Microsoft 提供了一种功能强大的方法，用于从模型中表示的数据生成代码、文档、配置文件 [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] 和其他项目。 使用 可以创建一组表示数据的类，还可以在名称和属性反映该数据的类中 [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] 编写文本模板。

例如，Fabrikam 有一个包含客户名称和电子邮件地址的 XML 文件。 他们的开发人员创建一个模型，其中 Customer 是一个类，具有属性名称和电子邮件。 他们编写多个文本模板处理数据，包括此片段，该片段生成一个包含所有客户的表作为 HTML 页面的一部分：

```
<table>
<# foreach (Customer c in ContactList) {  #>
  <tr><td> <#= c.FullName #> </td>
      <td> <#= c.EmailAddress #> </td> </tr>
<# } #>  </table>
```

处理客户数据库时，XML 文件将读入模型存储。 通过使用 *创建的* 指令处理器 [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] 使 Customer 类可用于文本模板中的代码。 许多文本模板可以针对同一存储运行。

文本模板对于 至关重要 [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] 。 它们用于为域模型的元素以及 VSPackage 和控件生成源代码，这些控件用于将工具与 Visual Studio。

本部分讨论创建、修改和调试 中使用的文本模板的一些方法 [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] 。

## <a name="in-this-section"></a>本节内容

[从文本模板访问模型](../modeling/accessing-models-from-text-templates.md)\
提供有关在文本模板中引用特定于域的语言的基本信息。

[演练：调试访问模型的文本模板](../modeling/walkthrough-debugging-a-text-template-that-accesses-a-model.md)\
介绍如何对引用域特定语言的文本模板执行故障排除和调试。

[演练：将主机连接到生成的指令处理器](../modeling/walkthrough-connecting-a-host-to-a-generated-directive-processor.md)\
介绍如何将自定义主机连接到生成的指令处理器。

[DslTextTransform 命令](../modeling/the-dsltexttransform-command.md)\
描述在命令行上为引用域特定语言的文本模板执行 TextTransform 可执行文件的命令文件。

## <a name="reference"></a>参考

[编写 T4 文本模板](../modeling/writing-a-t4-text-template.md)\
提供文本模板指令和控制块的语法。

## <a name="related-sections"></a>相关章节

[使用 T4 文本模板设计时代码生成](../modeling/design-time-code-generation-by-using-t4-text-templates.md)\
说明文本模板转换过程。

[生成过程中的代码生成](../modeling/code-generation-in-a-build-process.md)\
如果要从生成服务器上 DSL 生成文件，请阅读本主题。

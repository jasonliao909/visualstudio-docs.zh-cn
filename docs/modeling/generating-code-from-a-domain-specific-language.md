---
title: 从域特定语言生成代码
description: 了解特定于域的语言工具如何提供一种强大的方法来根据模型中表示的数据生成代码、文档和其他项目。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: b86507ac3e5aaadc0fc5f5c1b2bb9c1f380d9e5b
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126671852"
---
# <a name="generating-code-from-a-domain-specific-language"></a>从域特定语言生成代码

Microsoft [!INCLUDE[dsl](../modeling/includes/dsl_md.md)]提供了一种强大的方法，可根据模型中表示的数据生成代码、文档、配置文件和其他项目。 借助[!INCLUDE[dsl](../modeling/includes/dsl_md.md)]，可创建一组表示数据的类，并可在名称和属性反映该数据的类中编写文本模板。

例如，Fabrikam 有一个 XML 文件，其中包含客户名称和电子邮件地址。 他们的开发人员创建了一个模型，其中 Customer 为类，具有属性名称和电子邮件。 他们编写了多个文本模板来处理数据，包括此片段，它生成一个包含所有客户的表作为 HTML 页面的一部分：

```
<table>
<# foreach (Customer c in ContactList) {  #>
  <tr><td> <#= c.FullName #> </td>
      <td> <#= c.EmailAddress #> </td> </tr>
<# } #>  </table>
```

处理客户数据库时，会将 XML 文件读入模型存储区。 使用[!INCLUDE[dsl](../modeling/includes/dsl_md.md)]创建的指令处理器使 Customer 类可用于文本模板中的代码。 许多文本模板可针对同一个存储区运行。

文本模板对于[!INCLUDE[dsl](../modeling/includes/dsl_md.md)]来说是必需的。 它们用于生成域模型元素的源代码，以及用于将工具与 Visual Studio 集成的 VSPackage 和控件的源代码。

本部分介绍创建、修改和调试在[!INCLUDE[dsl](../modeling/includes/dsl_md.md)]中使用的文本模板的一些方式。

## <a name="in-this-section"></a>本节内容

[从文本模板访问模型](../modeling/accessing-models-from-text-templates.md)\
提供有关在文本模板中引用域特定语言的基本信息。

[演练：调试访问模型的文本模板](../modeling/walkthrough-debugging-a-text-template-that-accesses-a-model.md)\
介绍如何对引用域特定语言的文本模板进行故障排除和调试。

[演练：将主机连接至生成的指令处理器](../modeling/walkthrough-connecting-a-host-to-a-generated-directive-processor.md)\
介绍如何将自定义主机连接到生成的指令处理器。

[DslTextTransform 命令](../modeling/the-dsltexttransform-command.md)\
介绍在命令行上为引用域特定语言的文本模板执行 TextTransform 可执行文件的命令文件。

## <a name="reference"></a>参考

[编写 T4 文本模板](../modeling/writing-a-t4-text-template.md)\
提供文本模板指令和控制块的语法。

## <a name="related-sections"></a>相关章节

[使用 T4 文本模板生成设计时代码](../modeling/design-time-code-generation-by-using-t4-text-templates.md)\
说明文本模板转换过程。

[生成过程中的代码生成](../modeling/code-generation-in-a-build-process.md)\
如果要在生成服务器上从 DSL 生成文件，请阅读本主题。

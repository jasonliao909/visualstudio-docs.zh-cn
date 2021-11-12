---
title: 自定义域特定语言
description: 了解如何使用自定义代码以域特定语言 (DSL) 访问、修改或创建模型。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, programming
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: bd80246dfa98c898bd46518ebfc55c49b92504aa
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665482"
---
# <a name="write-code-to-customize-a-domain-specific-language"></a>编写代码以自定义域特定语言

本部分介绍如何使用自定义代码以域特定的语言访问、修改或创建模型。

可以在多种上下文中编写使用 DSL 的代码：

- 自定义命令。 你可以创建一个可修改模型的命令，用户可通过右键单击图表来调用该命令。 有关详细信息，请参阅[如何：向快捷菜单添加命令](../modeling/how-to-add-a-command-to-the-shortcut-menu.md)。

- **验证。** 可以编写代码来验证模型是否处于正确状态。 有关详细信息，请参阅[域特定语言中的验证](../modeling/validation-in-a-domain-specific-language.md)。

- 重写默认行为。 可以对从 DslDefinition.dsl 生成的代码的许多部分进行修改。 有关详细信息，请参阅[重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。

- 文本转换。 可以编写文本模板，其中包含可访问模型且可生成文本文件的代码，用于生成程序代码等。 有关详细信息，请参阅[从域特定语言生成代码](../modeling/generating-code-from-a-domain-specific-language.md)。

- 其他 Visual Studio 扩展。 可以编写单独的 VSIX 扩展来读取和修改模型。 有关详细信息，请参阅[如何：从程序代码中的文件打开模型](../modeling/how-to-open-a-model-from-file-in-program-code.md)

DslDefinition.dsl 中定义的类的实例保存在称为 In-Memory Store (IMS) 或 Store 的数据结构中 。 DSL 中定义的类始终将 Store 作为构造函数的参数。 例如，如果 DSL 定义了一个名为 Example 的类：

`Example element = new Example (theStore);`

将对象保存在 Store 中（而不是像普通对象一样保存）具有多个好处。

- **Transactions**。 可以将一系列相关更改分组到一个事务：

     `using (Transaction t = store.TransactionManager.BeginTransaction("updates"))`

     `{`

     `// make several changes to Store elements here`

     `t.Commit();`

     `}`

     如果更改过程中发生异常，导致最终的 Commit() 没有执行，Store 将重置为先前的状态。 这有助于确保错误不会导致模型处于不一致状态。 有关详细信息，请参阅[在程序代码中导航和更新模型](../modeling/navigating-and-updating-a-model-in-program-code.md)。

- 二进制关系。 如果定义两个类之间的关系，则两端的实例都具有一个可导航到另一端的属性。 这两端始终同步。 例如，如果使用名为“Parents”和“Children”的角色定义父子级关系，可以编写以下内容：

     `John.Children.Add(Mary)`

     以下两个表达式现在都为 true：

     `John.Children.Contains(Mary)`

     `Mary.Parents.Contains(John)`

     也可以通过编写以下内容来达到同样的效果：

     `Mary.Parents.Add(John)`

     有关详细信息，请参阅[在程序代码中导航和更新模型](../modeling/navigating-and-updating-a-model-in-program-code.md)。

- 规则和事件。 可以定义在进行指定更改时触发的规则。 例如，指定规则使图表上的形状与其呈现的模型元素保持同步。 有关详细信息，请参阅[响应和传播更改](../modeling/responding-to-and-propagating-changes.md)。

- 序列化。 Store 提供了一种将其包含的对象序列化到文件中的标准方法。 可以自定义序列化和反序列化的规则。 有关详细信息，请参阅[自定义文件存储和 XML 序列化](../modeling/customizing-file-storage-and-xml-serialization.md)。

## <a name="see-also"></a>另请参阅

- [自定义和扩展域特定语言](../modeling/customizing-and-extending-a-domain-specific-language.md)
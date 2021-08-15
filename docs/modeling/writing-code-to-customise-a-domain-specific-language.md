---
title: 自定义域特定语言
description: 了解如何使用自定义代码通过 DSL 代码访问、修改或创建特定于域的语言 (模型) 。
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
ms.openlocfilehash: d2cf06916c4dd149aa948c71d5f72eff307fcd45ea45227e91f89528e00a3fd9
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121398016"
---
# <a name="write-code-to-customize-a-domain-specific-language"></a>编写代码以自定义域特定语言

本部分演示如何使用自定义代码以域特定语言访问、修改或创建模型。

可以在多个上下文中编写适用于 DSL 的代码：

- **自定义命令。** 可以创建一个命令，用户可以通过右键单击关系图来调用该命令，该命令可以修改模型。 有关详细信息，请参阅 [如何：将命令添加到快捷菜单](../modeling/how-to-add-a-command-to-the-shortcut-menu.md)。

- **验证。** 可以编写验证模型是否位于正确状态的代码。 有关详细信息，请参阅在语言 [中Domain-Specific验证](../modeling/validation-in-a-domain-specific-language.md)。

- **重写默认行为。** 可以修改从 DslDefinition.dsl 生成的代码的许多方面。 有关详细信息，请参阅 [重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。

- **文本转换。** 可以编写包含访问模型并生成文本文件的代码的文本模板，例如生成程序代码。 有关详细信息，请参阅从语言 [语言](../modeling/generating-code-from-a-domain-specific-language.md)Domain-Specific代码。

- **其他Visual Studio扩展。** 可以编写单独的 VSIX 扩展来读取和修改模型。 有关详细信息，请参阅 [如何：在程序代码中从文件打开模型](../modeling/how-to-open-a-model-from-file-in-program-code.md)

在 DslDefinition.dsl 中定义的类的实例保存在称为内存中存储的数据结构中 (IMS ) *存储。* 在 DSL 中定义的类始终将 Store 作为构造函数的参数。 例如，如果 DSL 定义名为 Example 的类：

`Example element = new Example (theStore);`

将对象保存在 Store (而不是像普通对象一样) 有几个好处。

- **Transactions**。 可以将一系列相关更改分组到事务中：

     `using (Transaction t = store.TransactionManager.BeginTransaction("updates"))`

     `{`

     `// make several changes to Store elements here`

     `t.Commit();`

     `}`

     如果在更改过程中发生异常，因此不会执行最终的提交 () ，则 Store 将重置为以前的状态。 这有助于确保错误不会使模型保持不一致状态。 有关详细信息，请参阅在程序 [代码中导航和更新模型](../modeling/navigating-and-updating-a-model-in-program-code.md)。

- **二进制关系**。 如果定义两个类之间的关系，则两端的实例都有一个属性，该属性导航到另一端。 两端始终同步。 例如，如果定义与名为 Parent 和 Children 的角色的父子关系，可以编写：

     `John.Children.Add(Mary)`

     以下两个表达式现在都为 true：

     `John.Children.Contains(Mary)`

     `Mary.Parents.Contains(John)`

     也可通过编写以下代码来实现相同的效果：

     `Mary.Parents.Add(John)`

     有关详细信息，请参阅在程序 [代码中导航和更新模型](../modeling/navigating-and-updating-a-model-in-program-code.md)。

- **规则和事件**。 可以定义每当进行指定更改时所执行的规则。 例如，规则用于使关系图上的形状与它们显示的模型元素保持最新。 有关详细信息，请参阅 [响应和传播更改](../modeling/responding-to-and-propagating-changes.md)。

- **序列化**。 Store 提供了一种标准方法，用于将包含的对象序列化到文件中。 可以自定义序列化规则和反序列化规则。 有关详细信息，请参阅[自定义文件存储和 XML 序列化](../modeling/customizing-file-storage-and-xml-serialization.md)。

## <a name="see-also"></a>另请参阅

- [自定义和扩展域特定语言](../modeling/customizing-and-extending-a-domain-specific-language.md)
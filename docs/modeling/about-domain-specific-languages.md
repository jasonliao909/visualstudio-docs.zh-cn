---
title: 关于域特定语言
description: 了解 DSL 中特定于域 (语言) 旨在表达特定问题空间或域中的语句。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: ab56292aafda25efc0b3dfeeb14e93d4502a5567
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2021
ms.locfileid: "112384975"
---
# <a name="about-domain-specific-languages"></a>关于域特定语言

与常规用途语言（如 C# 或 UML）不同，特定于域的语言 (DSL) 旨在表达特定问题空间或域中的语句。

已知 DSL 包括正则表达式和 SQL。 每个 DSL 比描述对文本字符串或数据库的操作的常规用途语言要更好，但对于描述超出自身范围的想法要差得多。 各个行业也有其自己的 DSL。 例如，在电信行业中，呼叫说明语言广泛用于指定电话呼叫中的州序列，在航空公司中，标准 DSL 用于描述航班预订。

你的业务和项目还处理一组特殊的概念，这些概念可以通过 DSL 进行描述。 例如，你可以为以下应用程序之一定义 DSL：

- 规划网站中的导航路径。

- 电子组件的布线图。

- 用于机场的传送带和飞机处理设备网络。

设计 DSL 时，需要为域中每个重要概念（例如网页、灯或机场登记台）定义域类。 定义 *域关系（* 如超链接、线路或传送带）以将概念链接在一起。

DSL 用户创建 *模型。* 模型 *是* DSL 的实例。 例如，它们描述特定网站、特定设备的连接，或特定机场中的飞机处理系统。

用户可以将模型作为关系图或 Windows 窗体进行查看。 也可以将模型视为 XML，这是存储模型的方式。 定义 DSL 时，可以定义每个域类和关系的实例在用户屏幕上的显示方式。 典型的 DSL 显示为由箭头连接的图标或矩形的集合。

下图显示了关系图 DSL 中的一个小模型：

![都铎王朝家谱模型](../modeling/media/tudor_familytreemodel.png)

## <a name="what-you-can-do-with-dsls"></a>可以使用 DSL 执行哪些工作

DSL 的典型应用程序是生成程序代码或其他项目。 定义 DSL 时，可以定义 *文本模板* ，用于读取 DSL 的模型并生成文本文件。

例如，可以编写模板，用于制定机场计划，并生成部分软件用于飞机处理，以及一些描述该计划的用户文档。

定义 DSL 后，可以将它分发给可以在其自己的计算机上安装它的其他用户。 DSL 用户可以在 Visual Studio 中创建和编辑模型。

还可以定义菜单命令和其他工具，帮助用户编辑 DSL、验证约束以帮助确保正确使用 DSL，以及帮助用户创建新实例的项模板。 可以将一个或多个 DSL 及其工具和其他 Visual Studio作为集成包包装。

通常，当开发团队必须为多个产品编写类似的代码时，会创建特定于域的语言。 例如，一家专门使用包处理系统的公司可能会定义一个可为每个安装生成一些代码的步道 DSL。 DSL 的好处是，客户可以理解它，从它生成的代码是可靠的，并且如果客户需求发生变化，系统可以快速更新。

[!INCLUDE[dsl](../modeling/includes/dsl_md.md)] 允许你创建一个域特定的语言，该语言具有你自己的图形设计器和你自己的关系图表示法，然后使用该语言为每个项目生成适当的源代码。

## <a name="domain-specific-development"></a>Domain-Specific开发

特定于域的开发是识别应用程序的各个部分的过程，这些部分可以使用特定于域的语言进行建模，然后构造语言并部署到应用程序开发人员。 开发人员使用特定于域的语言来构造特定于其应用程序的模型，使用这些模型生成源代码，然后使用源代码开发应用程序。

## <a name="aspects-of-graphical-domain-specific-development"></a>图形化Domain-Specific的各个方面

特定于图形域的语言必须包含以下功能：

- 表示法

- 域模型

- 项目生成

- 序列化

- 与 Visual Studio 的集成

### <a name="notation"></a>表示法

特定于域的语言必须具有一组相当小的元素，这些元素可以轻松定义和扩展，以表示特定于域的构造。 表示法由表示元素的形状和表示图形关系图图面上元素之间的关系的连接器组成。 在 [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] 中，可以扩展和优化形状以表示域特定语言的元素。

### <a name="domain-model"></a>域模型

特定于域的语言必须将元素集及其之间的关系合并到一个一致的语法中。 它还必须定义元素和关系的组合是否有效。 例如，编程语言通常阻止循环继承，其中一个类派生自第二个类，第二个类派生自第一个类。 约束还可用于表示业务逻辑，例如，一个人不能依赖于自己。 [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] 使用约束来表示大多数特定于域的语言需要的限制类型。

### <a name="artifact-generation"></a>项目生成

特定于域的语言的主要用途之一是生成项目，例如源代码、XML 文件或一些其他可用数据。 通常，模型中的更改意味着项目更改。 可以使用 生成 [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] 项目，在更改模型时重新生成它们。

### <a name="serialization"></a>序列化

域特定语言必须以可编辑、保存、关闭和重新加载的某种形式持久保存。 [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] 使用 XML 格式，该格式可用于定义和自定义序列化或持久化域特定语言的方式。

### <a name="integration-with-visual-studio"></a>与 Visual Studio 的集成

由于 [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] 托管在 Visual Studio 中，因此它扩展了许多Visual Studio窗口和控件。 它还允许你自定义菜单命令、工具箱项和用户界面的其他元素的行为。

还可以为特定于域的语言创建模型总线适配器。 此适配器允许你引用模型中的模型和元素，并让你编写可以访问和更新 DSL 实例的代码。 通过使用功能强大的模型总线机制，可以编写Visual Studio模型扩展。 还可以编写使用模型独立应用程序。 有关详细信息，请参阅使用 [Modelbus 集成Visual Studio模型](../modeling/integrating-models-by-using-visual-studio-modelbus.md)。

## <a name="benefits-of-domain-specific-development"></a>开发Domain-Specific优势

特定于域的语言可提供以下优势：

- 包含完全适合问题空间的构造。

     与常规用途语言不同，特定于域的语言由直接表示问题空间逻辑的元素和关系组成。 例如，保险政策应用程序必须包含策略和索赔的元素。 域特定语言可以更轻松地设计应用程序，并查找和更正逻辑错误。

- 让非开发人员和不知道域的人了解整体设计。

     通过使用特定于域的图形语言，可以创建域的可视化表示形式，以便非开发人员可以轻松了解应用程序的设计。

- 可以更轻松地创建最终应用程序的原型。

     开发人员可以使用其模型生成的代码来创建可显示给客户端的原型应用程序。

## <a name="the-process-of-domain-specific-development"></a>开发Domain-Specific过程

大多数使用域特定语言的软件开发团队都遵循以下步骤来创建和使用其模型：

- 团队将域的可变部分与永不更改的部分进行区分。

- 开发人员为固定部件编写代码，并保留变量部分的扩展点。

- 首席软件开发人员或架构师创建一种特定于域的语言，该语言包含域的固定部分和变量部分的扩展点的设计模式。

- 首席软件开发人员或架构师将特定于域的语言部署到团队生成的各种应用程序的开发人员。

- 每个开发人员都会创建一个适用于特定应用程序的模型。

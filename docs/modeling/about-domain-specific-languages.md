---
title: 关于域特定语言
description: 了解域特定语言 (DSL) 如何被设计用来表达特定问题空间或域中的语句。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 54eeb75a623a7c20d0fad3f5f66e30c0b4617558
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664794"
---
# <a name="about-domain-specific-languages"></a>关于域特定语言

与通用语言（如 C# 或 UML）不同，域特定语言 (DSL) 旨在表达特定问题空间或域中的语句。

已知的 DSL 包括正则表达式和 SQL。 每个 DSL 在描述对文本字符串或数据库的操作时比通用语言好得多，但在描述其自身范围之外的想法时却差得多。 各个行业也都有其自己的 DSL。 例如，在电信行业，呼叫说明语言广泛用于指定电话呼叫中的状态序列，而在航空旅游行业，标准 DSL 被用于描述航班预订信息。

你的业务和项目也处理一组特殊的概念，这些概念可以用 DSL 来描述。 例如，你可以为以下应用之一定义 DSL：

- 规划网站中的导航路径。

- 电子元器件的接线图。

- 用于机场的传送带和行李处理设备的网络。

当你设计 DSL 时，需要为域中的每个重要概念（如网页、灯或机场登记台）定义一个域类。 需要定义域关系（如超链接、导线或传送带），将概念链接在一起。

你的 DSL 用户创建模型。 模型是 DSL 的实例。 例如，它们描述了一个特定的网站，或一个特定设备的布线，或一个特定机场的行李处理系统。

你的用户可以将模型作为关系图或 Windows 窗体。 也可以将模型视为 XML，这是存储模型的方式。 当你定义 DSL 时，可以定义每个域类和关系的实例在用户屏幕上的显示方式。 典型的 DSL 显示为由箭头连接的图标或矩形的集合。

下图显示了一个图解式 DSL 的小模型：

![都铎王朝家谱模型](../modeling/media/tudor_familytreemodel.png)

## <a name="what-you-can-do-with-dsls"></a>可以使用 DSL 执行哪些工作

DSL 的一个典型应用是生成程序代码或其他项目。 当你定义 DSL 时，可以定义文本模板，用于读取 DSL 的模型并生成文本文件。

例如，可以编写模板，用于制定机场计划，并生成部分软件用于行李处理，以及一些描述该计划的用户文档。

定义 DSL 后，可以将它分发给可以在其自己的计算机上安装它的其他用户。 DSL 用户可以在 Visual Studio 中创建和编辑模型。

你还可以定义菜单命令和其他工具以帮助用户编辑 DSL，定义验证约束以帮助确保正确使用 DSL，以及定义项目模板来帮助用户创建新的实例。 可以将一个或多个 DSL 及其工具和其他 Visual Studio 扩展打包成一个集成包。

通常，当开发团队必须为多个产品编写类似的代码时，会创建域特定语言。 例如，一家专门从事行李处理系统的公司可能会定义一个行李轨道 DSL，他们可以从这个 DSL 中生成每个安装的一些代码。 DSL 的好处是，客户可以理解它，通过它生成的代码是可靠的，并且如果客户需求发生变化，系统可以快速更新。

使用[!INCLUDE[dsl](../modeling/includes/dsl_md.md)]，可以创建一个域特定语言，使它具有你自己的图形设计器和你自己的关系图表示法，然后使用该语言为每个项目生成适当的源代码。

## <a name="domain-specific-development"></a>域特定开发

域特定开发是确定你的应用程序中可以通过使用域特定语言进行建模的部分，然后构造语言并部署给应用程序开发人员的过程。 开发人员使用域特定语言来构造特定于其应用程序的模型，使用这些模型生成源代码，然后使用源代码开发应用程序。

## <a name="aspects-of-graphical-domain-specific-development"></a>图形化域特定开发的各个方面

图形化域特定语言必须包含以下功能：

- 表示法

- 域模型

- 项目生成

- 序列化

- 与 Visual Studio 的集成

### <a name="notation"></a>表示法

域特定语言必须有一个合理的小的元素集，这些元素可以轻松地进行定义和扩展，以表示特定于域的构造。 表示法由表示元素的形状和表示图形关系图图面上元素之间的关系的连接符组成。 在[!INCLUDE[dsl](../modeling/includes/dsl_md.md)]中，可以对形状进行扩展和优化，以表示域特定语言的元素。

### <a name="domain-model"></a>域模型

域特定语言必须将元素集及元素之间的关系合并到一个一致的语法中。 它还必须定义元素和关系的组合是否有效。 例如，编程语言通常阻止循环继承，其中一个类派生自第二个类，第二个类派生自第一个类。 约束还可用于表示业务逻辑，例如，一个人不能依赖于自己。 [!INCLUDE[dsl](../modeling/includes/dsl_md.md)]使用约束来表示大多数域特定语言需要的限制类型。

### <a name="artifact-generation"></a>项目生成

域特定语言的主要用途之一是生成项目，例如源代码、XML 文件或一些其他可用数据。 通常，模型中的更改意味着项目更改。 你可以使用[!INCLUDE[dsl](../modeling/includes/dsl_md.md)]生成项目，并在更改模型时重新生成项目。

### <a name="serialization"></a>序列化

域特定语言必须以某种形式持久存在，可以编辑、保存、关闭和重新加载。 [!INCLUDE[dsl](../modeling/includes/dsl_md.md)]使用 XML 格式，让你可以定义和自定义序列化或持久化域特定语言的方式。

### <a name="integration-with-visual-studio"></a>与 Visual Studio 的集成

由于[!INCLUDE[dsl](../modeling/includes/dsl_md.md)]托管在 Visual Studio 中，因此它扩展了许多 Visual Studio 窗口和控件。 使用它，还可以自定义菜单命令、工具箱项和用户界面的其他元素的行为。

此外，你还可以为域特定语言创建模型总线适配器。 这个适配器可以让你在模型中引用模型和元素，并让你编写可以访问和更新 DSL 实例的代码。 通过使用功能强大的模型总线机制，你可以编写 Visual Studio 扩展，与多个模型一起工作。 还可以编写与模型一起使用的独立应用程序。 有关详细信息，请参阅[使用 Visual Studio Modelbus 集成模型](../modeling/integrating-models-by-using-visual-studio-modelbus.md)。

## <a name="benefits-of-domain-specific-development"></a>域特定开发的优势

域特定语言可提供以下优势：

- 包含完全适合问题空间的构造。

     与常规用途语言不同，域特定语言由直接表示问题空间逻辑的元素和关系组成。 例如，一个保单应用程序必须包括保单和索赔的元素。 使用域特定语言可以更轻松地设计应用程序，并查找和更正逻辑错误。

- 让非开发人员和不知道该域的人了解整体设计。

     通过使用图形化域特定语言，可以创建域的可视化表示形式，让非开发人员可以轻松了解应用程序的设计。

- 可以更轻松地创建最终应用程序的原型。

     开发人员可以使用其模型生成的代码来创建一个可以向客户端展示的原型应用程序。

## <a name="the-process-of-domain-specific-development"></a>域特定开发的过程

大多数使用域特定语言的软件开发团队都遵循以下步骤来创建和使用其模型：

- 团队将域的可变部分与永不改变的部分区分开来。

- 开发人员为固定部分编写代码，并保留可变部分的扩展点。

- 首席软件开发人员或架构师创建一个域特定语言，其中包含了域的固定部分和可变部分的扩展点的设计模式。

- 首席软件开发人员或架构师将域特定语言部署给团队生成的各种应用程序的开发人员。

- 每个开发人员都会创建一个适用于特定应用程序的模型。

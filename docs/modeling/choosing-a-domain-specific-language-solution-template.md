---
title: 选择域特定语言解决方案模板
description: 了解如何通过选择特定于域的语言设计器向导中提供的一个解决方案模板来创建特定于域的语言解决方案。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language Tools, solution templates
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 1b3d680df7f04b91c7640d54d994f38b84e41e10
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600678"
---
# <a name="choosing-a-domain-specific-language-solution-template"></a>选择域特定语言解决方案模板
若要通过选择特定于域的语言设计器向导中提供的一个解决方案模板来创建特定于域的语言解决方案。 通过选择要创建的语言最相似的模板，可以最大程度地减少对启动解决方案进行的修改。

 以下解决方案模板可用于特定于域的语言设计器向导。

|模板|功能|说明|
|-|-|-|
|类图|-   隔离舱形状<br />-   类继承<br />-   关系继承<br />-   形状继承<br />-   关系属性|如果域特定语言包含具有属性的实体和关系，则使用该解决方案模板。 该模板创建类似于 URL 类关系图的域特定语言。 主要实体是类和接口，以及关联、泛化和实现关系。 类或接口显示为包含属性列表的框。|
|组件关系图|-   端口|如果域特定语言包含组件（即软件系统的一部分），则使用该解决方案模板。 该模板创建类似于 UML 组件关系图的域特定语言。 主要实体是组件和端口，它们显示为组件外的小形状。|
|任务流关系图|-   图像和几何形状<br />-   泳道|如果域特定语言包含工作流、状态或序列，则使用该解决方案模板。 该模板创建类似于 UML 活动关系图的域特定语言。 主要实体是活动，主要关系是活动之间的转换。 该模板包括多个其他元素，例如开始状态、最终状态和同步栏。|
|最小语言|-   一个类和形状<br />-   一个关系和连接器|如果域特定语言与其他模板不相同，则使用该解决方案模板。 该模板创建具有两个类和一个关系的域特定语言，它们在“工具箱”中以“框”和“行”表示。   每个类和关系都具有示例字符串属性。|
|最小的 WinForm 设计器|-   小型模型。<br />-   显示模型的 Windows 窗体。|如果要构建一个应用程序，在该应用程序中 DSL 要绑定到 Windows 窗体，则使用该模板，而不是图像设计器。<br /><br /> 用作语言的用户界面的窗体位于文件夹 Dsl\UI 中。<br /><br /> 应在打开窗体设计器之前生成项目。<br /><br /> 有关详细信息，请参阅[创建基于 Windows 窗体的域特定语言](../modeling/creating-a-windows-forms-based-domain-specific-language.md)。|
|最小的 WPF 设计器|-   小型模型<br />-   显示模型的 Windows Presentation Foundation 用户界面|如果要构建一个应用程序，在该应用程序中 DSL 要绑定到 WPF 用户界面，则使用该模板，而不是图像设计器。<br /><br /> 用户界面的设计器位于文件夹 Dsl\UI 中。<br /><br /> 应在打开 UI 设计器之前生成项目。<br /><br /> 有关详细信息，请参阅[创建基于 WPF 窗体的域特定语言](../modeling/creating-a-wpf-based-domain-specific-language.md)。|
|DSL 库|-   最小的库|如果要生成可以导入到其他 DSL 定义中的部分 DSL 定义，则使用该模板。|

## <a name="see-also"></a>另请参阅

- [域特定语言工具的概述](../modeling/overview-of-domain-specific-language-tools.md)

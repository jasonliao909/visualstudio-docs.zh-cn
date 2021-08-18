---
title: 选择域特定语言解决方案模板
description: 了解如何通过选择语言设计器向导中可用的解决方案模板之一来创建Domain-Specific语言解决方案。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122085671"
---
# <a name="choosing-a-domain-specific-language-solution-template"></a>选择域特定语言解决方案模板
若要创建特定于域的语言解决方案，请选择"语言设计器向导"中提供的Domain-Specific模板之一。 通过选择与要创建的语言最相似的模板，可以最大程度地减少对启动解决方案所做的修改。

 以下解决方案模板在 Domain-Specific 设计器向导中提供。

|模板|功能|说明|
|-|-|-|
|类图|- 隔离舱形状<br />- 类继承<br />- 关系继承<br />- 形状继承<br />- 关系属性|如果特定于域的语言包含具有属性的实体和关系，请使用此解决方案模板。 此模板创建类似于 UML 类图的特定于域的语言。 主要实体是类和接口，以及关联、通用化和实现关系。 类或接口显示为包含属性列表的框。|
|组件关系图|- 端口|如果特定于域的语言包括组件（即软件系统的部件），请使用此解决方案模板。 此模板创建类似于 UML 组件关系图的特定于域的语言。 主要实体是组件和端口，这些组件和端口在组件外部显示为小形状。|
|任务Flow关系图|- 图像和几何形状<br />-   *泳道*|如果特定于域的语言包括工作流、状态或序列，请使用此解决方案模板。 此模板创建类似于 UML 活动关系图的特定于域的语言。 主实体是活动，主要关系是活动之间的转换。 该模板包括其他几个元素，例如开始状态、最终状态和同步栏。|
|最小语言|- 一个类和形状<br />- 一种关系和连接器|如果特定于域的语言与其他模板不一样，请使用此解决方案模板。 此模板创建域特定语言，该语言具有两个类和一个关系，在工具箱中以 **Box** 和 **Line 表示**。 类和关系各有一个示例字符串属性。|
|最小 WinForm 设计器|- 小型模型。<br />- Windows模型的窗体。|如果要生成将 DSL 绑定到窗体而不是图形设计器Windows模板，请使用此模板。<br /><br /> 充当语言用户界面的窗体位于 Dsl\UI 文件夹中。<br /><br /> 应在打开窗体设计器之前生成项目。<br /><br /> 有关详细信息，请参阅[创建语言Windows Forms-Based Domain-Specific语言](../modeling/creating-a-windows-forms-based-domain-specific-language.md)。|
|最小 WPF 设计器|- 小型模型<br />- Windows Presentation Foundation模型的用户界面|如果要生成一个应用程序，其中 DSL 绑定到 WPF 用户界面，而不是图形设计器，请使用此模板。<br /><br /> 用户界面的设计器位于 Dsl\UI 文件夹中。<br /><br /> 在打开 UI 设计器之前，应生成项目。<br /><br /> 有关详细信息，请参阅 [Creating a WPF-Based Domain-Specific Language](../modeling/creating-a-wpf-based-domain-specific-language.md)。|
|DSL 库|- 最小库|如果要生成可导入到其他 DSL 定义的部分 DSL 定义，请使用此模板。|

## <a name="see-also"></a>另请参阅

- [域特定语言工具的概述](../modeling/overview-of-domain-specific-language-tools.md)

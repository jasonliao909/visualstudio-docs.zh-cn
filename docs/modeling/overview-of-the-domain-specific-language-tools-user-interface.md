---
title: 域特定语言工具用户界面的概述
description: 概述 Visual Studio 中特定于域的语言工具解决方案的用户界面。
ms.date: 11/04/2016
ms.topic: overview
f1_keywords:
- vs.dsltools.dsldesigner.editor
helpviewer_keywords:
- Domain-Specific Language Tools, user interface
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.custom: SEO-VS-2020
ms.workload:
- multiple
ms.openlocfilehash: 7e5eadf964f8809c10a4a7b6654397b7ebb9b4f1
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122047733"
---
# <a name="overview-of-the-domain-specific-language-tools-user-interface"></a>域特定语言工具用户界面的概述
首次在 Visual Studio 中打开特定于域的语言工具（DSL 工具）解决方案时，用户界面如下图所示。

 ![dsl 设计器](../modeling/media/dsl_designer.png)

 下表说明了如何使用 UI 的部件。

|**元素**|**定义**|
|-|-|
|关系图|关系图显示域模型。<br /><br /> 关系图分为两侧。 一侧定义模型中的元素类型。 另一侧定义模型在屏幕上的显示方式。|
|工具箱|从工具箱拖动工具，将域类和形状类型添加到关系图。 若要添加关系、连接符和形状映射，请依次单击工具、关系图上的源节点以及目标节点。|
|DSL 资源管理器|**DSL 资源管理器** 在 DSL 定义是活动窗口时出现。 它以树形图的形式显示 DSL。 DSL 资源管理器允许编辑关系图上未显示的模型功能。 例如，可以使用 **DSL 资源管理器** 添加工具箱项和启动验证过程。|
|“DSL 详细信息”窗口|“DSL 详细信息”窗口显示域模型元素的属性，使你可以控制元素的显示方式，以及元素的复制和删除方式  。<br /><br /> - 默认情况下，“DSL 详细信息”窗口出现在“错误列表”窗口和“输出”窗口旁边    。|

## <a name="the-domain-model-diagram"></a>域模型关系图
 域模型关系图分为两个部分。 关系图的一侧显示模型中的元素和关系。 另一侧显示模型的显示方式，并包含用于显示模型关系图的元素和属性的形状。 下图显示了关系图中的元素。

 ![具有泳道的 dsl 设计器](../modeling/media/dsl_desinger.png)

 下表说明了域模型关系图中的部分元素。

|**条款**|**定义**|
|-|-|
|域类|域类是模型中的元素的类型。<br /><br /> 如果域类是多个关系的目标，则可以在关系图多次出现。<br /><br /> 若要添加域类，请将域类工具从“工具箱”拖动到关系图的“类和关系”侧   。|
|域关系|域关系是模型中的元素之间的链接类型。<br /><br /> 嵌入关系表示目标元素为源元素所有并受其限制，显示为实线  。 模型中的每个元素都应是一个嵌入关系的目标，以确保该模型变为树形。 引用关系表示模型元素之间的常规链接，显示为虚线  。 任何元素都可以具有任意数量的引用链接。<br /><br /> 通过依次单击“工具箱”上的工具、源域类以及目标类，创建关系  。|
|形状和连接符|形状指定模型元素应在 DSL 关系图上的显示方式，连接符指定 DSL 关系图上用于显示关系的线。<br /><br /> 若要创建形状或连接符，请将工具拖至关系图的“关系图元素”侧  。|
|形状映射|形状映射以线的形式在域模型关系图中显示，用于将形状链接到它显示的域类，或者将连接符链接到它显示的域关系。|

## <a name="see-also"></a>另请参阅

- [域特定语言工具的概述](../modeling/overview-of-domain-specific-language-tools.md)
- [域特定语言工具术语表](/previous-versions/bb126564(v=vs.100))
- [自定义和扩展域特定语言](../modeling/customizing-and-extending-a-domain-specific-language.md)
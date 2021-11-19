---
title: 使用 DSL 定义图表
description: 了解 DSL 工具定义关系表是用于定义域特定语言的重要工具。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.dsltools.dsldesigner.diagram
- vs.dsltools.dsldesigner.dsldiagram
helpviewer_keywords:
- Domain-Specific Language Tools, diagram
- Domain-Specific Language Tools, Split Tree
- Domain-Specific Language Tools, Show Map Lines
- Domain-Specific Language Tools, Show As Class
- Domain-Specific Language Tools, Bring Tree Here
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 566af235ff0894c35abe7d28aa18a06a2828281a
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665485"
---
# <a name="working-with-the-dsl-definition-diagram"></a>使用 DSL 定义图表
[!INCLUDE[dsl](../modeling/includes/dsl_md.md)] 定义关系表是用于定义域特定语言的重要工具。 你可以将元素添加到域模型并定义关系图上的关系，也可以修改关系图的布局以使其更具可读性。

## <a name="the-layout-of-the-diagram"></a>关系图的布局
 [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] 定义关系图有两个分区：“类和关系”分区和“关系图元素”分区。 “类和关系”分区显示域类、域关系和继承。 “关系图元素”分区显示了形状类、连接器类、泳道类和生成的设计器关系图。

 域类可以显示在“类和关系”分区的多个位置中。 如果域类是其他域类的基类，则域类定义将显示继承树；如果域类是嵌入或引用关系的源，则其定义将显示关系树。 域类占位符将显示为嵌入或引用关系的目标。 默认情况下，占位符元素将与折叠的“域属性”隔离舱一起显示。 它们不显示继承，也不显示嵌入或引用关系。

 当添加一个域类时，它将显示在“类和关系”分区的下半部分。 当添加一个嵌入或引用关系时，它将绘制在源域类的下方和右侧。

 当添加域类和关系时，可能很难找到某个特定的域类。 通过在“DSL 资源管理器”中右键单击一个域类，然后单击“在关系图中查找”，可找到该域类。

 以下部分介绍了如何更改关系图的外观以使其更易于阅读。

## <a name="copying-elements"></a>复制元素
 可以对 DSL 定义关系图中的元素使用复制、剪切和粘贴。

## <a name="zooming-in-or-out-on-the-diagram"></a>在关系图上放大或缩小
 通过使用“DSL 设计器”工具栏来设置缩放级别，可在关系图上放大或缩小。

## <a name="hiding-map-lines"></a>隐藏地图线条
 地图线条是在域类或域关系与其映射到的形状或连接符之间绘制的线条。 通过单击“DSL 设计器”工具栏上的“显示地图线条”按钮，可隐藏地图线条。 若要显示这些线条，请再次单击该按钮。

## <a name="changing-the-diagram-layout"></a>更改关系图布局
 可按以下方式更改“类和关系”分区的布局。

### <a name="expandcollapse"></a>展开/折叠
 通过右键单击表示域类或形状的隔离舱形状元素，然后单击“折叠”，可减小该元素的大小。 这将隐藏该形状的“域属性”隔离舱。 若要再次显示“域属性”隔离舱，请右键单击该形状，然后单击“展开”。

### <a name="move-updown"></a>上移/下移
 通过右键单击该元素，然后单击“上移”或“下移”，可在分区中上移或下移域类或关系图元素。 如果你要移动显示为嵌入或引用关系的目标的占位符元素，则关系将随它一起移动。

### <a name="expandcollapse-relationships-tree"></a>展开/折叠关系树
 如果一个域类在与其他域类的嵌入或引用关系中扮演源角色，则通过右键单击该域类定义，然后单击“折叠关系树”，可隐藏关系。 若要显示关系，请右键单击定义元素，然后单击“展开关系树”。

### <a name="expandcollapse-inheritance-tree"></a>展开/折叠继承树
 如果一个域类是其他域类的基类，则通过右键单击该域类定义，然后单击“折叠继承树”，可隐藏继承树。 若要显示继承树，请右键单击定义元素，然后单击“展开继承树”。

### <a name="bring-tree-here"></a>将树放在此处
 通过右键单击占位符域类，然后单击“将树放在此处”，可合并关系图。 该占位符域类将成为定义元素并显示继承和关系树。 如果前一个定义元素是关系的目标元素或继承关系中的子元素，则它将成为占位符元素；否则，它将消失。

### <a name="split-tree"></a>Split Tree
 通过右键单击显示继承或关系树的域类定义，然后单击“拆分树”，可中断继承或关系树。 该定义元素将成为占位符元素，并且定义域类连同其继承和关系树现在都可显示在分区底部。

### <a name="show-as-class"></a>显示为类
 如果域关系有派生关系，或者它与其他域关系有嵌入或引用关系，则通过右键单击该关系，然后单击“显示为类”，可将该关系显示为类。 该关系将与“域属性”隔离舱一起显示，并将显示继承和关系树。

## <a name="see-also"></a>另请参阅

- [域特定语言工具术语表](/previous-versions/bb126564(v=vs.100))
---
title: 连接线的属性
description: 了解连接器在生成的设计器中表示域关系，并使用这些属性自定义和扩展域特定语言。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Domain-Specific Language, connectors
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: ada7d2c78b818c18c9fdf21618ce66595eb9acfd
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126663933"
---
# <a name="properties-of-connectors"></a>连接线的属性
连接器表示生成的设计器中的域关系。

 有关详细信息，请参阅 [如何定义 Domain-Specific 语言](../modeling/how-to-define-a-domain-specific-language.md)。 有关如何使用这些属性的详细信息，请参阅 [自定义和扩展 Domain-Specific 语言](../modeling/customizing-and-extending-a-domain-specific-language.md)。

 连接器具有下表中列出的属性。

|Property|说明|默认|
|-|-|-|
|颜色|此连接符的颜色。|黑色|
|虚线样式|此连接符线的虚线线型 (纯色、短线、点、DashDot、DashDotDot 或自定义) 。|单色|
|源结束样式|此连接器 (Microsoft.visualstudio.modeling.diagrams.connectorarrowstyle.hollowarrow、Microsoft.visualstudio.modeling.diagrams.connectorarrowstyle.emptyarrow、Microsoft.visualstudio.modeling.diagrams.connectorarrowstyle.filledarrow、Microsoft.visualstudio.modeling.diagrams.connectorarrowstyle.emptydiamond、Microsoft.visualstudio.modeling.diagrams.connectorarrowstyle.filleddiamond 或 None) 的源端样式。|无|
|目标结束样式|此连接器的目标端样式 (Microsoft.visualstudio.modeling.diagrams.connectorarrowstyle.hollowarrow、Microsoft.visualstudio.modeling.diagrams.connectorarrowstyle.emptyarrow、Microsoft.visualstudio.modeling.diagrams.connectorarrowstyle.filledarrow、Microsoft.visualstudio.modeling.diagrams.connectorarrowstyle.emptydiamond、Microsoft.visualstudio.modeling.diagrams.connectorarrowstyle.filleddiamond 或 None) 。|无|
|文本颜色|与此连接器关联的文本修饰器所使用的颜色。|黑色|
|Thickness|此连接符线的粗细（英寸）。|0.03125|
|访问修饰符|类的访问级别 (`public` 或 `internal`) 。|公开|
|自定义特性|用于向从此连接器生成的源代码类添加特性。|\<none>|
|生成双派生|如果为 `True` ，则将生成基类和分部类 (来支持通过重写进行自定义) 。 有关详细信息，请参阅 [重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。|错误|
|具有自定义构造函数|如果为 `True` ，则在源代码中提供自定义构造函数。 有关详细信息，请参阅 [重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。|错误|
|继承修饰符|描述从连接器 (或) 生成的源代码类的继承类型 `none` `abstract` `sealed` 。|无|
|基本连接器|此连接器的基类。|（无）|
|名称|此连接器的名称。|当前名称|
|命名空间|与此连接器关联的命名空间。|当前命名空间|
|Tooltip 类型|如何定义工具提示 (fixed、variable 或 none) 。 如果已修复，则属性的值 `Fixed Tooltip Text` 将用作工具提示; 如果变量为，则在自定义代码中定义工具提示。|\<none>|
|说明|与此连接器关联的非正式注释。|\<none>|
|路由样式|用于路由连接器的样式。 `Rectilinear`连接器会按需向右倾斜; `Straight` 连接器不会。|折线|
|作为属性公开的颜色<br /><br /> 已公开虚线样式为属性<br /><br /> 以属性形式显示粗细<br /><br /> 公开文本颜色|如果 `True` 为，则用户可以设置形状的指定属性。 若要设置此项，请右键单击形状定义，然后单击 "添加" " **公开**"。|错误|
|说明|用于记录生成的设计器。|\<none>|
|显示名称|将在生成的设计器中显示的此连接器的名称。|\<none>|
|固定工具提示文本|用于固定工具提示的文本。|\<none>|
|帮助关键字|用于索引此元素的 F1 帮助的关键字。|\<none>|

## <a name="see-also"></a>另请参阅

- [域特定语言工具术语表](/previous-versions/bb126564(v=vs.100))
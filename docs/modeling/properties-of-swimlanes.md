---
title: 泳道属性
description: 了解泳道如何将关系图划分为垂直或水平区域，以及你如何定义要显示在泳道内的其他形状。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.dsltools.dsldesigner.swimlane
helpviewer_keywords:
- Domain-Specific Language, swimlane
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 27df14cad337fcb1ce1dffaeab1d501a6ff549e3
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126663907"
---
# <a name="properties-of-swimlanes"></a>泳道属性
可以向关系图添加泳道。 泳道将关系图划分为若干垂直或水平区域。 你可以定义要显示在泳道内的其他形状。 有关详细信息，请参阅[如何定义域特定语言](../modeling/how-to-define-a-domain-specific-language.md)。 有关如何使用这些属性的详细信息，请参阅[自定义和扩展域特定语言](../modeling/customizing-and-extending-a-domain-specific-language.md)。

 泳道具有下表中列出的属性。

|属性|说明|默认|
|-|-|-|
|主体填充颜色|泳道主体的填充颜色。|White|
|标头填充颜色|泳道标头的填充颜色。|深灰色|
|分隔符颜色|分隔线的颜色。|LightGray|
|分隔线样式|分隔线的样式（`Solid`、`Dash`、`Dot`、`DashDot`、`DashDotDot` 或 `Custom`）。|`Dash`|
|分隔符粗细|分隔线的粗细（英寸）。|0.03125|
|文本颜色|与此泳道相关联的文本修饰器所使用的颜色。|黑色|
|访问修饰符|类的访问级别（`public` 或 `internal`）。|公用|
|自定义特性|用于向从此泳道生成的代码类添加特性。|\<none>|
|生成双派生|如果为 `True`，将生成基类和分部类（用于支持通过重写进行自定义）。 有关详细信息，请参阅[重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。|错误|
|具有自定义构造函数|如果为 `True`，则在源代码中提供自定义构造函数。 有关详细信息，请参阅[重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。|错误|
|继承修饰符|描述从泳道生成的源代码类的继承类型（`none`、`abstract` 或 `sealed`）。|无|
|基本泳道|此泳道的基类。|（无）|
|名称|此泳道的名称。|当前名称|
|命名空间|与此泳道关联的命名空间。|当前命名空间|
|工具提示类型|工具提示是如何定义的（`fixed`、`variable` 或 `none`）。 如果为 `fixed`，将使用 `Fixed Tooltip Text` 属性的值，如果为 `variable`，则工具提示在自定义代码中进行定义。|\<none>|
|备注|与此泳道相关联的非正式说明。|\<none>|
|对齐方式|水平或垂直对齐。|垂直|
|初始高度|此泳道的初始高度（英寸）。 仅适用于水平泳道。|0|
|初始宽度|此泳道的初始宽度（英寸）。 仅适用于垂直泳道。|0|
|公开文本颜色|如果为 `True`，则用户可以在生成的设计器中设置泳道的颜色。 若要设置此项，请右键单击泳道形状，然后单击“添加已公开的项”。|错误|
|说明|用于记录生成的设计器。|\<none>|
|显示名称|将在生成的设计器中显示的名称，用来指代此泳道类。|\<none>|
|固定工具提示文本|用于固定工具提示的文本。|\<none>|
|帮助关键字|用于索引此泳道的 F1 帮助的关键字。|\<none>|

## <a name="see-also"></a>另请参阅

- [域特定语言工具术语表](/previous-versions/bb126564(v=vs.100))
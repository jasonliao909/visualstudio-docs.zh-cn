---
title: 几何形状的属性
description: 了解如何使用几何形状来指定如何以域特定语言显示域类的实例。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.dsltools.dsldesigner.geometryshape
helpviewer_keywords:
- Domain-Specific Language, geometry shape
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 62df0b182a0f160e3851ac5953bb7ca264f1b009
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126663909"
---
# <a name="properties-of-geometry-shapes"></a>几何形状的属性
您可以使用几何形状来指定如何以域特定语言显示域类的实例。 有关详细信息，请参阅 [如何定义 Domain-Specific 语言](../modeling/how-to-define-a-domain-specific-language.md)。 有关如何使用这些属性的详细信息，请参阅 [自定义和扩展 Domain-Specific 语言](../modeling/customizing-and-extending-a-domain-specific-language.md)。

 几何形状具有下表中列出的属性。

|属性|说明|默认|
|-|-|-|
|填充颜色|此形状的填充颜色。|White|
|填充渐变模式|此形状的填充渐变模式 (水平、垂直、正向对角线、向后对角或无) 。|横向|
|几何图形|此形状的几何图形 (矩形、圆角矩形、椭圆形或圆圈) 。|Rectangle|
|具有默认连接点|如果为 `True` ，则形状将使用生成的设计器中的顶部、底部、左侧和右侧连接点。|错误|
|轮廓颜色|此形状的边框颜色。|黑色|
|空心虚线样式|此形状的边框虚线样式 (纯色、破折号、点、DashDot、DashDotDot 或自定义) 。|单色|
|边框粗细|此形状的边框宽度。|0.03125|
|文本颜色|与此形状相关联的文本修饰器所使用的颜色。|黑色|
|访问修饰符|类的访问修饰符 (公共或内部) 。|公用|
|自定义特性|用于向为此形状生成的源代码类添加特性。|\<none>|
|生成双派生|如果为 `True` ，则将生成基类和分部类 (来支持通过重写进行自定义) 。 有关详细信息，请参阅 [重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。|错误|
|具有自定义构造函数|如果为 `True` ，则在源代码中提供自定义构造函数。 有关详细信息，请参阅 [重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。|错误|
|继承修饰符|描述从形状 (或) 生成的源代码类的继承类型 `none` `abstract` `sealed` 。|无|
|基本几何形状|此形状的基类。|（无）|
|名称|此形状的名称。|当前名称|
|命名空间|与此形状关联的命名空间。|当前命名空间|
|Tooltip 类型|如何定义工具提示 (fixed、variable 或 none) 。 如果已修复，则属性的值 `Fixed Tooltip Text` 将用作工具提示; 如果变量为，则在自定义代码中定义工具提示。|无|
|备注|与此元素相关联的非正式注释。|\<none>|
|初始高度|此形状的初始高度（英寸）。|1|
|初始宽度|此形状的初始宽度（英寸）。|1.5|
|作为属性公开的填充颜色<br /><br /> 公开的填充渐变模式<br /><br /> 作为属性公开的大纲颜色<br /><br /> 已公开大纲虚线样式为属性<br /><br /> 作为属性公开的大纲粗细<br /><br /> 公开文本颜色|如果 `True` 为，则用户可以设置形状的指定属性。 若要设置此项，请右键单击形状定义，然后单击 "添加" " **公开**"。|错误|
|说明|用于记录生成的设计器的说明。|\<none>|
|显示名称|将在生成的设计器中显示的此形状的名称。|\<none>|
|固定工具提示文本|用于固定工具提示的文本。|\<none>|
|帮助关键字|用于索引此形状的 F1 帮助的关键字。|\<none>|

## <a name="see-also"></a>另请参阅

- [域特定语言工具术语表](/previous-versions/bb126564(v=vs.100))
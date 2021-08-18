---
title: 端口形状的属性
description: 了解端口形状，以及如何使用端口形状在生成的设计器中表示域类。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.dsltools.dsldesigner.port
helpviewer_keywords:
- Domain-Specific Language, port shape
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 9b6b6cee3d0503116b149fe3da02fefc1429c603b79762aa2fb331b798cde166
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121428857"
---
# <a name="properties-of-port-shapes"></a>端口形状的属性
可以使用端口形状来表示生成的设计器中的域类。

 有关详细信息，请参阅 [How to Define a Domain-Specific Language](../modeling/how-to-define-a-domain-specific-language.md)。 若要详细了解如何使用这些属性，请参阅自定义和扩展Domain-Specific [语言](../modeling/customizing-and-extending-a-domain-specific-language.md)。

 端口形状具有下表中列出的属性。

|属性|说明|默认|
|-|-|-|
|填充颜色|此形状的填充颜色。|White|
|填充渐变模式|此形状的填充渐变模式。|横向|
|Geometry|此形状的几何图形 (矩形、圆角矩形、椭圆或圆形) 。|Rectangle|
|具有默认连接点|如果 `True` 为 ，则形状将使用生成的设计器中的上、下、左和右连接点。|错误|
|轮廓颜色|此形状的轮廓颜色。|黑色|
|大纲短划线样式|此形状的轮廓短划线样式 (Solid、Dash、Dot、DashDot、DashDotDot 或自定义) 。|单色|
|轮廓粗细|此形状的轮廓粗细。|0.03125|
|文本颜色|用于与此形状关联的文本修饰器的颜色。|黑色|
|访问修饰符|类的访问级别 (`public` 或 `internal`) 。|公共|
|自定义特性|用于向从此形状生成的源代码类添加属性。|\<none>|
|生成双派生|如果 `True` 为 ，则基类和分部 (都支持通过重写) 将生成自定义。 有关详细信息，请参阅 [重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)|错误|
|具有自定义构造函数|如果 `True` 为 ，将在源代码中提供自定义构造函数。 有关详细信息，请参阅 [重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。|错误|
|继承修饰符|描述从端口 或 (生成的源代码类的 `none` `abstract` `sealed` 继承) 。|无|
|基端口|此形状的基类。|（无）|
|名称|此形状的名称。|当前名称|
|命名空间|此形状所附属的命名空间。|当前命名空间|
|工具提示类型|如何定义工具提示 (固定、变量或无) 。 如果固定，则属性的值用作工具提示;如果为变量，则 `Fixed Tooltip Text` 工具提示在自定义代码中定义。|无|
|说明|与此形状关联的非正式说明。|\<none>|
|初始高度|此形状的初始高度（英寸）。|1|
|初始宽度|此形状的初始宽度（英寸）。|1.5|
|公开了填充颜色作为属性<br /><br /> 公开填充渐变模式<br /><br /> 将轮廓颜色公开为属性<br /><br /> 公开轮廓短划线样式作为属性<br /><br /> 公开轮廓粗细属性<br /><br /> 公开文本颜色|如果 `True` 为 ，则用户可以设置形状的已说明属性。 若要设置此选项，请右键单击形状定义，然后单击"**添加公开"。**|错误|
|说明|用于记录生成的设计器。|\<none>|
|显示名称|将在此形状的生成设计器中显示的名称。|\<none>|
|修复了工具提示文本|用于固定工具提示的文本。|\<none>|
|帮助关键字|用于为此形状索引 F1 帮助的 关键字。|\<none>|

## <a name="see-also"></a>请参阅

- [域特定语言工具术语表](/previous-versions/bb126564(v=vs.100))
---
title: 连接线的属性
description: 了解连接符在生成的设计器中表示域关系，并且使用这些属性自定义和扩展域特定语言。
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
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126663933"
---
# <a name="properties-of-connectors"></a>连接线的属性
连接符表示生成的设计器中的域关系。

 有关详细信息，请参阅[如何定义域特定语言](../modeling/how-to-define-a-domain-specific-language.md)。 有关如何使用这些属性的详细信息，请参阅[自定义和扩展域特定语言](../modeling/customizing-and-extending-a-domain-specific-language.md)。

 连接符具有下表中列出的属性。

|属性|说明|默认|
|-|-|-|
|颜色|此连接符的颜色。|黑色|
|Dash Style|此连接符线条的短划线样式（实线、短划线、点、短划线-点、短划线-点-点或自定义）。|单色|
|Source End Style|此连接符的源端样式（空心箭头、空箭头、实心箭头、空菱形、实心菱形或无）。|无|
|Target End Style|此连接符的目标端样式（空心箭头、空箭头、实心箭头、空菱形、实心菱形或无）。|无|
|Text Color|与此连接符相关联的文本修饰器所使用的颜色。|黑色|
|Thickness|此连接符线条的粗细（以英寸为单位）。|0.03125|
|访问修饰符|类的访问级别（`public` 或 `internal`）。|公用|
|自定义特性|用于向从此连接符生成的源代码类添加特性。|\<none>|
|Generates Double Derived|如果为 `True`，将生成基类和分部类（用于支持通过重写进行自定义）。 有关详细信息，请参阅[重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。|错误|
|Has Custom Constructor|如果为 `True`，则在源代码中提供自定义构造函数。 有关详细信息，请参阅[重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。|错误|
|Inheritance Modifier|描述从连接符生成的源代码类的继承类型（`none`、`abstract` 或 `sealed`）。|无|
|Base Connector|此连接符的基类。|（无）|
|名称|此连接符的名称。|当前名称|
|命名空间|与此连接符关联的命名空间。|当前命名空间|
|Tooltip Type|如何定义工具提示（固定、可变或无）。 如果为“固定”，`Fixed Tooltip Text` 属性值将用作工具提示，如果为“可变”，则工具提示在自定义代码中进行定义。|\<none>|
|备注|与此连接符相关联的非正式说明。|\<none>|
|Routing Style|用于排列连接符的样式。 `Rectilinear` 连接符会按要求进行直角旋转；`Straight` 连接符不会。|直线|
|Exposed Color As Property<br /><br /> Exposed Dash Style As Property<br /><br /> Exposed Thickness As Property<br /><br /> Exposes Text Color|如果为 `True`，则用户可以设置形状的指定属性。 若要设置此项，请右键单击形状定义，然后单击“添加已公开的项”。|错误|
|说明|用于记录生成的设计器。|\<none>|
|显示名称|将在生成的设计器中显示的此连接符的名称。|\<none>|
|Fixed Tooltip Text|用于固定工具提示的文本。|\<none>|
|帮助关键字|用于索引此元素的 F1 帮助的关键字。|\<none>|

## <a name="see-also"></a>另请参阅

- [域特定语言工具术语表](/previous-versions/bb126564(v=vs.100))
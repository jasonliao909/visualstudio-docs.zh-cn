---
title: 关系图属性
description: 了解关系图以及如何设置属性来指定关系图在生成的设计器中的显示方式。
ms.custom: SEO-VS-2020
ms.date: 10/31/2018
ms.topic: reference
f1_keywords:
- vs.dsltools.dsldesigner.dsldiagram
helpviewer_keywords:
- Domain-Specific Language, diagram
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 5128befb2460a364758a692cfe5cac0a30732f1e
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126663925"
---
# <a name="properties-of-diagrams"></a>关系图属性
你可以设置属性来指定关系图在生成的设计器中的显示方式。 例如，可以指定关系图中文本的默认颜色。

 有关详细信息，请参阅[如何定义域特定语言](../modeling/how-to-define-a-domain-specific-language.md)。 有关如何使用这些属性的详细信息，请参阅[自定义和扩展域特定语言](../modeling/customizing-and-extending-a-domain-specific-language.md)。

 下表列出了关系图的属性。

|属性|说明|默认|
|-|-|-|
|填充颜色|关系图的填充颜色。|White|
|文本颜色|关系图上显示的文本的颜色。|黑色|
|访问修饰符|类的访问修饰符（公用或内部）。|公用|
|自定义特性|用于将属性添加到已生成的代码类。|\<none>|
|生成双派生|如果为 `True`，将生成基类和分部类（用于支持通过重写进行自定义）。 有关详细信息，请参阅[重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。|错误|
|具有自定义构造函数|如果为 `True`，则在源代码中提供自定义构造函数。 有关详细信息，请参阅[重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。|错误|
|继承修饰符|描述从关系图生成的源代码类的继承类型（`none`、`abstract` 或 `sealed`）。|无|
|基本关系图|此关系图的基类。|（无）|
|名称|此关系图的名称。|当前名称|
|命名空间|与此关系图关联的命名空间。|当前命名空间|
|表示的类|此关系图表示的根域类。|当前根类（如果适用）|
|备注|与此元素相关联的非正式说明。|\<none>|
|作为属性公开填充颜色|如果为 `True`，则用户可以设置生成的设计器的关系图的填充颜色。 若要设置此属性，请右键单击关系图形状，然后单击“添加已公开的项”。|错误|
|作为属性公开文本颜色|如果为 `True`，则用户可以在生成的设计器中设置关系图的文本颜色。 若要设置此属性，请右键单击关系图形状，然后单击“添加已公开的项”。|错误|
|说明|用于记录生成的设计器的说明。|\<none>|
|显示名称|将在生成的设计器中显示的此关系图的名称。|\<none>|
|帮助关键字|用于索引此关系图的 F1 帮助的关键字。|\<none>|

## <a name="see-also"></a>另请参阅

[域特定语言工具术语表](/previous-versions/bb126564(v=vs.100))
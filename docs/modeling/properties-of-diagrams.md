---
title: 关系图的属性
description: 了解关系图以及如何设置指定关系图在生成的设计器中的显示方式的属性。
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
ms.workload:
- multiple
ms.openlocfilehash: 8a060c79866d1746135f8a29aef15ca96dd51f63
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2021
ms.locfileid: "112390667"
---
# <a name="properties-of-diagrams"></a>关系图的属性
可以设置指定关系图在生成的设计器中的显示方式的属性。 例如，可以指定关系图中文本的默认颜色。

 有关详细信息，请参阅 [如何定义特定于域的语言](../modeling/how-to-define-a-domain-specific-language.md)。 若要详细了解如何使用这些属性，请参阅自定义和扩展 [特定于域的语言](../modeling/customizing-and-extending-a-domain-specific-language.md)。

 下表列出了关系图的属性。

|属性|描述|默认|
|-|-|-|
|填充颜色|关系图的填充颜色。|White|
|文本颜色|关系图上显示的文本的颜色。|黑色|
|访问修饰符|类的访问修饰符 (公共或内部) 。|公用|
|自定义特性|用于将属性添加到生成的代码类。|\<none>|
|生成双派生|如果 `True` 为 ，则基类和分部 (类都支持通过重写) 将生成自定义。 有关详细信息，请参阅 [重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。|False|
|具有自定义构造函数|如果 `True` 为 ，将在源代码中提供自定义构造函数。 有关详细信息，请参阅 [重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。|False|
|继承修饰符|描述从关系图生成的源代码类的继承类型 (、 或 `none` `abstract` `sealed`) 。|无|
|基图|此关系图的基类。|（无）|
|名称|此关系图的名称。|当前名称|
|命名空间|此关系图所附属的命名空间。|当前命名空间|
|表示的类|此关系图表示的根域类。|当前根类（如果适用）|
|说明|与此元素关联的非正式说明。|\<none>|
|将填充颜色公开为 属性|如果 `True` 为 ，则用户可以设置生成的设计器的关系图的填充颜色。 若要设置此属性，请右键单击关系图形状，然后单击"**添加公开"。**|False|
|将文本颜色公开为 属性|如果 `True` 为 ，则用户可以在生成的设计器中设置关系图的文本颜色。 若要设置此属性，请右键单击关系图形状，然后单击"**添加公开"。**|False|
|描述|用于记录生成的设计器的说明。|\<none>|
|显示名称|将在此关系图的生成设计器中显示的名称。|\<none>|
|帮助关键字|用于索引此关系图的 F1 帮助的 关键字。|\<none>|

## <a name="see-also"></a>另请参阅

[特定于域的语言工具术语表](/previous-versions/bb126564(v=vs.100))
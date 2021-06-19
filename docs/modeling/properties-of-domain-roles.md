---
title: 域角色的属性
description: 了解与域角色关联的属性，如集合类型、自定义属性和 Is Property Browsable。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 670704a86f0c149d26c7c869259c0f2f6bb75881
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2021
ms.locfileid: "112385140"
---
# <a name="properties-of-domain-roles"></a>域角色的属性
下表中的属性与域角色相关联。 有关域角色的信息，请参阅 [了解模型、类和关系](../modeling/understanding-models-classes-and-relationships.md)。 有关如何使用这些属性的信息，请参阅自定义和扩展Domain-Specific [语言](../modeling/customizing-and-extending-a-domain-specific-language.md)。

|属性|描述|默认|
|-|-|-|
|集合类型|如果此角色的乘数为 0..*或 1..，则此属性将自定义用于存储链接集合 \* 的泛型类型。|`(none)` - <xref:Microsoft.VisualStudio.Modeling.LinkedElementCollection%601> 使用|
|自定义特性|此处指定的属性将添加为生成的代码类的属性。|<无\>|
|属性可浏览|如果为 ，并且关系的乘数为 `True` 0..1 或 1..1，则用户可以在"属性"窗口中浏览 **角色** 属性。 属性在关系链接的另一端显示元素的名称。|`True`|
|Is 属性生成器|如果为 ，则为此角色生成一个角色属性，可用于 `True` 遍历程序代码中的关系。 如果设置此 false，可以使用域关系的静态方法以效率较低的方式遍历关系。|`True`|
|属性 Getter Access 修饰符|生成的属性的 getter 的访问修饰符 (`public` 、 或 `internal` `private` `protected` `protected internal`) 。|`public`|
|属性 Setter Access 修饰符|生成的属性的 setter 的访问修饰符 (`public` `internal` `private` 、、、 或 `protected` `protected internal`) 。|`public`|
|多重性|在 、、 或 (可以起到相反作用的模型 `0..1` `1..1` `0..*` `1..*` 元素) 。 如果乘数为 或 `0..*` ，则生成的 `1..*` 属性表示集合;否则，生成的属性表示单个模型元素。|取决于关系类型以及这是关系中的源角色还是目标角色。|
|名称|域角色的名称。 此属性不能包含空格。|此角色的角色播放器的域类的名称。|
|传播复制|`DoNotPropagateCopy` - 复制的角色播放器将没有此链接的副本。<br /><br /> `PropagateCopyToLinkOnly` - 复制的链接指向现有的相反角色播放器。<br /><br /> `PropagateCopyToLinkAndOppositeRolePlayer` - 复制的链接指向相反的角色播放器的副本。|`PropagateCopyToLinkAndOppositeRolePlayer` 用于嵌入的源角色的 。<br /><br /> `DoNotPropagateCopy` 其他角色的 。<br /><br /> 有关详细信息，请参阅 [自定义复制行为](../modeling/customizing-copy-behavior.md)|
|传播删除|`True` 如果删除关联的链接，则删除扮演此角色的元素。|`True` 作为嵌入角色的目标。<br /><br /> `False` 其他角色的 。|
|属性名称|在角色播放器代码中生成的属性的名称。 此名称不能包含空格。|如果此角色具有零对一或一对一乘法，则相反角色的名称;否则为相反角色的复数形式名称。|
|角色播放器|可在关系中扮演此角色的元素的域类。 此属性为只读。|此角色的角色播放器的域类。|
|说明|与域角色关联的非正式说明。|<无\>|
|类别|生成的属性在生成的设计器的"属性 **"** 窗口中显示时所基于的类别。 如果此属性为空，则生成的属性将显示在 **Misc 类别** 下|<无\>|
|描述|用于记录代码的说明，在生成的设计器的 UI 中使用。<br /><br /> 说明显示在角色播放器类上生成的属性的 IntelliSense 工具提示中。|`Description for`*角色的全名*|
|显示名称|在生成的设计器中为域角色显示的名称。|Name 属性的调整后的值。|
|帮助关键字|用于为域角色的 F1 帮助编制索引的可选关键字。|\<none>|
|属性显示名称|在生成的设计器中为生成的角色属性显示的名称。|"属性名称"属性的调整后的值。|

> [!NOTE]
> 显示名称的默认值基于关联的属性值，在以小写字符为前且后跟另一个大写字符的每个大写字符之前插入空格。

## <a name="see-also"></a>另请参阅

- [域关系的属性](../modeling/properties-of-domain-relationships.md)
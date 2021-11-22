---
title: 域角色的属性
description: 了解与域角色关联的属性，例如“集合类型”、“自定义属性”和“属性是否可浏览”。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: f542faecf3ba1ac64076f145cc1e280cf255aad6
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126663916"
---
# <a name="properties-of-domain-roles"></a>域角色的属性
下表中的属性与域角色相关联。 有关域角色的信息，请参阅[了解模型、类和关系](../modeling/understanding-models-classes-and-relationships.md)。 有关如何使用这些属性的详细信息，请参阅[自定义和扩展域特定语言](../modeling/customizing-and-extending-a-domain-specific-language.md)。

|属性|说明|默认|
|-|-|-|
|集合类型|如果此角色的多重性为 0..* 或 1..\*，那么该属性会自定义用来存储链接集合的泛型类型。|`(none)` - <xref:Microsoft.VisualStudio.Modeling.LinkedElementCollection%601> 已使用|
|自定义特性|此处指定的属性将添加为已生成代码类的属性。|<none\>|
|Is Property Browsable|如果为 `True` 且关系的多重性为 0..1 或 1..1，那么用户可以在“属性”窗口中浏览角色属性。 属性会在关系链接的另一端显示元素的名称。|`True`|
|Is Property Generator|如果为 `True`，则可以为该角色生成角色属性，你可以使用它来在程序代码中遍历关系。 如果设置此 false，可以使用域关系的静态方法以效率较低的方式遍历关系。|`True`|
|属性 Getter 访问修饰符|已生成属性的 Getter 的访问修饰符（`public`、`internal`、`private`、`protected` 或 `protected internal`）。|`public`|
|属性资源库访问修饰符|已生成属性的资源库的访问修饰符（`public`、`internal`、`private`、`protected` 或 `protected internal`）。|`public`|
|多重性|可扮演相反角色的模块元素的数目（`0..1`、`1..1`、`0..*` 或 `1..*`）。 如果多重性为 `0..*` 或 `1..*`，则已生成属性表示集合，否则，已生成属性表示单个模型元素。|取决于关系类型，以及它是关系中的源角色还是目标角色。|
|名称|域角色的名称。 该属性不能包含空格。|适用于该角色的角色扮演者域类的名称。|
|Propagates Copy|`DoNotPropagateCopy` - 复制的角色扮演者将没有此链接的副本。<br /><br /> `PropagateCopyToLinkOnly` - 复制的链接指向现有的相反角色扮演者。<br /><br /> `PropagateCopyToLinkAndOppositeRolePlayer` - 复制的链接指向相反角色扮演者的副本。|`PropagateCopyToLinkAndOppositeRolePlayer` 用于嵌入的源角色。<br /><br /> `DoNotPropagateCopy` 用于其他角色。<br /><br /> 有关详细信息，请参阅[自定义复制行为](../modeling/customizing-copy-behavior.md)|
|Propagates Delete|如果为 `True`，则在删除关联链接时删除扮演该角色的元素。|如果为 `True`，则为嵌入角色的目标。<br /><br /> 如果为 `False`，则为其他角色。|
|属性名称|在角色扮演者代码中生成的属性的名称。 该名称不能包含空格。|如果该角色具有零对一或一对一多重性，则为相反角色的名称；否则，为相反角色的复数形式名称。|
|角色扮演者|可在关系中扮演此角色的元素的域类。 此属性为只读。|适用于该角色的角色扮演者的域类。|
|备注|与域角色关联的非正式说明。|<none\>|
|Category|一个类别，在其下的已生成属性显示在已生成设计器的“属性”窗口中。 如果该属性为空，则已生成属性显示在“杂项”类别下|<none\>|
|说明|用于记录代码并且用于生成的设计器的用户界面的说明。<br /><br /> 对于角色扮演者类上的已生成属性，该描述显示在 IntelliSense 工具提示中。|`Description for` 类型的全名|
|显示名称|针对域角色在生成的设计器中显示的名称。|“名称”属性的已调整值。|
|帮助关键字|用于针对域角色索引 F1 帮助的可选关键字。|\<none>|
|属性显示名称|在生成的设计器中显示的已生成角色属性的名称。|“属性名称”属性的已调整值。|

> [!NOTE]
> 通过在每个大写字符（以小写字符开头且后面没有其他大写字符）之前插入空格，显示名称的默认值基于已关联的属性值。

## <a name="see-also"></a>另请参阅

- [域关系的属性](../modeling/properties-of-domain-relationships.md)
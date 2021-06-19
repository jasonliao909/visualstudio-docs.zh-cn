---
title: 域关系的属性
description: 了解与域关系工厂关联的属性，如 Access 修饰符、自定义属性和生成双重派生。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Domain-Specific Language, domain relationships
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: fc92bbc32a454208f3d455734b7697a2e69037b4
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2021
ms.locfileid: "112390654"
---
# <a name="properties-of-domain-relationships"></a>域关系的属性
下表中的属性与域关系相关联。 有关域关系的信息，请参阅 [了解模型、类和关系](../modeling/understanding-models-classes-and-relationships.md)。 有关如何使用这些属性的信息，请参阅自定义和扩展Domain-Specific [语言](../modeling/customizing-and-extending-a-domain-specific-language.md)。

|属性|描述|默认|
|-|-|-|
|访问修饰符|域关系的访问级别 (`public` 或 `internal`) 。|`public`|
|自定义特性|用于将属性添加到从域关系生成的源代码类。|\<none>|
|生成双派生|如果 `True` 为 ，则基类和分部 (都支持通过重写) 自定义。 有关详细信息，请参阅 [重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。|`False`|
|具有自定义构造函数|如果 `True` 为 ，则指示源代码中提供了自定义构造函数。 有关详细信息，请参阅 [重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。|`False`|
|继承修饰符|描述从域关系生成的源代码类的继承类型 (`none` `abstract` 或 `sealed`) 。|\<none>|
|允许重复项|如果 `True` 为 ，则在同一两个元素之间可能会创建域关系的重复链接。|`False`|
|基关系|如果域关系派生为域关系的基关系。|\<none>|
|正在嵌入|如果 `True` 为 ，则域关系是嵌入关系。 如果 `False` 为 ，则关系是引用关系。|\<both>|
|名称|域关系的名称。|当前名称|
|命名空间|与域关系附属的命名空间。|当前命名空间|
|说明|与域关系关联的非正式说明。|\<none>|
|描述|用于记录代码的说明，在生成的设计器的 UI 中使用。|\<none>|
|显示名称|在生成的设计器中为域关系显示的名称。|\<none>|
|帮助关键字|用于为域关系的 F1 帮助编制索引的可选关键字。|\<none>|

## <a name="see-also"></a>另请参阅

- [域特定语言工具术语表](/previous-versions/bb126564(v=vs.100))
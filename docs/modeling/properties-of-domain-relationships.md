---
title: 域关系的属性
description: 了解与域关系关联的属性，如访问修饰符、自定义属性和生成双派生。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Domain-Specific Language, domain relationships
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 8972722c0f65f4d007db7173ef41b7a40dba1208
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126663921"
---
# <a name="properties-of-domain-relationships"></a>域关系的属性
下表中的属性与域关系相关联。 有关域关系的信息，请参阅[了解模型、类和关系](../modeling/understanding-models-classes-and-relationships.md)。 有关如何使用这些属性的详细信息，请参阅[自定义和扩展域特定语言](../modeling/customizing-and-extending-a-domain-specific-language.md)。

|属性|说明|默认|
|-|-|-|
|访问修饰符|域关系的访问级别（`public` 或 `internal`）。|`public`|
|自定义特性|用于向从域关系生成的源代码类添加特性。|\<none>|
|生成双派生|如果为 `True`，会生成基类和分部类（用于支持通过重写进行自定义）。 有关详细信息，请参阅[重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。|`False`|
|具有自定义构造函数|如果为 `True`，则指示在源代码中提供自定义构造函数。 有关详细信息，请参阅[重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。|`False`|
|继承修饰符|描述从域关系生成的源代码类的继承类型（`none`、`abstract` 或 `sealed`）。|\<none>|
|允许重复项|如果为 `True`，则允许在相同的两个元素之间创建域关系的重复链接。|`False`|
|基本关系|如果派生域关系，则为域关系的基本关系。|\<none>|
|嵌入|如果为 `True`，则域关系是嵌入关系。 如果为 `False`，则域关系是引用关系。|\<both>|
|名称|域关系的名称。|当前名称|
|命名空间|与域关系关联的命名空间。|当前命名空间|
|备注|与域关系相关联的非正式说明。|\<none>|
|说明|用于记录代码，并且用于生成的设计器的用户界面的说明。|\<none>|
|显示名称|针对域关系在生成的设计器中显示的名称。|\<none>|
|帮助关键字|用于针对域关系索引 F1 帮助的可选关键字。|\<none>|

## <a name="see-also"></a>另请参阅

- [域特定语言工具术语表](/previous-versions/bb126564(v=vs.100))
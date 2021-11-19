---
title: 域类的属性
description: 了解域类的各种属性，例如访问修饰符、自定义特性和生成双派生。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Domain-Specific Language, domain class
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 55a91ed135d2417ec12603942c00b47ca0a96952
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126663924"
---
# <a name="properties-of-domain-classes"></a>域类的属性
域类具有下表中的属性。 有关域类的信息，请参阅[了解模型、类和关系](../modeling/understanding-models-classes-and-relationships.md)。 有关如何使用这些属性的详细信息，请参阅[自定义和扩展域特定语言](../modeling/customizing-and-extending-a-domain-specific-language.md)。

|属性|说明|默认|
|-|-|-|
|访问修饰符|域类的访问级别（`public` 或 `internal`）。|`public`|
|自定义特性|用于向从此域类生成的源代码类添加特性。|\<none>|
|生成双派生|如果为 `True`，则将生成基类和分部类（来支持通过重写进行自定义）。 有关详细信息，请参阅[重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。|`False`|
|具有自定义构造函数|如果为 `True`，则在源代码中提供自定义构造函数。 有关详细信息，请参阅[重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。|`False`|
|继承修饰符|描述从域类生成的源代码类的继承类型（`none`、`abstract` 或 `sealed`）。|`none`|
|基类|如果派生此域类，则为基类的名称。|\<none>|
|名称|此域属性的名称。|当前名称|
|命名空间|此域属性的命名空间。|当前命名空间|
|备注|与此域类相关联的非正式说明。|\<none>|
|说明|用于记录已生成设计器的用户界面的说明。|\<none>|
|显示名称|将针对此域类在生成的设计器中显示的名称。|\<none>|
|帮助关键字|用于针对此域类索引 F1 帮助的可选关键字。|\<none>|

## <a name="see-also"></a>另请参阅

- [域特定语言工具术语表](/previous-versions/bb126564(v=vs.100))
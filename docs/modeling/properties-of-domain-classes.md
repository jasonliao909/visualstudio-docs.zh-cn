---
title: 域类的属性
description: 了解域类的各种属性，例如 Access 修饰符、自定义属性和生成双重派生。
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
ms.openlocfilehash: c8a426e27a4b959e4356484e6694407c9f56cf5a6be38253717dd7b5fe9479ad
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121428899"
---
# <a name="properties-of-domain-classes"></a>域类的属性
域类具有下表中的属性。 有关域类的信息，请参阅 [了解模型、类和关系](../modeling/understanding-models-classes-and-relationships.md)。 若要详细了解如何使用这些属性，请参阅自定义和扩展Domain-Specific [语言](../modeling/customizing-and-extending-a-domain-specific-language.md)。

|属性|说明|默认|
|-|-|-|
|访问修饰符|域类的访问级别（`public` 或 `internal`）。|`public`|
|自定义特性|用于向从此域类生成的源代码类添加属性。|\<none>|
|生成双派生|如果 `True` 为 ，则基类和分部 (都支持通过重写) 将生成自定义。 有关详细信息，请参阅 [重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。|`False`|
|具有自定义构造函数|如果 `True` 为 ，将在源代码中提供自定义构造函数。 有关详细信息，请参阅 [重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。|`False`|
|继承修饰符|描述从域类生成的源代码类的继承类型 (`none` `abstract` 或 `sealed`) 。|`none`|
|基类|如果派生此域类，则为基类的名称。|\<none>|
|名称|此域类的名称。|当前名称|
|命名空间|此域类的命名空间。|当前命名空间|
|说明|与此域类关联的非正式说明。|\<none>|
|说明|用于记录生成的设计器的 UI 的说明。|\<none>|
|显示名称|将在为此域类生成的设计器中显示的名称。|\<none>|
|帮助关键字|用于索引此域类的 F1 帮助的可选关键字。|\<none>|

## <a name="see-also"></a>请参阅

- [域特定语言工具术语表](/previous-versions/bb126564(v=vs.100))
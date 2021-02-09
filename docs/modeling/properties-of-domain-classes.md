---
title: 域类的属性
description: 了解域类的各种属性，例如访问修饰符、自定义属性和生成双精度派生。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Domain-Specific Language, domain class
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: cc86f04841a819423bc45c9220d6de80a5340b2d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99916000"
---
# <a name="properties-of-domain-classes"></a>域类的属性
域类具有下表中的属性。 有关域类的信息，请参阅 [了解模型、类和关系](../modeling/understanding-models-classes-and-relationships.md)。 有关如何使用这些属性的详细信息，请参阅 [自定义和扩展 Domain-Specific 语言](../modeling/customizing-and-extending-a-domain-specific-language.md)。

|属性|说明|默认|
|-|-|-|
|访问修饰符|域类的访问级别（`public` 或 `internal`）。|`public`|
|自定义特性|用于将特性添加到从此域类生成的源代码类中。|\<none>|
|生成双派生|如果为 `True` ，则将生成基类和分部类 (来支持通过重写进行自定义) 。 有关详细信息，请参阅 [重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。|`False`|
|具有自定义构造函数|如果为 `True` ，则在源代码中提供自定义构造函数。 有关详细信息，请参阅 [重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。|`False`|
|继承修饰符|描述从域类 (或) 生成的源代码类的继承类型 `none` `abstract` `sealed` 。|`none`|
|基类|如果此域类是派生的，则为基类的名称。|\<none>|
|“属性”|此域类的名称。|当前名称|
|命名空间|此域类的命名空间。|当前命名空间|
|说明|与此域类相关联的非正式注释。|\<none>|
|说明|用于为生成的设计器的 UI 记录文档的说明。|\<none>|
|显示名称|将在此域类的生成的设计器中显示的名称。|\<none>|
|帮助关键字|用于索引此域类的 F1 帮助的可选关键字。|\<none>|

## <a name="see-also"></a>另请参阅

- [域特定语言工具术语表](/previous-versions/bb126564(v=vs.100))
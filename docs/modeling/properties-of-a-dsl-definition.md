---
title: DSL 定义的属性
description: 了解 Dsldefinition.dsl 属性定义域特定语言定义属性，如版本编号。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Domain-Specific Language, definition file
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: cd32788e6b423b5ceb1ceafa54ad72cd3a885b15
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126663934"
---
# <a name="properties-of-a-dsl-definition"></a>DSL 定义的属性
Dsldefinition.dsl 属性定义 *域特定语言* 定义属性，如版本编号。 单击 *特定于域的语言设计器* 中的关系图区域时，dsldefinition.dsl 属性将显示在 "**属性**" 窗口中。

 有关详细信息，请参阅 [如何定义 Domain-Specific 语言](../modeling/how-to-define-a-domain-specific-language.md)。 有关如何使用这些属性的详细信息，请参阅 [自定义和扩展 Domain-Specific 语言](../modeling/customizing-and-extending-a-domain-specific-language.md)。

 Dsldefinition.dsl 具有下表中的属性：

|属性|说明|默认|
|-|-|-|
|访问修饰符|确定域类的访问修饰符是公共的还是内部的。|public|
|自定义特性|域类的自定义属性。<br /><br /> **注意** 使用 "浏览" 按钮添加属性。|\<none>|
|公司名称|系统注册表中当前公司名称的名称。|当前公司名称|
|名称|此域类的名称。|当前名称|
|命名空间|与此域类关联的命名空间。|当前命名空间|
|包 Guid|为此 DSL 生成的 Visual Studio 包的 guid。|\<none>|
|包命名空间|为此 DSL 生成的 Visual Studio 包的命名空间。|\<none>|
|产品名称|将为为此 DSL 生成的 Visual Studio 包注册的产品名称。|\<none>|
|备注|与此域类关联的注释。|\<none>|
|说明|此域类的说明。|\<none>|
|显示名称|将在此域类的生成的设计器中显示的名称。|\<none>|
|帮助关键字|与此域类关联的帮助关键字。|\<none>|
|构建|此域特定语言定义的递增生成号。|0|
|主要版本|此域特定语言定义的递增主要版本号。|1|
|次要版本|此域特定语言定义的递增次内部版本号。|0|
|修订|此域特定语言定义的递增修订版本号。|0|

## <a name="see-also"></a>另请参阅

- [域特定语言工具术语表](/previous-versions/bb126564(v=vs.100))
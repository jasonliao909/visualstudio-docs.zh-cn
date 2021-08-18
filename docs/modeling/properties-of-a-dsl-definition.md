---
title: DSL 定义的属性
description: 了解 DslDefinition 属性定义特定于域的语言定义属性，例如版本号。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122034248"
---
# <a name="properties-of-a-dsl-definition"></a>DSL 定义的属性
DslDefinition 属性定义 *特定于域的语言定义* 属性，例如版本号。 单击 "属性" 窗口中的关系图的打开区域时，DslDefinition 属性 *特定于域的语言设计器。*

 有关详细信息，请参阅 [How to Define a Domain-Specific Language](../modeling/how-to-define-a-domain-specific-language.md)。 若要详细了解如何使用这些属性，请参阅自定义和扩展Domain-Specific [语言](../modeling/customizing-and-extending-a-domain-specific-language.md)。

 DslDefinition 具有下表中的属性：

|属性|说明|默认|
|-|-|-|
|访问修饰符|确定域类的访问修饰符是公共的还是内部的。|public|
|自定义特性|域类的自定义定义属性。<br /><br /> **注意** 使用浏览按钮添加属性。|\<none>|
|公司名称|系统注册表中当前公司名称的名称。|当前公司名称|
|名称|此域类的名称。|当前名称|
|命名空间|与此域类附属的命名空间。|当前命名空间|
|包 Guid|为此 DSL 生成的Visual Studio包的 guid。|\<none>|
|包命名空间|为此 DSL 生成的Visual Studio包的命名空间。|\<none>|
|产品名称|将为为此 DSL 生成的服务包注册Visual Studio的名称。|\<none>|
|说明|与此域类关联的说明。|\<none>|
|说明|此域类的说明。|\<none>|
|显示名称|将在为此域类生成的设计器中显示的名称。|\<none>|
|帮助关键字|与此域类关联的 help 关键字。|\<none>|
|构建|此特定于域的语言定义的增量生成号。|0|
|主要版本|此特定于域的语言定义的增量主内部版本号。|1|
|次要版本|此特定于域的语言定义的增量次要内部版本号。|0|
|修订|此特定于域的语言定义的增量修订版本号。|0|

## <a name="see-also"></a>另请参阅

- [域特定语言工具术语表](/previous-versions/bb126564(v=vs.100))
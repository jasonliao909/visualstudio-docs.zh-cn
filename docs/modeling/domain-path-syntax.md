---
title: 域路径语法
description: 了解域路径语法以及 DSL 定义如何使用类似 XPath 的语法来查找模型中的特定元素。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, domain path
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: a5e3a80c09456cf50a021410a2df6ecc1ae65cc97e9897eb1682c054840df9e7
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121316807"
---
# <a name="domain-path-syntax"></a>域路径语法
DSL 定义使用类似 XPath 的语法在模型中查找特定元素。

 通常，你不必直接使用此语法。 在“DSL 详细信息”或“属性”窗口中，你可以在它所显示的位置中单击向下箭头并使用路径编辑器。 但是，在使用编辑器后，该路径将以此形式显示在字段中。

 域路径采用以下形式：

 *RelationshipName.PropertyName/!Role*

 ![CommentReferencesSubjects 引用关系](../modeling/media/dsl_reference.png)

 该语法将遍历模型树。 例如，上图中的域关系 **CommentReferencesSubjects** 具有"主题 **"** 角色。 路径段 **/！Subjectt** 指定路径在通过"主题"角色访问 **的元素上** 完成。

 每段都以域关系的名称开头。 如果遍历从元素到关系，则路径段显示为 *Relationship.PropertyName*。 如果跃点来自元素的链接，则路径段显示为 *Relationship/！RoleName*。

 使用斜杠分隔路径的语法。 每个路径段是都从元素到链接（关系的实例）或从链接到元素的跳跃。 路径段经常成对显示。 一个路径段表示从元素到链接的跳跃，而下一个段则表示从链接到另一端的元素的跳跃。 （任何链接还可以是关系本身的源或目标）。

 用于元素到链接跳跃的名称是角色的 `Property Name` 的值。 用于链接到元素跳跃的名称是目标角色名称。

## <a name="see-also"></a>另请参阅

- [了解模型、类和关系](../modeling/understanding-models-classes-and-relationships.md)

---
title: 在成员表示法与关联表示之间转换
description: 了解如何在类设计器中更改类图表示两种类型（从成员表示法到关联表示法）之间的关联关系的方式，反之亦然。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- notation, member
- association notation
- member notation
- notation, association
ms.assetid: 65881c5a-d251-4a36-ad0d-73d088436092
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: 3b97ff04abdbed42b9adb1a5fd2b41d4feca9931
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122124212"
---
# <a name="how-to-change-between-member-notation-and-association-notation-in-class-designer"></a>如何：在类设计器中在成员表示法与关联表示法之间转换

在“类设计器”中，可以更改类图表示两种类型（从成员表示法到关联表示法）之间的关联关系的方式，反之亦然。 通常，显示为关联行的成员可提供类型关联方式的有用可视化。

> [!NOTE]
> 关联关系可以表示为成员属性或字段。 若要将成员表示法更改为关联表示法，其中一种类型必须具有另一种类型的成员。 若要将关联表示法更改为成员表示法，则必须通过关联行连接这两种类型。 有关详细信息，请参阅[如何：创建类型之间的关联](how-to-create-associations-between-types.md)。 如果项目包含多个类图，则更改某个类图显示关联关系的方式仅会影响该类图。 若要更改另一个类图显示关联关系的方式，请打开或显示该类图并执行以下步骤。

## <a name="to-change-member-notation-to-association-notation"></a>将成员表示法更改为关联表示法

1. 从“解决方案资源管理器”中的项目节点打开类图 (.cd) 文件。

2. 在类图上的类型形状中，右键单击表示此关联的成员属性或字段，然后选择“显示为关联”。

    > [!TIP]
    > 如果在类型形状中没有看到属性或字段，则形状中的隔离舱处于折叠状态。 若要展开类型形状，请双击隔离舱名称或右键单击类型形状，然后选择“展开”。

    成员将从类型形状的隔离舱中消失，并将出现连接这两种类型的关联行。 关联行标有属性或字段的名称。

## <a name="to-change-association-notation-to-member-notation"></a>将关联表示法更改为成员表示法

在类图中，右键单击关联行，然后根据情况选择“显示为属性”或“显示为字段”。 关联行将消失，并且属性将显示在类图上类型形状内的相应隔离舱中。

## <a name="see-also"></a>另请参阅

- [如何：创建类型之间的继承](how-to-create-inheritance-between-types.md)
- [如何：查看类型之间的继承](how-to-view-inheritance-between-types.md)
- [查看类型和关系](designing-and-viewing-classes-and-types.md)
- [如何：可视化集合关联](how-to-visualize-a-collection-association.md)

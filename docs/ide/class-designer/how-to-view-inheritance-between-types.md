---
title: 查看类型之间的继承
description: 了解如何在类设计器中的类图上查看基类型和派生类型之间的继承关系。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.classdesigner.AssociationTypeNotFoundError
helpviewer_keywords:
- types [Visual Studio], inheritance
- types [Visual Studio], base
- types [Visual Studio], derived
ms.assetid: ea3f0ada-f53b-4fb1-9fb5-908286f5ec3e
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: ba469d7f4d9460b6c53ae37432d65a941e0d8fcb
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126735559"
---
# <a name="how-to-view-inheritance-between-types-in-class-designer"></a>如何：在类设计器中查看类型之间的继承

如果基类型和派生类型之间存在继承关系，则可在类设计器中的类图上查看这种关系。 若要创建两个类型之间的继承关系（如果不存在该关系），请参阅[如何：创建类型之间的继承](how-to-create-inheritance-between-types.md)。

## <a name="to-find-the-base-type"></a>查找基类型

1. 在类关系图中，单击要查看基类或基接口的类型。

2. 在“类图”菜单中，选择“显示基类”或“显示基接口”。

     类型的基类或基接口在关系图中显示为选中状态。 原来隐藏的所有继承连线现在都会出现在两个形状之间。

还可以右键单击想要显示其基类型的类型，然后选择“显示基类”或“显示基接口”。

## <a name="to-find-the-derived-types"></a>查找派生类型

1. 在类关系图中，单击要查看派生类或派生接口的类型。

2. 在“类图”菜单中，选择“显示派生类”或“显示派生接口”。

     该类型的派生类或派生接口即会出现在关系图中。 原来隐藏的所有继承连线现在都会出现在形状之间。

还可以右键单击想要显示其派生类型的类型，然后选择“显示派生类”或“显示派生接口”。

## <a name="see-also"></a>另请参阅

- [如何：创建类型之间的关联](how-to-create-associations-between-types.md)
- [查看类型和关系](designing-and-viewing-classes-and-types.md)

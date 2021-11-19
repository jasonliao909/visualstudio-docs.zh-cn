---
title: 如何：将实体添加到模型 | Microsoft Docs
description: 通过将实体控件从 Visual Studio 工具箱添加到业务数据连接 (BDC) 设计器来将实体添加到模型。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- EntityTool
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], entity
- Business Data Connectivity service [SharePoint development in Visual Studio], adding an entity
- Business Data Connectivity service [SharePoint development in Visual Studio], entity
- BDC [SharePoint development in Visual Studio], adding an entity
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 7905b4b3686c10ad9c6ac019253c71f94305f0b8
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665020"
---
# <a name="how-to-add-an-entity-to-a-model"></a>如何：将实体添加到模型
  若要创建实体，请将实体控件从 Visual Studio“工具箱”添加到业务数据连接 (BDC) 设计器。

### <a name="to-add-an-entity-to-the-model"></a>将实体添加到模型

1. 创建 BDC 项目，或打开现有 BDC 项目。 有关详细信息，请参阅[创建业务数据连接模型](../sharepoint/creating-a-business-data-connectivity-model.md)。

2. 在“工具箱”中，从“BusinessDataCatalog”组中将“实体”控件添加到设计器上  。

     新实体将显示在设计器上。 Visual Studio 将 `<Entity>` 元素添加到你项目中的 BDC 模型文件的 XML。 有关 Entity 元素特性的详细信息，请参阅 [Entity](/previous-versions/office/developer/sharepoint-2010/ee558325(v=office.14))。

3. 在设计器上，打开实体的快捷菜单，选择“添加”，然后选择“标识符” 。

     实体上会显示一个新的标识符。

    > [!NOTE]
    > 可以在“属性”窗口中更改实体和标识符的名称。

4. 定义类中实体的字段。 你可以向项目添加新的类或使用通过对象关系设计器（O/R 设计器）等其他工具创建的现有类。 以下示例演示名为 Contact 的实体类。

    :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sp_bdc_entity_data_class/bdcmodel1/contact.cs" id="Snippet1":::
    :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_bdc_entity_data_class/bdcmodel1/contact.vb" id="Snippet1":::

## <a name="see-also"></a>另请参阅
- [如何：添加 Creator 方法](../sharepoint/how-to-add-a-creator-method.md)
- [如何：添加 Deleter 方法](../sharepoint/how-to-add-a-deleter-method.md)
- [如何：添加 Updater 方法](../sharepoint/how-to-add-an-updater-method.md)
- [如何：添加 Finder 方法](../sharepoint/how-to-add-a-finder-method.md)
- [如何：添加特定的 Finder 方法](../sharepoint/how-to-add-a-specific-finder-method.md)

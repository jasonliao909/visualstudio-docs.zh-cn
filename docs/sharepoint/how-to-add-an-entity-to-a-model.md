---
title: 如何：将实体添加到模型|Microsoft Docs
description: 通过将实体控件从"工具箱"添加到 BDC Visual Studio设计器中的"业务数据连接" (模型) 实体。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122093185"
---
# <a name="how-to-add-an-entity-to-a-model"></a>如何：向模型添加实体
  若要创建实体，请从"Visual Studio工具箱"将实体控件添加到BDC) 设计器中的"业务数据 (连接" 。

### <a name="to-add-an-entity-to-the-model"></a>向模型添加实体

1. 创建 BDC 项目，或打开现有 BDC 项目。 有关详细信息，请参阅[创建业务数据连接模型](../sharepoint/creating-a-business-data-connectivity-model.md)。

2. 在" **工具箱"** 中，从 **BusinessDataCatalog** 组向设计器 **添加实体** 控件。

     新实体将显示在设计器上。 Visual Studio向 `<Entity>` 项目中 BDC 模型文件的 XML 添加元素。 有关 Entity 元素的属性详细信息，请参阅 [实体](/previous-versions/office/developer/sharepoint-2010/ee558325(v=office.14))。

3. 在设计器上，打开实体的快捷菜单，选择"**添加**"，然后选择"标识符 **"。**

     实体上会显示一个新标识符。

    > [!NOTE]
    > 可以在"属性"窗口中更改实体的名称 **和标识符。**

4. 定义类中实体的字段。 可以将新类添加到项目，或使用使用其他工具（如 对象关系设计器 (O/R 设计器）创建的现有) 。 以下示例演示名为 Contact 的实体类。

    :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sp_bdc_entity_data_class/bdcmodel1/contact.cs" id="Snippet1":::
    :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_bdc_entity_data_class/bdcmodel1/contact.vb" id="Snippet1":::

## <a name="see-also"></a>请参阅
- [如何：添加 Creator 方法](../sharepoint/how-to-add-a-creator-method.md)
- [如何：添加 Deleter 方法](../sharepoint/how-to-add-a-deleter-method.md)
- [如何：添加 Updater 方法](../sharepoint/how-to-add-an-updater-method.md)
- [如何：添加查找器方法](../sharepoint/how-to-add-a-finder-method.md)
- [如何：添加特定的 Finder 方法](../sharepoint/how-to-add-a-specific-finder-method.md)

---
title: 如何：添加 Finder 方法 | Microsoft Docs
description: 在 Visual Studio 中添加 Finder 方法，这将使业务数据连接 (BDC) 服务能够在 SharePoint Web 部件或列表中显示实体列表。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], get entities
- Business Data Connectivity service [SharePoint development in Visual Studio], return entities
- BDC [SharePoint development in Visual Studio], return entities
- Business Data Connectivity service [SharePoint development in Visual Studio], Finder method
- Business Data Connectivity service [SharePoint development in Visual Studio], get entities
- BDC [SharePoint development in Visual Studio], Finder method
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 3df15148f2a42d0dea7a258d17097d515a1249e9
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600637"
---
# <a name="how-to-add-a-finder-method"></a>如何：添加 Finder 方法
  若要使业务数据连接 (BDC) 服务能够在 Web 部件或列表中显示实体列表，必须创建 Finder 方法。 Finder 方法是一种特殊的方法，它可以返回实体实例的集合。 有关详细信息，请参阅[设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)。

### <a name="to-create-a-finder-method"></a>创建 Finder 方法

1. 在“BDC 设计器”上，选择一个实体。

    有关详细信息，请参阅[如何：向模型添加实体](../sharepoint/how-to-add-an-entity-to-a-model.md)。

2. 在菜单栏上，选择“视图” > “其他窗口” > “BDC 方法详细信息”。

    “BDC 方法详细信息”窗口将打开。 有关“BDC 方法详细信息”窗口的详细信息，请参阅 [BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)。

3. 在“添加方法”列表中，选择“创建 Finder 方法”。

    Visual Studio 添加了一个方法、一个返回参数和一个类型描述符。

4. 将类型描述符配置为一个实体集合类型描述符。 若要详细了解如何创建实体集合类型描述符，请参阅[如何：定义参数的类型描述符](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)。

   > [!NOTE]
   > 如果你已经向实体添加了特定的 Finder 方法，则无需执行此步骤。 Visual Studio 将使用你在特定的 Finder 方法中定义的类型描述符。

5. 在“解决方案资源管理器”中，打开为实体生成的服务代码文件的快捷菜单，然后选择“查看代码”。 有关服务代码文件的详细信息，请参阅[创建业务数据连接模型](../sharepoint/creating-a-business-data-connectivity-model.md)。

6. 向 Finder 方法添加代码。 此代码执行以下任务：

   - 从数据源中检索数据。

   - 将实体列表返回给 BDC 服务。

     以下示例使用 SQL Server AdventureWorks 示例数据库中的数据返回 `Contact` 实体的集合。

   > [!NOTE]
   > 将 `ServerName` 字段的值替换为你的服务器名称。

    :::code language="csharp" source="../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs" id="Snippet2":::
    :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb" id="Snippet2":::

## <a name="see-also"></a>另请参阅
- [BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)
- [设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)
- [如何：添加特定的 Finder 方法](../sharepoint/how-to-add-a-specific-finder-method.md)
- [如何：添加 Creator 方法](../sharepoint/how-to-add-a-creator-method.md)
- [如何：添加 Deleter 方法](../sharepoint/how-to-add-a-deleter-method.md)
- [如何：添加 Updater 方法](../sharepoint/how-to-add-an-updater-method.md)
- [如何：将参数添加到方法](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [如何：定义方法实例](../sharepoint/how-to-define-a-method-instance.md)

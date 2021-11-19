---
title: 如何：添加 Creator 方法 | Microsoft Docs
description: 了解如何添加 Creator 方法，该方法将新数据添加到 SharePoint 中业务数据连接 (BDC) 服务中的实体的数据源。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], Creator
- BDC [SharePoint development in Visual Studio], adding entity instances
- Business Data Connectivity service [SharePoint development in Visual Studio], adding entities
- Business Data Connectivity service [SharePoint development in Visual Studio], adding entity instances
- BDC [SharePoint development in Visual Studio], adding entities
- Business Data Connectivity service [SharePoint development in Visual Studio], Creator
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: adec17c0a381edb3587da50d3d9e3e8aedbc6cdd
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600640"
---
# <a name="how-to-add-a-creator-method"></a>如何：添加 Creator 方法
  Creator 方法向实体的数据源添加新数据。 当用户在基于模型的列表的功能区上选择“新建项”按钮时，业务数据连接 (BDC) 服务调用此方法 。 有关详细信息，请参阅[设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)。

### <a name="to-add-a-creator-method"></a>添加 Creator 方法

1. 在“BDC 设计器”上，选择一个实体。

2. 在菜单栏上，选择“视图” > “其他窗口” >“BDC 方法详细信息”  。

    “BDC 方法详细信息”窗口将打开。 有关该窗口的详细信息，请参阅 [BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)。

3. 在“添加方法”列表中，选择“创建 Creator 方法” 。

    Visual Studio 将以下元素添加到模型中，这些元素显示在“BDC 方法详细信息”窗口中。

   - 名为 Create 的方法。

   - 该方法的输入参数。

   - 该方法的返回参数。

   - 参数的类型描述符。

   - 该方法的方法实例。

     有关详细信息，请参阅[设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)。

4. 在“解决方案资源管理器”中，打开为实体生成的服务代码文件的快捷菜单，然后选择“查看代码” 。

    实体服务代码文件将在代码编辑器中打开。 有关该实体服务代码文件的详细信息，请参阅[创建业务数据连接模型](../sharepoint/creating-a-business-data-connectivity-model.md)。

5. 将代码添加到向数据源添加数据的 Creator 方法。 以下示例向 SQL Server AdventureWorks 示例数据库添加联系人。

   > [!NOTE]
   > 将 `ServerName` 字段的值替换为你的服务器名称。

    :::code language="csharp" source="../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs" id="Snippet4":::
    :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb" id="Snippet4":::

## <a name="see-also"></a>另请参阅
- [设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)
- [如何：添加 Finder 方法](../sharepoint/how-to-add-a-finder-method.md)
- [如何：添加特定的 Finder 方法](../sharepoint/how-to-add-a-specific-finder-method.md)
- [如何：添加 Deleter 方法](../sharepoint/how-to-add-a-deleter-method.md)
- [如何：添加 Updater 方法](../sharepoint/how-to-add-an-updater-method.md)
- [BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)
- [如何：将参数添加到方法](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [如何：定义方法实例](../sharepoint/how-to-define-a-method-instance.md)

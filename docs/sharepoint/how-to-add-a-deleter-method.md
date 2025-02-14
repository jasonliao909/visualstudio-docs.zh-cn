---
title: 如何：添加 Deleter 方法 | Microsoft Docs
description: 了解如何在 Visual Studio 的 BDC 设计器中添加 Deleter 方法，以便最终用户可以从 SharePoint 站点上的外部列表中删除数据记录。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], deleting data
- Business Data Connectivity service [SharePoint development in Visual Studio], Deleter
- BDC [SharePoint development in Visual Studio], Deleter
- BDC [SharePoint development in Visual Studio], removing data
- BDC [SharePoint development in Visual Studio], deleting entity instances
- Business Data Connectivity service [SharePoint development in Visual Studio], deleting entity instances
- Business Data Connectivity service [SharePoint development in Visual Studio], deleting data
- Business Data Connectivity service [SharePoint development in Visual Studio], removing data
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: b4c42d5020ff78a2d2e66715edb913fe8cea127e
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600639"
---
# <a name="how-to-add-a-deleter-method"></a>如何：添加 Deleter 方法
  通过将 Deleter 方法添加到模型，可让最终用户从 SharePoint 站点的外部列表中删除数据记录。 有关详细信息，请参阅[设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)。

### <a name="to-create-a-deleter-method"></a>创建 Deleter 方法

1. 在“BDC 设计器”上，选择一个实体。

2. 在菜单栏上，选择“视图” > “其他窗口” > “BDC 方法详细信息”  。

    “BDC 方法详细信息”窗口将打开。 有关此窗口的详细信息，请参阅 [BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)。

3. 在“添加方法”列表中，选择“创建 Deleter 方法” 。

    Visual Studio 将以下元素添加到模型中。 这些元素显示在“BDC 方法详细信息”窗口中。

   - 名为“Create”的方法。

   - 该方法的输入参数。

   - 参数的类型描述符。

   - 该方法的方法实例。

     有关详细信息，请参阅[设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)。

4. 在“解决方案资源管理器”中，打开为实体生成的服务代码文件的快捷菜单，然后选择“查看代码” 。

    实体服务代码文件将在代码编辑器中打开。 有关该实体服务代码文件的详细信息，请参阅[创建业务数据连接模型](../sharepoint/creating-a-business-data-connectivity-model.md)。

5. 将代码添加到 Deleter 方法以删除记录。 以下示例通过为 SQL Server 使用 AdventureWorks 示例数据库，从销售订单中删除行项目。

   > [!NOTE]
   > 此示例中的方法采用两个输入参数。

   > [!NOTE]
   > 将 `ServerName` 字段的值替换为你的服务器名称。

    :::code language="csharp" source="../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/salesorderdetailservice.cs" id="Snippet6":::
    :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/salesorderdetailservice.vb" id="Snippet6":::

## <a name="see-also"></a>另请参阅
- [设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)
- [如何：添加 Finder 方法](../sharepoint/how-to-add-a-finder-method.md)
- [如何：添加特定的 Finder 方法](../sharepoint/how-to-add-a-specific-finder-method.md)
- [如何：添加 Creator 方法](../sharepoint/how-to-add-a-creator-method.md)
- [如何：添加 Updater 方法](../sharepoint/how-to-add-an-updater-method.md)
- [BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)
- [如何：将参数添加到方法](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [如何：定义方法实例](../sharepoint/how-to-define-a-method-instance.md)

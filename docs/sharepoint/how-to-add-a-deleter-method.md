---
title: 如何：添加删除器方法 |Microsoft Docs
description: 了解如何在 Visual Studio 的 BDC 设计器中添加删除器方法，使最终用户可以从 SharePoint 网站上的外部列表中删除数据记录。
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
ms.openlocfilehash: 2ecdb9a9dde1ac10e1d4037078fe272f7e3229952830bc6fca3308e8f7bf4105
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121385310"
---
# <a name="how-to-add-a-deleter-method"></a>如何：添加删除器方法
  您可以通过向模型中添加删除器方法，使最终用户可以从 SharePoint 站点的外部列表中删除数据记录。 有关详细信息，请参阅[设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)。

### <a name="to-create-a-deleter-method"></a>创建删除器方法

1. 在 **BDC 设计器** 中选择一个实体。

2. 在菜单栏上，选择 "**查看**  >  **其他 Windows**  >  **BDC 方法详细信息**"。

    此时将打开 " **BDC 方法详细信息** " 窗口。 有关此窗口的详细信息，请参阅 [BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)。

3. 在 " **添加方法** " 列表中，选择 " **创建删除器方法**"。

    Visual Studio 将以下元素添加到模型中。 这些元素出现在 " **BDC 方法详细信息** " 窗口中。

   - 名为 **Delete** 的方法。

   - 方法的输入参数。

   - 参数的类型描述符。

   - 方法的方法实例。

     有关详细信息，请参阅[设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)。

4. 在 **解决方案资源管理器** 中，打开为实体生成的服务代码文件的快捷菜单，然后选择 " **查看代码**"。

    实体服务代码文件将在代码编辑器中打开。 有关实体服务代码文件的详细信息，请参阅 [创建业务数据连接模型](../sharepoint/creating-a-business-data-connectivity-model.md)。

5. 向删除器方法添加代码以删除记录。 下面的示例通过使用 SQL Server 的 AdventureWorks 示例数据库，从销售订单中删除行项。

   > [!NOTE]
   > 此示例中的方法使用两个输入参数。

   > [!NOTE]
   > 将字段的值替换 `ServerName` 为服务器的名称。

    :::code language="csharp" source="../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/salesorderdetailservice.cs" id="Snippet6":::
    :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/salesorderdetailservice.vb" id="Snippet6":::

## <a name="see-also"></a>请参阅
- [设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)
- [如何：添加 Finder 方法](../sharepoint/how-to-add-a-finder-method.md)
- [如何：添加特定的 Finder 方法](../sharepoint/how-to-add-a-specific-finder-method.md)
- [如何：添加 Creator 方法](../sharepoint/how-to-add-a-creator-method.md)
- [如何：添加更新程序方法](../sharepoint/how-to-add-an-updater-method.md)
- [BDC 模型设计工具概述](../sharepoint/bdc-model-design-tools-overview.md)
- [如何：向方法添加参数](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [如何：定义方法实例](../sharepoint/how-to-define-a-method-instance.md)

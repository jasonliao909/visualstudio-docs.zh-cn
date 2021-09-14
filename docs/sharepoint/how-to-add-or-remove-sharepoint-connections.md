---
title: 如何：添加或删除SharePoint连接|Microsoft Docs
description: 使用"SharePoint"窗口的"SharePoint连接"节点添加服务器资源管理器或删除Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, browsing SharePoint sites
- SharePoint development in Visual Studio, SharePoint Connections
- SharePoint Connections [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 90923440dcbe5201c30a1b8c97d1275cd9719f1c
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600605"
---
# <a name="how-to-add-or-remove-sharepoint-connections"></a>如何：添加或删除 SharePoint 连接
  服务器资源管理器浏览SharePoint以及数据连接。 但是，在浏览 SharePoint 站点的内容之前，必须将其添加到"SharePoint **连接"** 节点。

### <a name="to-add-a-sharepoint-site-to-the-sharepoint-connections-node"></a>将SharePoint站点添加到 SharePoint 连接节点

1. 在菜单栏上，选择" **视图"，** 然后选择 **服务器资源管理器"**。

2. 在 **服务器资源管理器** 中，选择"SharePoint连接"节点，然后在菜单栏上选择"工具  >  **""添加SharePoint连接"。**

3. 在 **"添加SharePoint连接**"框中，输入SharePoint [!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)] 站点 (，例如 http://testserver/sites/unittests) 。

### <a name="to-delete-a-sharepoint-site-from-the-sharepoint-connections-node"></a>从"SharePoint连接"节点中删除SharePoint站点

1. 在菜单栏上，选择"查看 **"，服务器资源管理器****打开** 服务器资源管理器。 

2. 展开 **"SharePoint连接**"节点，SharePoint要从 **中删除的站点** 服务器资源管理器。

3. 选择站点，然后在菜单栏上选择"编辑 **删除**  >  **"。**

    > [!NOTE]
    > 此步骤不会删除基础站点;它仅从 服务器资源管理器 **连接。**

## <a name="see-also"></a>另请参阅
- [使用服务器资源管理器浏览 SharePoint 连接](../sharepoint/browsing-sharepoint-connections-using-server-explorer.md)

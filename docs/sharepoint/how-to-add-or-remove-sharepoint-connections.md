---
title: 如何：添加或删除 SharePoint 连接 | Microsoft Docs
description: 使用 Visual Studio 的“服务器资源管理器”窗口中的“SharePoint 连接”节点添加或删除 SharePoint 连接。
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
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600605"
---
# <a name="how-to-add-or-remove-sharepoint-connections"></a>如何：添加或删除 SharePoint 连接
  服务器资源管理器使你可以浏览 SharePoint 站点以及数据连接。 但是，你必须将 SharePoint 站点的内容添加到“SharePoint 连接”节点中，然后才能浏览该站点的内容。

### <a name="to-add-a-sharepoint-site-to-the-sharepoint-connections-node"></a>将 SharePoint 站点添加到 SharePoint 连接 节点

1. 在菜单栏上，依次选择“视图”、“服务器资源管理器”。

2. 在“服务器资源管理器”中，选择“SharePoint 连接”节点，然后在菜单栏上选择“工具” > “添加 SharePoint 连接”   。

3. 在“添加 SharePoint 连接”框中，输入 SharePoint 站点的 [!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)]（例如， http://testserver/sites/unittests) ）。

### <a name="to-delete-a-sharepoint-site-from-the-sharepoint-connections-node"></a>从 SharePoint 连接节点中删除 SharePoint 站点

1. 在菜单栏上，依次选择“视图”、“服务器资源管理器”以打开“服务器资源管理器”。

2. 展开“SharePoint 连接”节点以显示要从“服务器资源管理器”中删除的 SharePoint 站点。

3. 选择站点，然后在菜单栏上选择“编辑” > “删除”。

    > [!NOTE]
    > 此步骤不会删除基础站点；它仅从“服务器资源管理器”中删除连接。

## <a name="see-also"></a>另请参阅
- [使用服务器资源管理器浏览 SharePoint 连接](../sharepoint/browsing-sharepoint-connections-using-server-explorer.md)

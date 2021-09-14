---
title: 扩展SharePoint连接节点服务器资源管理器 |Microsoft Docs
titleSuffix: ''
description: 在 SharePoint 中扩展"服务器资源管理器连接"Visual Studio。 将自定义属性添加到节点。 获取内置节点的数据。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint Connections [SharePoint development in Visual Studio], extending a node
- SharePoint development in Visual Studio, extending SharePoint Connections node in Server Explorer
- SharePoint Connections [SharePoint development in Visual Studio], creating a new node type
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: c6ae20393f60ffe0e17cee9baf85c1572cea32ac
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600658"
---
# <a name="extend-the-sharepoint-connections-node-in-server-explorer"></a>扩展服务器资源管理器中的“SharePoint 连接”节点
  在 Visual Studio 中，可以使用"SharePoint"窗口中的"SharePoint **连接"节点** 连接到开发 **服务器资源管理器站点。** 此节点在分层树视图中显示SharePoint站点的许多组件。 例如，可以在本地网站上查看列表、文档库和内容类型。 有关使用 服务器资源管理器 **连接到本地** SharePoint 站点SharePoint，请参阅使用 SharePoint [浏览服务器资源管理器。](../sharepoint/browsing-sharepoint-connections-using-server-explorer.md)

 可以通过为现有 **SharePoint** 扩展，或者创建自定义节点类型并添加到节点层次结构，来扩展"连接"节点。

## <a name="tasks-for-extending-the-sharepoint-connections-node"></a>用于扩展 SharePoint 连接节点的任务
 若要扩展现有节点，请创建Visual Studio接口的扩展 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> 。 扩展节点时，可以将功能添加到节点，例如你自己的快捷菜单项或自定义属性。 有关详细信息，请参阅[如何：扩展](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)SharePoint 中的 服务器资源管理器 节点。

 若要创建自定义节点类型，请创建Visual Studio接口的扩展 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider> 。 如果要显示默认未显示在SharePoint站点的组件，请 **服务器资源管理器** 节点。 例如 **，服务器资源管理器** 不显示 SharePoint 站点的 Web 部件库，但可以添加执行此操作的自定义节点。 有关详细信息，请参阅[如何：将自定义SharePoint](../sharepoint/how-to-add-a-custom-sharepoint-node-to-server-explorer.md)节点添加到服务器资源管理器演练[：扩展服务器资源管理器以显示Web 部件。](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)

## <a name="add-custom-properties-to-nodes"></a>将自定义属性添加到节点
 扩展节点或创建自定义节点类型时，可以将自定义属性添加到该节点。 选择节点时 **，属性** 将显示在"属性"窗口中。

 有两种类型的自定义属性可以添加到节点：

- 显示来自数据库站点的一组只读SharePoint的属性。 数据描述SharePoint表示的组件。 有关演示如何执行此操作的演练，请参阅演练：扩展服务器资源管理器 [以显示 Web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)。

- 显示自定义读/写数据的属性。 有关演示如何执行此操作的代码示例，请参阅如何：在 SharePoint[中扩展服务器资源管理器。](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)

## <a name="get-data-for-built-in-nodes"></a>获取内置节点的数据
 由 Visual Studio 提供的所有内置节点均包含一些有关SharePoint表示的组件的数据。 例如，表示 SharePoint 站点上的列表的节点提供有关该列表的一些数据，例如列表的默认视图的标题和 URL。

 若要访问此数据，请从表示你感兴趣的节点的 对象的 属性 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode> 中检索数据对象。 数据对象的类型取决于节点的类型。

 下面的代码示例演示如何获取列表节点的数据对象。 若要在较大示例的上下文中查看此示例，请参阅如何：获取中内置节点[SharePoint的数据](../sharepoint/how-to-get-data-for-a-built-in-sharepoint-node-in-server-explorer.md)服务器资源管理器。

 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/serverexplorerextensionnodeinfo.vb" id="Snippet11":::
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/serverexplorerextensionnodeinfo.cs" id="Snippet11":::

 下表列出了每个内置节点类型的数据对象类型。

|节点类型|数据对象类型|
|---------------|----------------------|
|SharePoint站点节点|<xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerSiteNodeInfo>|
|内容类型|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IContentTypeNodeInfo>|
|Feature|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IFeatureNodeInfo>|
|字段|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IFieldNodeInfo>|
|列出|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IListNodeInfo>|
|列表模板|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IListTemplateNodeInfo>|
|Microsoft (视图。SharePoint。SPView) |<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IListViewNodeInfo>|
|工作流关联|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IWorkflowAssociationNodeInfo>|
|工作流模板|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IWorkflowTemplateNodeInfo>|

 有关使用 属性的信息 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> ，请参阅[将自定义](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)数据与SharePoint扩展关联。

## <a name="see-also"></a>另请参阅
- [演练：扩展服务器资源管理器以显示 Web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
- [如何：扩展SharePoint节点服务器资源管理器](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)
- [如何：将自定义SharePoint节点添加到服务器资源管理器](../sharepoint/how-to-add-a-custom-sharepoint-node-to-server-explorer.md)
- [如何：获取中内置节点SharePoint的数据服务器资源管理器](../sharepoint/how-to-get-data-for-a-built-in-sharepoint-node-in-server-explorer.md)
- [将自定义数据与 SharePoint 工具扩展关联](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)
- [使用服务器资源管理器浏览 SharePoint 连接](../sharepoint/browsing-sharepoint-connections-using-server-explorer.md)
- [扩展 Visual Studio 中的 SharePoint 工具](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)

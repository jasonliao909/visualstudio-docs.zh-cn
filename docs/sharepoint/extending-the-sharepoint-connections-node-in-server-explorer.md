---
title: 扩展服务器资源管理器中的 SharePoint 连接节点 | Microsoft Docs
titleSuffix: ''
description: 扩展 Visual Studio 中“服务器资源管理器”窗口中的 SharePoint 节点。 向节点添加自定义属性。 获取内置节点的数据。
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
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600658"
---
# <a name="extend-the-sharepoint-connections-node-in-server-explorer"></a>扩展服务器资源管理器中的“SharePoint 连接”节点
  在 Visual Studio 中，通过使用“服务器资源管理器”窗口中的“SharePoint 连接”节点，可以连接到开发计算机上的本地 SharePoint 站点 。 此节点在分层树状视图中显示本地 SharePoint 站点的许多组件。 例如，可以在本地网站上查看列表、文档库和内容类型。 有关使用“服务器资源管理器”连接到本地 SharePoint 站点的详细信息，请参阅[使用 Server Explorer 浏览 SharePoint 连接](../sharepoint/browsing-sharepoint-connections-using-server-explorer.md)。

 可以通过为现有节点创建扩展，或通过创建自定义节点类型并将其添加到节点层次结构来扩展“SharePoint 连接”节点。

## <a name="tasks-for-extending-the-sharepoint-connections-node"></a>用于扩展 SharePoint 连接节点的任务
 若要扩展现有节点，请创建执行 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> 接口的 Visual Studio 扩展。 扩展节点时，可以将功能添加到节点，例如你自己的快捷菜单项或自定义属性。 有关详细信息，请参阅[操作说明：扩展服务器资源管理器中的 SharePoint 节点](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)。

 若要创建自定义节点类型，请创建执行 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider> 接口的 Visual Studio 扩展。 如果想要显示默认情况下不显示在“服务器资源管理器”中的 SharePoint 站点组件，则创建自定义节点。 例如，“服务器资源管理器”默认不会显示 SharePoint 站点的 Web 部件库，但可以添加执行此操作的自定义节点。 有关详细信息，请参阅[操作说明：将自定义 SharePoint 节点添加到服务器资源管理器](../sharepoint/how-to-add-a-custom-sharepoint-node-to-server-explorer.md)和[演练：扩展服务器资源管理器以显示 Web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)。

## <a name="add-custom-properties-to-nodes"></a>向节点添加自定义属性
 扩展节点或创建自定义节点类型时，可以将自定义属性添加到该节点。 选择节点时，“属性”窗口中会显示各个属性。

 有两种类型的自定义属性可以添加到节点：

- 显示来自 SharePoint 站点的一组只读数据的属性。 数据描述节点代表的 SharePoint 组件。 有关演示如何执行此操作的演练，请参阅[演练：扩展服务器资源管理器以显示 Web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)。

- 显示自定义读/写数据的属性。 有关演示如何执行此操作的代码示例，请参阅[操作说明：扩展服务器资源管理器中的 SharePoint 节点](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)。

## <a name="get-data-for-built-in-nodes"></a>获取内置节点的数据
 由 Visual Studio 提供的所有内置节点都包含一些有关它们所表示的 SharePoint 组件的数据。 例如，表示 SharePoint 站点上列表的节点提供有关该列表的一些数据，例如列表的默认视图的标题和 URL。

 若要访问此数据，请从表示你感兴趣的节点的 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode> 对象的 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> 属性中检索数据对象。 数据对象的类型取决于节点的类型。

 下面的代码示例演示了如何获取列表节点的数据对象。 若要在较大示例的上下文中查看此示例，请参阅[操作说明：获取服务器资源管理器中内置 SharePoint 节点的数据](../sharepoint/how-to-get-data-for-a-built-in-sharepoint-node-in-server-explorer.md)。

 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/serverexplorerextensionnodeinfo.vb" id="Snippet11":::
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/serverexplorerextensionnodeinfo.cs" id="Snippet11":::

 下表列出了每个内置节点类型的数据对象类型。

|节点类型|数据对象类型|
|---------------|----------------------|
|SharePoint 站点节点|<xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerSiteNodeInfo>|
|内容类型|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IContentTypeNodeInfo>|
|功能|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IFeatureNodeInfo>|
|字段|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IFieldNodeInfo>|
|列出|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IListNodeInfo>|
|列表模板|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IListTemplateNodeInfo>|
|列表视图 (Microsoft.SharePoint.SPView)|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IListViewNodeInfo>|
|工作流关联|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IWorkflowAssociationNodeInfo>|
|工作流模板|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IWorkflowTemplateNodeInfo>|

 有关使用 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> 属性的详细信息，请参阅[将自定义数据与 SharePoint 工具扩展相关联](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)。

## <a name="see-also"></a>另请参阅
- [演练：扩展服务器资源管理器以显示 Web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
- [操作说明：扩展服务器资源管理器中的 SharePoint 节点](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)
- [操作说明：将自定义 SharePoint 节点添加到服务器资源管理器](../sharepoint/how-to-add-a-custom-sharepoint-node-to-server-explorer.md)
- [操作说明：为服务器资源管理器中的内置 SharePoint 节点获取数据](../sharepoint/how-to-get-data-for-a-built-in-sharepoint-node-in-server-explorer.md)
- [将自定义数据与 SharePoint 工具扩展相关联](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)
- [使用服务器资源管理器浏览 SharePoint 连接](../sharepoint/browsing-sharepoint-connections-using-server-explorer.md)
- [扩展 Visual Studio 中的 SharePoint 工具](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)

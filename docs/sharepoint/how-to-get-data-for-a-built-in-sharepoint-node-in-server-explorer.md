---
title: 在服务器资源管理器中获取内置 SharePoint 节点数据
titleSuffix: ''
description: 在 Visual Studio 的“服务器资源管理器”窗口中，获取内置 SharePoint 节点的基础 SharePoint 数据。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint Connections [SharePoint development in Visual Studio], extending a node
- SharePoint development in Visual Studio, extending SharePoint Connections node in Server Explorer
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 322a5278ab2b21b02fb501523bfe9663948ae0fe
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126666180"
---
# <a name="how-to-get-data-for-a-built-in-sharepoint-node-in-server-explorer"></a>操作说明：在服务器资源管理器中获取内置 SharePoint 节点数据
  对于“服务器资源管理器”中的每个内置 SharePoint 节点，你都可以获取该节点表示的基础 SharePoint 组件的数据。 有关详细信息，请参阅[扩展服务器资源管理器中的 SharePoint 连接节点](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)。

## <a name="example"></a>示例
 下面的代码示例演示如何获取列表节点在“服务器资源管理器”中表示的基础 SharePoint 列表的数据。 默认情况下，列表节点有一个“在浏览器中查看”上下文菜单项，你可以单击它在 Web 浏览器中打开列表。 此示例通过添加“在 Visual Studio 中查看”上下文菜单项来扩展列表节点，该菜单项在 Visual Studio 中直接打开列表。 此代码访问节点的列表数据，以获取要在 Visual Studio 中打开的列表 URL。

 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/serverexplorerextensionnodeinfo.vb" id="Snippet10":::
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/serverexplorerextensionnodeinfo.cs" id="Snippet10":::

 此示例使用 SharePoint 项目服务获取用于在 Visual Studio 中打开列表的 <xref:EnvDTE.DTE> 对象。 有关 SharePoint 项目服务的详细信息，请参阅[使用 SharePoint 项目服务](../sharepoint/using-the-sharepoint-project-service.md)。

 有关为 SharePoint 节点创建扩展的基本任务的详细信息，请参阅[操作说明：在服务器资源管理器中扩展 SharePoint 节点](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)。

## <a name="compile-the-code"></a>编译代码
 本示例需要引用以下程序集：

- EnvDTE

- Microsoft.VisualStudio.SharePoint

- Microsoft.VisualStudio.SharePoint.Explorer.Extensions

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>部署扩展
 若要部署服务器资源管理器扩展，请为程序集以及要随扩展分发的任何其他文件创建 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 扩展 (VSIX) 包。 有关详细信息，请参阅[在 Visual Studio 中部署 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>另请参阅
- [扩展服务器资源管理器中的“SharePoint 连接”节点](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [操作说明：扩展服务器资源管理器中的 SharePoint 节点](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)
- [使用 SharePoint 项目服务](../sharepoint/using-the-sharepoint-project-service.md)
- [在 Visual Studio 中部署 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)

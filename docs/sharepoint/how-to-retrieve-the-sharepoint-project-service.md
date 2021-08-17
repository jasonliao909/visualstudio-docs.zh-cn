---
title: 如何：检索SharePoint Project服务|Microsoft Docs
description: 了解如何访问项目SharePoint 项目服务扩展、服务器资源管理器扩展或其他扩展Visual Studio扩展。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint project service
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: aa962e3b82ec994cfceee3d82566029c536af283
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122047616"
---
# <a name="how-to-retrieve-the-sharepoint-project-service"></a>如何：检索SharePoint 项目服务
  可以在以下SharePoint 项目服务访问应用程序：

- 项目系统的扩展SharePoint，如项目扩展、项目项扩展或项目项类型定义。 有关这些扩展类型详细信息，请参阅扩展 SharePoint[项目系统](../sharepoint/extending-the-sharepoint-project-system.md)。

- 中 SharePoint **连接** 节点的 **服务器资源管理器。** 有关这些扩展类型详细信息，请参阅 扩展 SharePoint[连接节点服务器资源管理器。](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)

- 另一Visual Studio扩展，例如 VSPackage。

## <a name="retrieve-the-service-in-project-system-extensions"></a>检索项目系统扩展中的服务
 在项目系统SharePoint扩展中，项目服务 对象的 属性 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject.ProjectService%2A> 访问该 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject> 扩展。

 还可通过以下项目服务检索数据。

#### <a name="to-retrieve-the-service-in-a-project-extension"></a>在项目扩展中检索服务

1. 在 接口的实现 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> 中，找到 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension.Initialize%2A> 方法。

2. 使用 *projectService* 参数访问服务。

     下面的代码示例演示如何使用 项目服务将消息写入简单项目扩展中的"输出"窗口和"错误列表"窗口。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spextensibility.projectservice.fromprojectsystemextensions.getprojectservice/extension/extension.vb" id="Snippet1":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/spextensibility.projectservice.fromprojectsystemextensions.getprojectservice/extension/extension.cs" id="Snippet1":::

     有关创建项目扩展插件的信息，请参阅[如何：](../sharepoint/how-to-create-a-sharepoint-project-extension.md)创建SharePoint扩展。

#### <a name="to-retrieve-the-service-in-a-project-item-extension"></a>在项目项扩展中检索服务

1. 在 接口的实现 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> 中，找到 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension.Initialize%2A> 方法。

2. 使用 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemType.ProjectService%2A> *projectItemType* 参数的 属性检索服务。

     下面的代码示例演示如何使用 项目服务在列表定义项目项的简单扩展中将消息写入"输出"窗口和"**错误列表**"窗口。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spextensibility.projectservice.fromprojectsystemextensions.getprojectservice/extension/extension.vb" id="Snippet2":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/spextensibility.projectservice.fromprojectsystemextensions.getprojectservice/extension/extension.cs" id="Snippet2":::

     有关创建项目项扩展的详细信息，请参阅[如何：创建SharePoint项目项扩展](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)。

#### <a name="to-retrieve-the-service-in-a-project-item-type-definition"></a>在项目项类型定义中检索服务

1. 在 接口的实现 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> 中，找到 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A> 方法。

2. 使用 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition.ProjectService%2A> *typeDefinition* 参数的 属性检索服务。

     下面的代码示例演示如何使用 项目服务在简单的项目项类型定义中将消息写入"输出"窗口和"错误列表"窗口。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spextensibility.projectservice.fromprojectsystemextensions.getprojectservice/extension/extension.vb" id="Snippet3":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/spextensibility.projectservice.fromprojectsystemextensions.getprojectservice/extension/extension.cs" id="Snippet3":::

     有关定义项目项类型的详细信息，请参阅[如何：定义SharePoint项类型](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)。

## <a name="retrieve-the-service-in-server-explorer-extensions"></a>在扩展中服务器资源管理器服务
 在 SharePoint 连接服务器资源管理器的扩展中，项目服务对象的 属性 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode.ServiceProvider%2A> 访问该 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode> 连接。

#### <a name="to-retrieve-the-service-in-a-server-explorer-extension"></a>在扩展中检索服务器资源管理器

1. 从 <xref:System.IServiceProvider> 扩展中对象的 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode.ServiceProvider%2A> <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode> 属性获取 对象。

2. 使用 <xref:System.IServiceProvider.GetService%2A> 方法请求 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService> 对象。

     下面的代码示例演示如何使用 项目服务 从扩展添加到 服务器资源管理器 中的列表节点的快捷菜单中将消息写入到"输出"**窗口和"错误列表"服务器资源管理器。**

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spextensibility.projectservice.fromspexplorerextensions.getprojectservice/extension/extension.vb" id="Snippet1":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/spextensibility.projectservice.fromspexplorerextensions.getprojectservice/extension/extension.cs" id="Snippet1":::

     有关扩展 SharePoint 中的 SharePoint **连接** 节点 **服务器资源管理器，请参阅** 如何：扩展 SharePoint [中的](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)服务器资源管理器。

## <a name="retrieve-the-service-in-other-visual-studio-extensions"></a>检索其他扩展Visual Studio服务
 可以在 VSPackage 项目服务或有权访问自动化对象模型中的对象的任何 Visual Studio 扩展（如实现 接口的项目模板向导）中检索对象。 <xref:EnvDTE80.DTE2> <xref:Microsoft.VisualStudio.TemplateWizard.IWizard>

 在 VSPackage 中，可以使用以下方法之一请求 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService> 对象：

- 派生自 类的托管 <xref:System.IServiceProvider.GetService%2A> VSPackage 的 <xref:Microsoft.VisualStudio.Shell.Package> 方法。 有关详细信息，请参阅 [如何：获取服务](../extensibility/how-to-get-a-service.md)。

- 静态 <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> 方法。 有关详细信息，请参阅使用 [GetGlobalService](../extensibility/internals/service-essentials.md#how-to-use-getglobalservice)。

  在Visual Studio访问 对象的扩展中，可以使用 对象的 方法 <xref:EnvDTE80.DTE2> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService> <xref:Microsoft.VisualStudio.Shell.ServiceProvider.GetService%2A> 请求 <xref:Microsoft.VisualStudio.Shell.ServiceProvider> 对象。 有关详细信息，请参阅从 [DTE 对象 获取服务](../extensibility/how-to-get-a-service.md#getting-a-service-from-the-dte-object)。

## <a name="see-also"></a>请参阅
- [使用SharePoint 项目服务](../sharepoint/using-the-sharepoint-project-service.md)
- [如何：获取服务](../extensibility/how-to-get-a-service.md)
- [如何：将向导与项目模板一同使用](../extensibility/how-to-use-wizards-with-project-templates.md)

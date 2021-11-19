---
title: 如何：检索 SharePoint 项目服务 | Microsoft Docs
description: 了解如何在项目系统扩展、服务器资源管理器扩展或其他 Visual Studio 扩展中访问 SharePoint 项目服务。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665289"
---
# <a name="how-to-retrieve-the-sharepoint-project-service"></a>如何：检索 SharePoint 项目服务
  可以在以下类型的解决方案中访问 SharePoint 项目服务：

- SharePoint 项目系统的扩展，例如项目扩展、项目项扩展或项目项类型定义。 有关这些类型的扩展的详细信息，请参阅[扩展 SharePoint 项目系统](../sharepoint/extending-the-sharepoint-project-system.md)。

- 服务器资源管理器中的“SharePoint 连接”节点的扩展 。 有关这些类型的扩展的详细信息，请参阅[扩展服务器资源管理器中的“SharePoint 连接”节点](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)。

- 另一种类型的 Visual Studio 扩展，例如 VSPackage。

## <a name="retrieve-the-service-in-project-system-extensions"></a>在项目系统扩展中检索服务
 在 SharePoint 项目系统的任何扩展中，可以使用 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject> 项目的 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject.ProjectService%2A> 属性访问项目服务。

 还可使用以下过程检索项目服务。

#### <a name="to-retrieve-the-service-in-a-project-extension"></a>在项目扩展中检索服务

1. 在 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> 接口的实现中，找到 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension.Initialize%2A> 方法。

2. 使用 projectService 参数访问服务。

     下面的代码示例演示如何使用项目服务将消息写入简单项目扩展中的“输出”窗口和“错误列表”窗口 。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spextensibility.projectservice.fromprojectsystemextensions.getprojectservice/extension/extension.vb" id="Snippet1":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/spextensibility.projectservice.fromprojectsystemextensions.getprojectservice/extension/extension.cs" id="Snippet1":::

     有关创建项目扩展的详细信息，请参阅[如何：创建 SharePoint 项目扩展](../sharepoint/how-to-create-a-sharepoint-project-extension.md)。

#### <a name="to-retrieve-the-service-in-a-project-item-extension"></a>在项目项扩展中检索服务

1. 在 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> 接口的实现中，找到 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension.Initialize%2A> 方法。

2. 使用 projectItemType 参数的 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemType.ProjectService%2A> 属性检索服务。

     下面的代码示例演示如何使用项目服务将消息写入“列表定义”项目项的简单项目扩展中的“输出”窗口和“错误列表”窗口  。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spextensibility.projectservice.fromprojectsystemextensions.getprojectservice/extension/extension.vb" id="Snippet2":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/spextensibility.projectservice.fromprojectsystemextensions.getprojectservice/extension/extension.cs" id="Snippet2":::

     有关创建项目项扩展的详细信息，请参阅[如何：创建 SharePoint 项目项扩展](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)。

#### <a name="to-retrieve-the-service-in-a-project-item-type-definition"></a>在项目项类型定义中检索服务

1. 在 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> 接口的实现中，找到 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A> 方法。

2. 使用 typeDefinition 参数的 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition.ProjectService%2A> 属性检索服务。

     下面的代码示例演示如何使用项目服务将消息写入简单项目项类型定义中的“输出”窗口和“错误列表”窗口 。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spextensibility.projectservice.fromprojectsystemextensions.getprojectservice/extension/extension.vb" id="Snippet3":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/spextensibility.projectservice.fromprojectsystemextensions.getprojectservice/extension/extension.cs" id="Snippet3":::

     有关定义项目项类型的详细信息，请参阅[如何：定义 SharePoint 项目项类型](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)。

## <a name="retrieve-the-service-in-server-explorer-extensions"></a>在服务器资源管理器扩展中检索服务
 在“服务器资源管理器”中的“SharePoint 连接”节点的扩展中，可以使用 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode> 对象的 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode.ServiceProvider%2A> 属性访问项目服务 。

#### <a name="to-retrieve-the-service-in-a-server-explorer-extension"></a>在服务器资源管理器扩展中检索服务

1. 从扩展中 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode> 对象的 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode.ServiceProvider%2A> 属性获取 <xref:System.IServiceProvider> 对象。

2. 使用 <xref:System.IServiceProvider.GetService%2A> 方法请求 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService> 对象。

     下面的代码示例演示如何使用项目服务从扩展添加到服务器资源管理器中的列表节点的快捷菜单中将消息写入“输出”窗口和“错误列表”窗口  。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spextensibility.projectservice.fromspexplorerextensions.getprojectservice/extension/extension.vb" id="Snippet1":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/spextensibility.projectservice.fromspexplorerextensions.getprojectservice/extension/extension.cs" id="Snippet1":::

     有关扩展“服务器资源管理器”中的“SharePoint 连接”节点的详细信息，请参阅[如何：扩展服务器资源管理器中的 SharePoint 节点](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md) 。

## <a name="retrieve-the-service-in-other-visual-studio-extensions"></a>在其他 Visual Studio 扩展中检索服务
 可以在 VSPackage 或任何能够访问自动化对象模型中的 <xref:EnvDTE80.DTE2> 对象的 Visual Studio 扩展（例如实现 <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> 接口的项目模板向导）中检索项目服务。

 在 VSPackage 中，可以使用以下方法之一请求 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService> 对象：

- 派生自 <xref:Microsoft.VisualStudio.Shell.Package> 类的托管 VSPackage 的 <xref:System.IServiceProvider.GetService%2A> 方法。 有关详细信息，请参阅[如何：获取服务](../extensibility/how-to-get-a-service.md)。

- 静态 <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> 方法。 有关详细信息，请参阅[使用 GetGlobalService](../extensibility/internals/service-essentials.md#how-to-use-getglobalservice)。

  在有权访问 <xref:EnvDTE80.DTE2> 对象的 Visual Studio 扩展中，可以使用 <xref:Microsoft.VisualStudio.Shell.ServiceProvider> 对象的 <xref:Microsoft.VisualStudio.Shell.ServiceProvider.GetService%2A> 方法请求 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService> 对象。 有关详细信息，请参阅[从 DTE 对象获取服务](../extensibility/how-to-get-a-service.md#getting-a-service-from-the-dte-object)。

## <a name="see-also"></a>另请参阅
- [使用 SharePoint 项目服务](../sharepoint/using-the-sharepoint-project-service.md)
- [如何：获取服务](../extensibility/how-to-get-a-service.md)
- [如何：使用向导来处理项目模板](../extensibility/how-to-use-wizards-with-project-templates.md)

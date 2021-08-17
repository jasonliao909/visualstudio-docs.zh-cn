---
title: 如何：执行 SharePoint 命令|Microsoft Docs
description: 阅读如何创建自定义 SharePoint 命令，以从 SharePoint 扩展调用服务器对象模型 API。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint commands [SharePoint development in Visual Studio], executing
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: b589569d5675644deae2b7ecb47b1c992d4c76c7
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122093016"
---
# <a name="how-to-execute-a-sharepoint-command"></a>如何：执行SharePoint命令
  如果要在 SharePoint 扩展中使用服务器对象模型，则必须创建自定义 SharePoint *命令* 来调用 API。 定义命令并随 SharePoint 扩展一起部署后，扩展可以执行 命令以调用 SharePoint 对象模型。 若要执行命令，请使用 对象的 ExecuteCommand 方法之 <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection> 一。

 有关命令用途SharePoint，请参阅[调用对象SharePoint模型](../sharepoint/calling-into-the-sharepoint-object-models.md)。

### <a name="to-execute-a-sharepoint-command"></a>执行 SharePoint 命令

1. 在 SharePoint 工具扩展中，获取 <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection> 对象。 获取对象 <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection> 的方式取决于要创建的扩展的类型：

    - 在项目系统的扩展SharePoint，使用 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject.SharePointConnection%2A> 属性。

         有关项目系统扩展详细信息，请参阅[扩展SharePoint系统](../sharepoint/extending-the-sharepoint-project-system.md)。

    - 在 SharePoint **中的 服务器资源管理器** 连接 **节点** 的扩展中，使用 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeContext.SharePointConnection%2A> 属性。 若要获取 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeContext> 对象，请使用 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode.Context%2A> 属性。

         有关 **扩展服务器资源管理器，** 请参阅 扩展 SharePoint 中的 [服务器资源管理器。](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)

    - 在不是工具扩展的一SharePoint（如项目模板向导）的代码中，使用 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService.SharePointConnection%2A> 属性。

         有关检索数据项目服务，请参阅[使用](../sharepoint/using-the-sharepoint-project-service.md)SharePoint 项目服务。

2. 调用 对象的 ExecuteCommand 方法之 <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection> 一。 将要执行的命令的名称传递给 ExecuteCommand 方法的第一个参数。 如果命令具有自定义参数，则向 ExecuteCommand 方法的第二个参数传递该参数。

     每个支持的命令签名都有不同的 ExecuteCommand 重载。 下表列出了支持的签名以及要用于每个签名的重载。

    |命令签名|使用 ExecuteCommand 重载|
    |-----------------------|------------------------------------|
    |该命令只有默认参数 <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext> ，没有返回值。|<xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A>|
    |该命令只有默认参数 <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext> 和返回值。|<xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A>|
    |该命令具有两个参数 (默认参数，自定义参数) <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext> 没有返回值。|<xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A>|
    |该命令有两个参数和一个返回值。|<xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A>|

## <a name="example"></a>示例
 下面的代码示例演示如何使用 重载调用如何：创建命令 中所述SharePoint <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A> `Contoso.Commands.UpgradeSolution` [命令](../sharepoint/how-to-create-a-sharepoint-command.md)。

 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/UpgradeDeploymentStep/deploymentstepextension/upgradestep.cs" id="Snippet6":::
 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/upgradedeploymentstep/deploymentstepextension/upgradestep.vb" id="Snippet6":::

 `Execute`此示例中显示的方法是自定义部署 <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentStep.Execute%2A> 步骤 <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentStep> 中 接口的 方法的实现。 若要在较大示例的上下文中查看此代码，请参阅[演练：为项目创建自定义SharePoint步骤](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)。

 请注意有关方法调用的以下 <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A> 详细信息：

- 第一个参数标识要调用的命令。 此字符串与传递给命令定义 <xref:Microsoft.VisualStudio.SharePoint.Commands.SharePointCommandAttribute> 上的 的值匹配。

- 第二个参数是你想要传递给命令的自定义第二个参数的值。 在这种情况下，它是要升级到 SharePoint 站点中的 *.wsp* 文件的完整路径。

- 代码不会将隐式 <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext> 参数传递给 命令。 当你从项目 SharePoint系统的扩展或 服务器资源管理器 中的 SharePoint 连接节点的扩展调用 命令时，**此** 参数会自动 **传递到 服务器资源管理器。** 在其他类型的解决方案中（例如，在实现 接口的项目模板向导中）中， <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> 此参数为 **null。**

## <a name="compile-the-code"></a>编译代码
 此示例需要引用 Microsoft.VisualStudio。SharePoint程序集。

## <a name="see-also"></a>请参阅
- [调用对象SharePoint模型](../sharepoint/calling-into-the-sharepoint-object-models.md)
- [如何：创建SharePoint命令](../sharepoint/how-to-create-a-sharepoint-command.md)
- [演练：扩展服务器资源管理器以显示 Web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)

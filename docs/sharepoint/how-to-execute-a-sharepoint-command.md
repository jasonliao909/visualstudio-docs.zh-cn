---
title: 操作说明：执行 SharePoint 命令 | Microsoft Docs
description: 阅读如何创建自定义 SharePoint 命令，以从 SharePoint 工具扩展调用服务器对象模型 API。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126666182"
---
# <a name="how-to-execute-a-sharepoint-command"></a>操作说明：执行 SharePoint 命令
  如果要在 SharePoint 工具扩展中使用服务器对象模型，必须创建自定义 SharePoint 命令来调用 API。 在你定义命令并将它部署到你的 SharePoint 工具扩展后，你的扩展可以执行此命令来调入 SharePoint 服务器对象模型。 若要执行命令，请使用 <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection> 对象的 ExecuteCommand 方法之一。

 有关 SharePoint 命令用途的详细信息，请参阅[调入 SharePoint 对象模型](../sharepoint/calling-into-the-sharepoint-object-models.md)。

### <a name="to-execute-a-sharepoint-command"></a>执行 SharePoint 命令

1. 在你的 SharePoint 工具扩展中，获取 <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection> 对象。 获取 <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection> 对象的方式取决于要创建的扩展类型：

    - 在 SharePoint 项目系统的扩展中，使用 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject.SharePointConnection%2A> 属性。

         有关项目系统扩展的详细信息，请参阅[扩展 SharePoint 项目系统](../sharepoint/extending-the-sharepoint-project-system.md)。

    - 在“服务器资源管理器”中的“SharePoint 连接”节点的扩展中，使用 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeContext.SharePointConnection%2A> 属性 。 若要获取 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeContext> 对象，请使用 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode.Context%2A> 属性。

         有关“服务器资源管理器”扩展的详细信息，请参阅[扩展服务器资源管理器中的 SharePoint 连接节点](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)。

    - 在不属于 SharePoint 工具扩展部分的代码中，例如项目模板向导，使用 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService.SharePointConnection%2A> 属性。

         有关检索项目服务的详细信息，请参阅[使用 SharePoint 项目服务](../sharepoint/using-the-sharepoint-project-service.md)。

2. 调用 <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection> 对象的 ExecuteCommand 方法之一。 将要执行的命令的名称传递给 ExecuteCommand 方法的第一个参数。 如果你的命令具有自定义参数，请将该自定义参数传递给 ExecuteCommand 方法的第二个参数。

     每个支持的命令签名都有不同的 ExecuteCommand 重载。 下表列出了支持的签名以及要用于每个签名的重载。

    |命令签名|要使用的 ExecuteCommand 重载|
    |-----------------------|------------------------------------|
    |命令只有默认的 <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext> 参数，没有返回值。|<xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A>|
    |命令只有默认的 <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext> 参数和一个返回值。|<xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A>|
    |命令有两个参数（默认的 <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext> 参数和一个自定义参数），没有返回值。|<xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A>|
    |命令有两个参数和一个返回值。|<xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A>|

## <a name="example"></a>示例
 下面的代码示例展示了如何使用 <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A> 重载来调用[操作说明：创建 SharePoint 命令](../sharepoint/how-to-create-a-sharepoint-command.md)中所述的 `Contoso.Commands.UpgradeSolution` 命令。

 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/UpgradeDeploymentStep/deploymentstepextension/upgradestep.cs" id="Snippet6":::
 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/upgradedeploymentstep/deploymentstepextension/upgradestep.vb" id="Snippet6":::

 此示例中显示的 `Execute` 方法是自定义部署步骤中 <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentStep> 接口的 <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentStep.Execute%2A> 方法的实现。 若要在更大的上下文示例中查看此代码，请参阅[演练：为 SharePoint 项目创建自定义部署步骤](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)。

 请注意有关调用 <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A> 方法的以下详细信息：

- 第一个参数标识要调用的命令。 此字符串与传递给命令定义上的 <xref:Microsoft.VisualStudio.SharePoint.Commands.SharePointCommandAttribute> 的值相匹配。

- 第二个参数是要传递给命令的第二个自定义参数的值。 在这种情况下，它是要升级到 SharePoint 站点的 .wsp 文件的完整路径。

- 代码不会将隐式 <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext> 参数传递给命令。 在你从 SharePoint 项目系统的扩展或“服务器资源管理器”中的“SharePoint 连接”节点的扩展调用命令时，此参数会自动传递到命令中 。 在其他类型的解决方案中，例如在实现 <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> 接口的项目模板向导中，此参数为 null。

## <a name="compile-the-code"></a>编译代码
 此示例需要引用 Microsoft.VisualStudio.SharePoint 程序集。

## <a name="see-also"></a>另请参阅
- [调入 SharePoint 对象模型](../sharepoint/calling-into-the-sharepoint-object-models.md)
- [操作说明：创建 SharePoint 命令](../sharepoint/how-to-create-a-sharepoint-command.md)
- [演练：扩展服务器资源管理器以显示 Web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)

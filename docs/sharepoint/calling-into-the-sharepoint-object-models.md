---
title: 调用 SharePoint 对象模型 | Microsoft Docs
description: 了解如何调用两个不同的对象模型，这些模型可用于 SharePoint 工具扩展。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, client object model
- SharePoint development in Visual Studio, server object model
- SharePoint commands [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, extensibility features
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 0cdcee9a763a7354ceca6821796f455a1a878aa3
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664241"
---
# <a name="call-into-the-sharepoint-object-models"></a>调用 SharePoint 对象模型
  在 Visual Studio 中创建 SharePoint 工具扩展时，可能需要调用 SharePoint API 来执行某些任务。 例如，如果为 SharePoint 项目创建自定义部署步骤，可能需要调用 SharePoint API 来执行某些任务以部署解决方案。

 [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] 和 [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] 提供了两个不同的对象模型，可用于 SharePoint 工具扩展：服务器对象模型和客户端对象模型。 每个对象模型在 SharePoint 工具扩展的上下文中都有优缺点。

 有关 SharePoint 对象模型的概述，请参阅 [SharePoint 工具扩展的编程模型概述](../sharepoint/overview-of-the-programming-model-of-sharepoint-tools-extensions.md)。

## <a name="use-the-client-object-model-in-extension-projects"></a>在扩展项目中使用客户端对象模型
 开发 SharePoint 工具扩展时，可以在项目中使用客户端对象模型，就像任何其他托管 API 集一样。 可以将对客户端对象模型中的程序集的引用添加到项目，并且可以直接从代码调用客户端对象模型中的 API。

 但是，客户端对象模型在 SharePoint 工具扩展的上下文中有两个缺点：

- 客户端对象模型仅提供服务器对象模型的子集。 如果必须使用客户端对象模型中未公开的 SharePoint 功能，则必须使用服务器对象模型。

- 尽管在 SharePoint 工具扩展中使用客户端对象模型在大多数情况下应是可行的，但你可能会遇到一些场景，其中对客户端对象模型的调用不会按预期工作。 客户端对象模型旨在在客户端应用程序中用于调用远程服务器或场上的 SharePoint 网站。 Visual Studio 中的 SharePoint 工具只能与开发计算机上的本地 SharePoint 安装一起工作。 因此，在 SharePoint 工具扩展中使用客户端对象模型时，将调用本地计算机上的 SharePoint 网站，这不是客户端对象模型的设计初衷。

  有关演示如何在 Visual Studio 中的 SharePoint 工具扩展中使用客户端对象模型的演练，请参阅[演练：在服务器资源管理器扩展中调用 SharePoint 客户端对象模型](../sharepoint/walkthrough-calling-into-the-sharepoint-client-object-model-in-a-server-explorer-extension.md)。

## <a name="use-the-server-object-model-in-extension-projects"></a>在扩展项目中使用服务器对象模型
 服务器对象模型是客户端对象模型的超集。 使用服务器对象模型，可以使用 [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] 和 [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] 以编程方式公开的所有功能。

 SharePoint 工具扩展可以使用服务器对象模型中的 API，但不能直接调用 API。 只能从面向 .NET Framework 3.5 的 64 位进程调用服务器对象模型。 但是，SharePoint 工具扩展需要 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]，并且它们在 32 位 Visual Studio 进程中运行。 这可以防止 SharePoint 扩展直接引用 SharePoint 对象模型中的程序集。

 如果要在 SharePoint 工具扩展中使用服务器对象模型，必须创建自定义 SharePoint 命令来调用 API。 在可直接调用服务器对象模型的辅助程序集中定义 SharePoint 命令。 在扩展项目中，通过使用 <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection> 对象的 ExecuteCommand 方法间接调用 SharePoint 命令。

 有关创建和使用 SharePoint 命令的详细信息，请参阅[如何：创建 SharePoint 命令](../sharepoint/how-to-create-a-sharepoint-command.md)和[如何：执行 SharePoint 命令](../sharepoint/how-to-execute-a-sharepoint-command.md)。 若要了解如何部署 SharePoint 命令，请参阅[在 Visual Studio 中部署 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

 有关演示如何创建和使用 SharePoint 命令的演练，请参阅[演练：为 SharePoint 项目创建自定义部署步骤](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)和[演练：扩展服务器资源管理器以显示 Web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)。

### <a name="understand-how-sharepoint-commands-are-executed"></a>了解如何执行 SharePoint 命令
 定义 SharePoint 命令的程序集将加载到名为vssphost4.exe 的 64 位主机进程中。 在 SharePoint 工具扩展中调用 SharePoint 命令后，该命令将由 vssphost4.exe 执行，而不是由 32 位 Visual Studio进程 (devenv.exe) 执行。 可以通过在注册表中设置值来控制 SharePoint 命令执行的某些方面。 有关详细信息，请参阅[在 Visual Studio 中调试 SharePoint 工具扩展](../sharepoint/debugging-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>另请参阅
- [操作说明：创建 SharePoint 命令](../sharepoint/how-to-create-a-sharepoint-command.md)
- [操作说明：执行 SharePoint 命令](../sharepoint/how-to-execute-a-sharepoint-command.md)
- [SharePoint 工具扩展的编程模型概述](../sharepoint/overview-of-the-programming-model-of-sharepoint-tools-extensions.md)

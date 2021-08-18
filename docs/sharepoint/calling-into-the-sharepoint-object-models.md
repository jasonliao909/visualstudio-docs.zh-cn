---
title: 调用对象SharePoint模型|Microsoft Docs
description: 了解如何调用两个不同的对象模型，这些模型可用于SharePoint扩展。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122100447"
---
# <a name="call-into-the-sharepoint-object-models"></a>调用对象SharePoint模型
  在 Visual Studio 中为 SharePoint 工具创建扩展时，SharePoint调用 SharePoint API 来执行某些任务。 例如，如果为项目创建SharePoint部署步骤，可能需要调用 SharePoint API 来执行某些任务来部署解决方案。

 [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)]和 [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] 提供了两个不同的对象模型，可用于SharePoint扩展：服务器对象模型和客户端对象模型。 每个对象模型在工具扩展的上下文中都有SharePoint缺点。

 有关对象模型的SharePoint，请参阅工具扩展的[编程SharePoint概述](../sharepoint/overview-of-the-programming-model-of-sharepoint-tools-extensions.md)。

## <a name="use-the-client-object-model-in-extension-projects"></a>在扩展项目中使用客户端对象模型
 在开发适用于 SharePoint 工具的扩展时，可以在项目中使用客户端对象模型，就像使用任何其他一组托管 API 一样。 可以将对客户端对象模型中的程序集的引用添加到项目，并且可以直接从代码调用客户端对象模型中的 API。

 但是，客户端对象模型在工具扩展的上下文中SharePoint缺点：

- 客户端对象模型仅提供服务器对象模型的子集。 如果必须使用客户端SharePoint模型中未公开的功能，则必须使用服务器对象模型。

- 尽管在大多数情况下，在 SharePoint中使用客户端对象模型，但在某些情况下，对客户端对象模型的调用可能无法如预期工作。 客户端对象模型旨在用于客户端应用程序中，以调用SharePoint或场上的站点。 SharePoint中的 Visual Studio 工具仅适用于开发SharePoint本地安装。 因此，在 SharePoint 工具扩展中使用客户端对象模型时，将调用本地计算机上 SharePoint 站点，而不是客户端对象模型的设计使用方式。

  有关演示如何在 Visual Studio 中 SharePoint 工具的扩展中使用客户端对象模型的演练，请参阅演练：调用 服务器资源管理器 扩展中的 SharePoint 客户端[对象模型](../sharepoint/walkthrough-calling-into-the-sharepoint-client-object-model-in-a-server-explorer-extension.md)。

## <a name="use-the-server-object-model-in-extension-projects"></a>在扩展项目中使用服务器对象模型
 服务器对象模型是客户端对象模型的超集。 使用服务器对象模型时，可以使用 和 以编程方式 [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] 公开的所有功能。

 SharePoint工具扩展可以使用服务器对象模型中的 API，但不能直接调用 API。 服务器对象模型只能从面向 3.5 的 64 位.NET Framework调用。 但是，SharePoint扩展需要 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ，并且它们在 32 位扩展进程中Visual Studio运行。 这可以防止SharePoint扩展直接引用 SharePoint 对象模型中的程序集。

 如果要在 SharePoint 扩展中使用服务器对象模型，则必须创建自定义 SharePoint *命令* 来调用 API。 可以在可SharePoint服务器对象模型的辅助程序集中定义命令。 在扩展项目中，通过使用 对象的 ExecuteCommand SharePoint间接调用命令 <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection> 。

 有关创建和使用命令SharePoint，请参阅[如何：](../sharepoint/how-to-create-a-sharepoint-command.md)创建 SharePoint 命令和[如何：](../sharepoint/how-to-execute-a-sharepoint-command.md)执行 SharePoint 命令。 若要了解如何部署 SharePoint 命令，请参阅在 Visual Studio 中为 SharePoint[工具部署Visual Studio。](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)

 有关演示如何创建和使用 SharePoint 命令的演练，请参阅演练：为 SharePoint 项目创建自定义部署步骤和[演练：](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)扩展[服务器资源管理器](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)以显示 Web 部件。

### <a name="understand-how-sharepoint-commands-are-executed"></a>了解如何SharePoint命令
 定义这些SharePoint的程序集将加载到名为vssphost4.exe的 64 *位主机进程中*。 在 SharePoint 工具扩展中调用 SharePoint 命令后，该命令由 *vssphost4.exe* 而不是 32 位 Visual Studio 进程 *(devenv.exe) 。* 可以通过在注册表中设置SharePoint控制命令的执行方式的某些方面。 有关详细信息，请参阅 Visual Studio 中 SharePoint[工具的调试Visual Studio。](../sharepoint/debugging-extensions-for-the-sharepoint-tools-in-visual-studio.md)

## <a name="see-also"></a>请参阅
- [如何：创建 SharePoint 命令](../sharepoint/how-to-create-a-sharepoint-command.md)
- [如何：执行SharePoint命令](../sharepoint/how-to-execute-a-sharepoint-command.md)
- [SharePoint 工具扩展的编程模型概述](../sharepoint/overview-of-the-programming-model-of-sharepoint-tools-extensions.md)

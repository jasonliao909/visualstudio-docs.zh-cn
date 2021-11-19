---
title: 沙盒解决方案注意事项|Microsoft Docs
description: 浏览沙盒解决方案，这是 Microsoft SharePoint中的一项功能，可让网站集用户上传自己的自定义代码解决方案。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.Project.SandboxedSolutions
- VS.SharePointTools.Security.SandboxedSolutions
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, sandboxed solutions
- sandboxed solutions [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, farm solutions
- farm solutions [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 156ebc7fa17d53fd56cb8b069698f0bdf4b9a43c
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602533"
---
# <a name="sandboxed-solution-considerations"></a>沙盒解决方案注意事项
  *沙盒解决方案* 是 Microsoft SharePoint 2010 中的一项功能，可让网站集用户上传自己的自定义代码解决方案。 常见的沙盒解决方案是用户上传自己的Web 部件。

 沙盒SharePoint应用程序在有权访问 Web 场有限部分的安全监视进程中运行。 Microsoft SharePoint 2010 结合使用功能、解决方案库、解决方案监视和验证框架来启用沙盒解决方案。

## <a name="specify-project-trust-level"></a>指定项目信任级别
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 通过名为"沙盒解决方案"的布尔项目属性支持 *沙盒解决方案*。 此属性可以在项目中随时设置，也可在自定义向导 SharePoint **项目时指定**。

> [!NOTE]
> 创建 *项目的沙盒* 解决方案属性后，更改该属性可能会导致验证错误。

 如果将"沙盒解决方案"属性设置为 **false，** 或者选择"部署为场解决方案"选项，则解决方案被视为场 **范围** 解决方案。 但是，如果将"沙盒解决方案"属性设置为 **true，** 或者你在向导中选择"部署为沙盒解决方案"选项，则解决方案处理方式不同于场解决方案。

## <a name="sharepoint-site-hierarchy"></a>SharePoint站点层次结构
 若要了解沙盒解决方案如何工作，可帮助了解SharePoint站点在范围内是分层的。 顶部元素称为 Web 场，其他元素从属于它：

 Web 场

 Web 应用程序 A

 网站集 A1

 站点 A1a

 Web 应用程序 B

 网站集 B1

 站点 B1a

 站点 B1b

 网站集 B2

 站点 B2a

 如你所见，Web 场可以包含一个或多个 Web 应用程序，而 Web 应用程序又可以包含一个或多个网站集，这些网站集可以具有子网站，等等。 对一个网站集所做的更改仅影响该网站集，而不会影响其他网站集。 但是，在 Web 场级别所做的更改会影响场上的所有网站集。

 Windows SharePoint Services (WSS) 3.0 仅允许将解决方案部署到场级别，但允许你部署到场级别 (场解决方案) 或站点集级别 (沙盒解决方案 [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)]) 。

## <a name="why-sandboxed-solutions"></a>为何使用沙盒解决方案？
 在 WSS 3.0 中，解决方案只能部署到场级别。 这意味着可以部署可能有害的或不稳定的解决方案，从而影响整个 Web 场及其下运行的所有其他网站集和应用程序。 但是，通过使用沙盒解决方案，可以将解决方案部署到场的子区域（特定网站集）。 为了提供额外的保护，解决方案的程序集不会加载到主进程中 [!INCLUDE[TLA2#tla_iis5](../sharepoint/includes/tla2sharptla-iis5-md.md)] *(w3wp.exe) 。* 相反，它会加载到单独的进程中 *(SPUCWorkerProcess.exe) 。* 此过程受到监视并实施配额和限制，以保护场免受执行有害活动的沙盒解决方案的影响，例如运行占用 CPU 周期的严格循环。

## <a name="site-collection-solution-gallery"></a>网站集解决方案库
 [!INCLUDE[sharepointShort](../sharepoint/includes/sharepointshort-md.md)] 2010 包含一项名为“网站集解决方案库”的功能。 可以从 SharePoint 2010 管理中心页或打开"站点操作"菜单，选择"站点 **设置"，** 然后选择 SharePoint 站点中的"库"下的"解决方案"链接来访问此功能。 解决方案库是解决方案存储库，可让网站集管理员管理其网站集中的解决方案。

 解决方案库是一个文档库，存储在 SharePoint 根 Web 中。 解决方案库取代了站点模板并支持解决方案包。 上传 SharePoint (*.wsp*) 解决方案包时，它会作为沙盒解决方案进行处理。

## <a name="sandboxed-solution-limitations"></a>沙盒解决方案限制
 部署沙盒解决方案时，SharePoint可用的各种安全功能，以帮助减少它可能具有的任何安全漏洞。 其中一些限制包括：

- 沙盒解决方案有一部分有限的可部署解决方案元素可供使用。 站点SharePoint工作流等项目模板可能易受攻击。

- SharePoint在独立于 *(SPUCWorkerProcess.exe)* 应用程序池的进程中运行沙盒 [!INCLUDE[TLA2#tla_iis5](../sharepoint/includes/tla2sharptla-iis5-md.md)] (w3wp.exe) 代码。 

- 无法将映射的文件夹添加到项目中。

- 程序集 [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] Microsoft.Office。服务器不能在沙盒解决方案中使用。 此外，只有 [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] 程序集 Microsoft.SharePoint中的类型才能在沙盒解决方案中使用。

  必须注意的是，将 SharePoint 解决方案指定为沙盒解决方案不会影响SharePoint服务器;它仅确定如何将SharePoint项目部署到SharePoint [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 以及它绑定到的程序集。 它不会影响生成的 *.wsp* 文件， *并且 .wsp* 文件没有与 *沙* 盒解决方案属性直接相关的数据。

## <a name="capabilities-and-elements-in-sandboxed-solutions"></a>沙盒解决方案中的功能和元素
 沙盒解决方案支持以下功能和元素：

- 内容类型/字段

- 自定义操作

- 声明性工作流

- 事件接收器

- 功能标注

- 列出定义

- 列出实例

- 模块/文件

- 导航

- *Onet.xml*

- SPItemEventReceiver

- SPListEventReceiver

- SPWebEventReceiver

- 支持派生Web 部件的所有类型`System.Web.UI.WebControls.WebParts.WebPart`

- Web 部件

- WebTemplate 功能元素 (而不是 *Webtemp.xml)*

- 视觉对象Web 部件

  沙盒解决方案不支持以下功能和元素：

- 应用程序页

- 自定义操作组

- 场范围功能

- `HideCustomAction` 元素

- Web 应用程序范围的功能

- 包含代码的工作流

## <a name="see-also"></a>另请参阅
- [沙盒解决方案和场解决方案之间的差异](../sharepoint/differences-between-sandboxed-and-farm-solutions.md)
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)

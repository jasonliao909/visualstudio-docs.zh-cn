---
title: 创建 SharePoint 网站定义 | Microsoft Docs
description: 创建 SharePoint 网站定义。 网站定义决定了 SharePoint 网站的外观和行为，还决定了其默认内容和功能。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: overview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, site definitions
- site definitions [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 3fca56cc3f0dbe8ed44adfce81cf7a8f5dae2fc4852c49f305473f20f4e9c747
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121425591"
---
# <a name="create-site-definitions-for-sharepoint"></a>创建 SharePoint 网站定义
  通过 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中的 SharePoint 站点定义项目，可创建一个网站定义，是新 SharePoint 网站的基础。 这些定义不仅决定了 SharePoint 网站的外观和行为，还决定了其默认内容和功能。 在定义中，您可以放入预配置的列表、内容类型、事件接收器、图像以及其他项。 例如 SharePoint 包含某些网站定义（如 BLOG）。 根据 BLOG 网站定义创建网站时，该网站包含列表、Web 部件和博客网站所需的其他项。

 有关网站定义的详细信息，请参阅[网站模板和定义](/previous-versions/office/developer/sharepoint-2010/ms434313(v=office.14))。

## <a name="site-definition-projects"></a>网站定义项目
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中的网站定义项目仅提供 SharePoint 网站所需的基本文件，不提供任何默认功能。 必须添加文件和内容才能提供所需的功能。 可通过创建和添加所需的文件，手动生成网站。

## <a name="feature-stapling"></a>功能装订
 在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中创建网站定义的一个优点是，它们会自动使用“功能装订”。 “功能装订”将功能附加到网站定义，而不是将其功能嵌入到网站定义本身。 这样便可将功能添加到使用网站定义创建的任何网站，而无需修改原始网站定义。 有关详细信息，请参阅[功能装订](/previous-versions/office/developer/sharepoint-2007/bb861862(v=office.12))。

## <a name="site-definition-project-components"></a>网站定义项目组件
 创建网站定义解决方案时，系统会将以下默认文件会添加到其 SiteDefinition 节点。

|文件名|说明|
|---------------|-----------------|
|default.aspx|新 SharePoint 网站的默认 ASPX 主页。|
|onet.xml|指定新网站的配置、网站定义模板的组件和默认行为。 这些设置可以包含属性，如已启用的内容类型、默认列表视图、文档模板文件以及网站中包含的 Web 部件。 默认情况下，`Modules` 部分列出了要添加到 SharePoint 网站的文件以及它们的配置方式。|
|*webtemp_\<SiteDefinitionName>.xml*|指定在“新 SharePoint 网站”页的“模板选择”部分中显示的网站定义配置 。|

 默认情况下，所有网站定义都存储在 \<drive:>\Program Files\Common Files\Microsoft Shared\Web Server Extensions\14\TEMPLATE\SiteTemplates 文件夹中。 每个网站定义都有自己的子文件夹。

## <a name="related-topics"></a>相关主题

|Title|说明|
|-----------|-----------------|
|[演练：创建基本网站定义项目](../sharepoint/walkthrough-create-a-basic-site-definition-project.md)|引导你在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中逐步创建基本网站定义项目。|
|[如何：创建自定义网站定义和配置](/previous-versions/office/developer/sharepoint-2010/ms454677(v=office.14))|介绍如何通过复制现有网站定义并修改该副本，在 SharePoint 中创建自定义网站定义。|
|[*WebTemp.xml*](/previous-versions/office/developer/sharepoint-2010/ms447717(v=office.14))|介绍原始文件，用于指定在“新 SharePoint 网站”页的“模板选择”部分中提供的网站定义 。|
|[本地化 SharePoint 解决方案](../sharepoint/localizing-sharepoint-solutions.md)|介绍如何准备供全局使用的 SharePoint 解决方案。|
|[为 SharePoint 创建 Web 部件](../sharepoint/creating-web-parts-for-sharepoint.md)|介绍如何创建用户可修改的 SharePoint 页的部件。|
|[为 Web 部件或应用程序页创建可重用控件](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)|介绍如何创建在应用程序页和 Web 部件中运行的可重用控件。|
|[Visual Web Developer](/previous-versions/visualstudio/visual-studio-2010/ms178093(v=vs.100))|介绍如何使用在项目中打开网页时显示的设计器。|
|[ASP.NET 网页概述](/previous-versions/aspnet/428509ah(v=vs.100))|简要介绍 [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] 网页结构、[!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] 如何处理页面以及 [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] 页面如何显示符合 XHTML 标准的标记。|
|[ASP.NET 网页语法](/previous-versions/aspnet/k33801s3(v=vs.100))|描述构成 ASP.NET 页面的标记元素。|
|[ASP.NET 网页编程](/previous-versions/aspnet/0yt4zca8(v=vs.100))|介绍如何在 [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] 页面中创建事件处理程序以及如何使用客户端脚本。|
|[在 Windows SharePoint Services 中编程](/previous-versions/office/developer/sharepoint-services/ms430674(v=office.12))|介绍如何使用 [!INCLUDE[sharepointShort](../sharepoint/includes/sharepointshort-md.md)] 中提供的托管对象模型。|

## <a name="see-also"></a>另请参阅
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)

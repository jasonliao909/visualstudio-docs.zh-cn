---
title: 为应用程序创建应用程序SharePoint |Microsoft Docs
description: 创建应用程序页SharePoint。 应用程序页是一 ASP.NET 网页，旨在用于SharePoint网站。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, Web pages
- SharePoint development in Visual Studio, content pages
- SharePoint development in Visual Studio, application pages
- application pages [SharePoint development in Visual Studio], developing
- application pages [SharePoint development in Visual Studio], creating
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 035c3b952fd16dd8aa4adf3ffb95542fe39464ff
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122149515"
---
# <a name="create-application-pages-for-sharepoint"></a>为 SharePoint 创建应用程序页
  *应用程序页* 是一 ASP.NET 网页，旨在用于SharePoint网站。 应用程序页是专用类型的 ASP.NET 页。 应用程序页和标准页面之间的主要 ASP.NET 在于，应用程序页包含与主页SharePoint的内容。 母版页使应用程序页能够与站点上的其他页面共享相同的外观和行为。

 Visual Studio设计器设计应用程序页。 设计器为母版页中定义的每个内容占位符显示一个内容区域。 可以通过将控件拖动到这些内容区域来设计应用程序页。

## <a name="application-pages"></a>应用程序页
 应用程序页在服务器上的所有站点之间共享，而站点页特定于一个站点。 有关详细信息，请参阅[SharePoint类型。](/previous-versions/office/developer/sharepoint-2010/aa979592(v=office.14))

 默认情况下，创建站点站点时显示SharePoint是网站页。 可以将站点页添加到SharePoint库。 用户可以使用设计器等工具自定义SharePoint页。 站点页还可以托管动态部件和 web 部件Web 部件等功能。

 应用程序页无法执行这些操作。 但是，如果希望页面包含自定义代码，则应用程序页是要创建的最佳页面类型。 尽管可以将自定义代码添加到站点页，但当用户使用设计器等工具自定义页面时，代码SharePoint运行。

> [!NOTE]
> Visual Studio未提供模板来帮助你为 web 站点创建SharePoint页面。 有关详细信息，请参阅页[SharePoint类型](/previous-versions/office/developer/sharepoint-2010/aa979592(v=office.14))。

## <a name="create-an-application-page"></a>创建应用程序页
 若要创建应用程序页，将应用程序 **页** 项添加到SharePoint项目。 创建应用程序页时，Visual Studio将以下文件夹添加到项目：

|文件夹|说明|
|------------|-----------------|
|布局|地图_layouts文件系统的SharePoint虚拟目录。|
|布局子文件夹|包含应用程序页中的文件。 默认情况下，此文件夹与项目同名。 你随时都可以重命名此文件夹。 运行项目时，Visual Studio文件夹部署到 _layouts 文件系统的 SharePoint 目录。|

 Visual Studio将以下文件添加到项目：

|文件|说明|
|----------|-----------------|
|ASP.NET *.aspx (页)*|包含定义页面的 XML 标记。|
|应用程序页代码文件|包含应用程序页后面的代码。 将处理事件的代码添加到此文件。|
|应用程序页设计器代码文件|包含设计器生成的代码。 不要直接编辑此文件。|

## <a name="design-and-debug-an-application-page"></a>设计和调试应用程序页
 使用应用程序中的设计器视图设计应用程序页Visual Studio。 通过双击或打开其快捷菜单，然后选择"打开) "，然后选择编辑器底部的"设计"按钮，在项目 (中打开应用程序页时，将显示此设计器。 

> [!NOTE]
> 只能在设计器的"源 **"视图中** 设计页面。 **为** 应用程序页禁用设计器的"设计"视图。

 可以像调试应用程序中的其他项目项一样SharePoint应用程序Visual Studio。 当你启动 Visual Studio 调试器时，Visual Studio 将打开 SharePoint 网站。

 若要查看应用程序页，必须手动导航到应用程序页的位置 (例如：http://<em>Server_Name</em>/_layouts/*Project_Name*/ApplicationPage1.aspx) 。

 有关如何调试 SharePoint 项目的详细信息，请参阅 [SharePoint 解决方案疑难解答](../sharepoint/troubleshooting-sharepoint-solutions.md)。

## <a name="choose-a-master-page"></a>选择母版页
 默认情况下， **应用程序页** 项引用你正在调试项目的站点的母版页。 该页名为 v4.master，可在该站点的母版页库中SharePoint列出。

 可以通过设置应用程序元素的 属性来显式更改应用程序页 `MasterPageFile` 使用的母版 `Page` 页。  (例如 `MasterPageFile="~/_layouts/applicationv4.master"` ：) 。 事实上，如果未在服务器服务器上启用动态母版页，则必须SharePoint此属性。 有关中母版页SharePoint，请参阅[母版页](/previous-versions/office/developer/sharepoint-2010/ms443795(v=office.14))。

## <a name="see-also"></a>请参阅
- [SharePoint深度基础开发](/previous-versions/office/developer/sharepoint-2010/ee539092(v=office.14))
- [ASP.NET 概述](/aspnet/overview)
- [ASP.NET 网页](/aspnet/web-pages/index)

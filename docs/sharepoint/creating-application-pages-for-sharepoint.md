---
title: 为 SharePoint 创建应用程序页 |Microsoft Docs
description: 为 SharePoint 创建应用程序页。 应用程序页是设计为在 SharePoint 网站中使用的 ASP.NET 网页。
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
ms.openlocfilehash: 6c74a575df0b13136faf25861c7f7011c154d41fc42ddb5569bc11b0e72d626a
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121332373"
---
# <a name="create-application-pages-for-sharepoint"></a>为 SharePoint 创建应用程序页
  *应用程序页* 是设计为在 SharePoint 网站中使用的 ASP.NET 网页。 应用程序页是 ASP.NET 页的专用类型。 应用程序页和标准 ASP.NET 页之间的主要区别在于，应用程序页包含与 SharePoint 母版页合并的内容。 母版页使应用程序页面与站点上的其他页面共享相同的外观和行为。

 Visual Studio 使你能够使用设计器来设计应用程序页。 设计器显示在母版页中定义的每个内容占位符的内容区域。 您可以通过将控件拖到这些内容区域来设计应用程序页。

## <a name="application-pages"></a>应用程序页
 应用程序页在服务器上的所有站点之间共享，而站点页面则特定于一个站点。 有关详细信息，请[SharePoint 页类型](/previous-versions/office/developer/sharepoint-2010/aa979592(v=office.14))。

 默认情况下，创建 SharePoint 站点时显示的大多数页面都是网站页面。 可以将网站页面添加到 SharePoint 的页面库。 用户可以使用工具（如 SharePoint 设计器）来自定义网站页面。 网站页面还可以托管功能，如动态 Web 部件和 Web 部件区域。

 应用程序页不能执行这些操作。 但是，如果您希望页面包含自定义代码，则可以创建一个应用程序页。 虽然您可以将自定义代码添加到站点页，但当用户通过使用 SharePoint 设计器之类的工具自定义该页时，代码将停止运行。

> [!NOTE]
> Visual Studio 不提供可帮助你为 SharePoint 网站创建网站页面的模板。 有关详细信息，请参阅[SharePoint 页类型](/previous-versions/office/developer/sharepoint-2010/aa979592(v=office.14))。

## <a name="create-an-application-page"></a>"创建应用程序" 页
 若要创建应用程序页，请将 "**应用程序页**" 项添加到 SharePoint 项目。 当你创建应用程序页时，Visual Studio 会将以下文件夹添加到你的项目：

|文件夹|说明|
|------------|-----------------|
|布局|地图到 SharePoint 文件系统的 _layouts 虚拟目录。|
|布局子文件夹|包含构成应用程序页面的文件。 默认情况下，此文件夹具有与项目相同的名称。 你可以随时重命名此文件夹。 运行项目时，Visual Studio 将此文件夹部署到 SharePoint 文件系统的 _layouts 虚拟目录。|

 Visual Studio 将以下文件添加到项目中：

|文件|说明|
|----------|-----------------|
|ASP.NET 页面文件 (*.aspx*) |包含用于定义该页的 XML 标记。|
|应用程序页代码文件|包含应用程序页后的代码。 将处理事件的代码添加到此文件。|
|应用程序页设计器代码文件|包含由设计器生成的代码。 不要直接编辑此文件。|

## <a name="design-and-debug-an-application-page"></a>设计和调试应用程序页
 使用 Visual Studio 中的设计器视图设计应用程序页的内容。 当您在项目中打开应用程序页面时，将显示此设计器 (方法是双击它，或打开其快捷菜单，然后选择 " **打开**) 然后选择编辑器底部的" **设计** "按钮。

> [!NOTE]
> 您只能在设计器的 " **源** " 视图中设计此页。 对于应用程序页，禁用设计器的 **设计** 视图。

 您可以像调试 Visual Studio 中的其他 SharePoint 项目项一样调试应用程序页。 当你启动 Visual Studio 调试器时，Visual Studio 将打开 SharePoint 网站。

 若要查看应用程序页，必须手动导航到应用程序页的位置 (例如： http://<em>Server_Name</em>/_layouts/*Project_Name*/ApplicationPage1.aspx) 。

 有关如何调试 SharePoint 项目的详细信息，请参阅 [SharePoint 解决方案疑难解答](../sharepoint/troubleshooting-sharepoint-solutions.md)。

## <a name="choose-a-master-page"></a>选择母版页
 默认情况下， **应用程序页** 项引用用于调试项目的站点的母版页。 该页命名为 "v4"，您可以在 SharePoint 网站的 **母版页库** 中找到它。

 通过设置应用程序元素的属性，可以显式更改应用程序页所使用的母版页 `MasterPageFile` `Page` 。  (例如： `MasterPageFile="~/_layouts/applicationv4.master"`) 。 事实上，如果未在 SharePoint 服务器上启用动态母版页，则必须设置此属性。 有关 SharePoint 中的母版页的详细信息，请参阅[母版页](/previous-versions/office/developer/sharepoint-2010/ms443795(v=office.14))。

## <a name="see-also"></a>另请参阅
- [SharePoint深入了解基础开发](/previous-versions/office/developer/sharepoint-2010/ee539092(v=office.14))
- [ASP.NET 概述](/aspnet/overview)
- [ASP.NET 网页](/aspnet/web-pages/index)

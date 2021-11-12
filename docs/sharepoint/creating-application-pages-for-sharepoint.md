---
title: 为 SharePoint 创建应用程序页 | Microsoft Docs
description: 为 SharePoint 创建应用程序页。 应用程序页是专为在 SharePoint 网站中使用而设计的 ASP.NET 网页。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665295"
---
# <a name="create-application-pages-for-sharepoint"></a>为 SharePoint 创建应用程序页
  应用程序页是专为在 SharePoint 网站中使用而设计的 ASP.NET 网页。 应用程序页是一种专用类型的 ASP.NET 页面。 应用程序页和标准 ASP.NET 页之间的主要区别在于，应用程序页包含与 SharePoint 母版页合并的内容。 母版页使应用程序页能够与网站上的其他页面共享相同的外观和行为。

 使用 Visual Studio，可以通过设计器设计应用程序页。 设计器为母版页中定义的每个内容占位符显示一个内容区域。 可以通过将控件拖动到这些内容区域来设计应用程序页。

## <a name="application-pages"></a>应用程序页
 应用程序页在服务器上的所有网站之间共享，而网站页特定于一个网站。 有关详细信息，请参阅 [SharePoint 页面类型](/previous-versions/office/developer/sharepoint-2010/aa979592(v=office.14))。

 默认情况下，创建 SharePoint 网站时显示的大多数页面都是网站页。 网站页可以添加到 SharePoint 页面库中。 用户可使用 SharePoint Designer 等工具自定义网站页。 网站页还可以承载动态 Web 部件和 Web 部件区域等功能。

 应用程序页无法执行这些操作。 但如果希望页面包含自定义代码，则应用程序页是应创建的最佳页面类型。 尽管可向网站页添加自定义代码，但当用户使用 SharePoint Designer 等工具自定义页面时，代码将停止运行。

> [!NOTE]
> Visual Studio 不提供模板来帮助你为 SharePoint 网站创建网站页。 有关详细信息，请参阅 [SharePoint 页面类型](/previous-versions/office/developer/sharepoint-2010/aa979592(v=office.14))。

## <a name="create-an-application-page"></a>创建应用程序页
 若要创建应用程序页，请向 SharePoint 项目添加“应用程序页”项。 创建应用程序页时，Visual Studio 会将以下文件夹添加到项目中：

|文件夹|说明|
|------------|-----------------|
|布局|映射到 SharePoint 文件系统的 _layouts 虚拟目录。|
|布局子文件夹|包含构成应用程序页的文件。 默认情况下，此文件夹与项目同名。 可以随时重命名此文件夹。 运行项目时，Visual Studio 会将此文件夹部署到 SharePoint 文件系统的 _layouts 虚拟目录中。|

 Visual Studio 会将以下文件添加到项目：

|文件|说明|
|----------|-----------------|
|ASP.NET 页面文件 (.aspx)|包含用于定义页面的 XML 标记。|
|应用程序页代码文件|包含应用程序页背后的代码。 将处理事件的代码添加到此文件。|
|应用程序页设计器代码文件|包含设计器生成的代码。 不要直接编辑此文件。|

## <a name="design-and-debug-an-application-page"></a>设计和调试应用程序页
 使用 Visual Studio 中的设计器视图设计应用程序页的内容。 在打开项目中的应用程序页（通过双击此页或通过打开其快捷菜单并选择“打开”），然后选择编辑器底部的“设计”按钮时，将显示此设计器 。

> [!NOTE]
> 只能在设计器的“源”视图中设计页面。 应用程序页禁用设计器的“设计”视图。

 可以像在 Visual Studio 中调试其他 SharePoint 项目项一样调试应用程序页。 当你启动 Visual Studio 调试器时，Visual Studio 将打开 SharePoint 网站。

 若要查看应用程序页，必须手动转到应用程序页的位置（例如： http://<em>Server_Name</em>/_layouts/*Project_Name*/ApplicationPage1.aspx）。

 有关如何调试 SharePoint 项目的详细信息，请参阅 [SharePoint 解决方案疑难解答](../sharepoint/troubleshooting-sharepoint-solutions.md)。

## <a name="choose-a-master-page"></a>选择母版页
 默认情况下，“应用程序页”项引用要用于调试项目的网站的母版页。 该页名为 v4.master，可在 SharePoint 网站的“母版页库”中找到。

 可通过设置应用程序 `Page` 元素的 `MasterPageFile` 属性，显式更改应用程序页使用的母版页。 （例如：`MasterPageFile="~/_layouts/applicationv4.master"`）。 事实上，如果未在 SharePoint 服务器上启用动态母版页，则必须设置此属性。 有关 SharePoint 中母版页的详细信息，请参阅[母版页](/previous-versions/office/developer/sharepoint-2010/ms443795(v=office.14))。

## <a name="see-also"></a>另请参阅
- [SharePoint Foundation 开发详解](/previous-versions/office/developer/sharepoint-2010/ee539092(v=office.14))
- [ASP.NET 概述](/aspnet/overview)
- [ASP.NET 网页](/aspnet/web-pages/index)

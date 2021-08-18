---
title: 如何：创建应用程序页|Microsoft Docs
description: 为一 ASP.NET 个 (站点创建) 应用程序Visual Studio应用程序SharePoint网页。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application pages [SharePoint development in Visual Studio], adding
- application pages [SharePoint development in Visual Studio], creating
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 211bba75c6acee1a820a2b8b4adaefb508818a04
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122060071"
---
# <a name="how-to-create-an-application-page"></a>如何：创建应用程序页
  可以为一个或多个 SharePoint 网站创建 ASP.NET 网页。 在SharePoint中，这些页面称为应用程序页。 与站点页不同，应用程序页包含页面后面运行的代码。 有关详细信息，请参阅[为应用程序创建SharePoint。](../sharepoint/creating-application-pages-for-sharepoint.md)

### <a name="to-create-an-application-page"></a>创建应用程序页

1. 在 Visual Studio 中打开或创建一个 SharePoint 项目。

     有关详细信息，请参阅SharePoint[和项目项模板](../sharepoint/sharepoint-project-and-project-item-templates.md)。

2. 在 **“解决方案资源管理器”** 中，选择项目节点。

3. 在菜单栏上，依次选择“项目” > “添加新项”。

4. 在"**添加新项"** 对话框中，展开"SharePoint"**节点**，然后选择 **"2010"** 项。

5. 在模板列表中，SharePoint"**应用程序页"。**

6. 在 **"名称** "框中，指定应用程序页的名称，然后选择"添加 **"** 按钮。

     Visual Studio向项目添加多个文件夹和文件。 有关这些文件的信息，请参阅[为应用程序创建SharePoint。](../sharepoint/creating-application-pages-for-sharepoint.md)

     在 **Visual** Web 开发人员设计器的"源"视图中，ASP.NET 页面文件。 可以通过从"工具箱"添加控件，并放置在内容占位符上来设计页面。 有关详细信息，请参阅源 [视图、网页设计器](/previous-versions/aspnet/ms178154\(v\=vs.100\))。

7. 如果您要处理控件事件，请向应用程序页的代码文件添加代码。

     如果展开页面文件的节点，并且具有 *.cs* 或 *.vb* 扩展名，则代码文件将显示 ASP.NET，具体取决于项目的语言。 有关如何创建应用程序页的端到端示例，请参阅演练：创建SharePoint[页](../sharepoint/walkthrough-creating-a-sharepoint-application-page.md)。

## <a name="see-also"></a>请参阅
- [为 SharePoint 创建应用程序页](../sharepoint/creating-application-pages-for-sharepoint.md)
- [演练：创建 SharePoint 应用程序页](../sharepoint/walkthrough-creating-a-sharepoint-application-page.md)

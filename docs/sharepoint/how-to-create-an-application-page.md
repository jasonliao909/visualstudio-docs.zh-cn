---
title: 如何：创建应用程序页 | Microsoft Docs
description: 在一个或多个 SharePoint 站点的 Visual Studio 中创建 ASP.NET 网页（也称为应用程序页）。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665291"
---
# <a name="how-to-create-an-application-page"></a>如何：创建应用程序页
  可以为一个或多个 SharePoint 网站创建 ASP.NET 网页。 在 SharePoint 中，这些页称为应用程序页。 与网站页不同，应用程序页包含在该页后面运行的代码。 有关详细信息，请参阅[为 SharePoint 创建应用程序页](../sharepoint/creating-application-pages-for-sharepoint.md)。

### <a name="to-create-an-application-page"></a>创建应用程序页

1. 在 Visual Studio 中打开或创建一个 SharePoint 项目。

     有关详细信息，请参阅 [SharePoint 项目和项目项模板](../sharepoint/sharepoint-project-and-project-item-templates.md)。

2. 在 **“解决方案资源管理器”** 中，选择项目节点。

3. 在菜单栏上，依次选择“项目” > “添加新项”。

4. 在“添加新项”对话框中，展开“SharePoint”节点，然后选择“2010”项  。

5. 在 SharePoint 模板列表中，选择“应用程序页”。

6. 在“名称”框中，指定应用程序页的名称，然后选择“添加”按钮 。

     Visual Studio 将多个文件夹和文件添加到项目。 有关这些文件的详细信息，请参阅[为 SharePoint 创建应用程序页](../sharepoint/creating-application-pages-for-sharepoint.md)。

     在 Visual Web Developer 设计器的“源”视图中，将显示 ASP.NET 页文件。 你可以通过从“工具箱”添加控件并将其置于内容占位符上来设计页。 有关详细信息，请参阅[“源”视图，网页设计器](/previous-versions/aspnet/ms178154\(v\=vs.100\))。

7. 如果您要处理控件事件，请向应用程序页的代码文件添加代码。

     如果展开 ASP.NET 页文件的节点并具有 .cs 或 .vb 扩展名（取决于项目语言），将显示代码文件 。 有关如何创建应用程序页的端到端示例，请参阅[演练：创建 SharePoint 应用程序页](../sharepoint/walkthrough-creating-a-sharepoint-application-page.md)。

## <a name="see-also"></a>另请参阅
- [为 SharePoint 创建应用程序页](../sharepoint/creating-application-pages-for-sharepoint.md)
- [演练：创建 SharePoint 应用程序页](../sharepoint/walkthrough-creating-a-sharepoint-application-page.md)

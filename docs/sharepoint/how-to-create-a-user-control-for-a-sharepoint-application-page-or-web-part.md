---
title: 为 SharePoint 应用程序页或 web 部件创建用户控件
titleSuffix: ''
description: 创建自定义用户控件，为你的 SharePoint 解决方案提供自定义功能，并在 web 部件或应用程序页中重复使用该功能。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- user controls [SharePoint development in Visual Studio], creating
- user controls [SharePoint development in Visual Studio], adding
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 891f68a44087506ad2d61c3db7ead70d5a01ae70
ms.sourcegitcommit: 541871db9065c4fb1b21c24f980c563991b183c7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2021
ms.locfileid: "129430784"
---
# <a name="how-to-create-a-user-control-for-a-sharepoint-application-page-or-web-part"></a>如何：为 SharePoint 应用程序页或 Web 部件创建用户控件
  可以创建为 SharePoint 解决方案提供自定义功能的自定义用户控件，您可以在项目中重复使用此功能。 可以在 Web 部件或应用程序页中包含用户控件、添加其他 ASP.NET 控件和 SharePoint 控件、定义控件的属性和方法。 有关用户控件的详细信息，请参阅为[web 部件或应用程序页创建可重用控件或](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)在 SharePoint 中创建用户控件和服务器控件。

### <a name="to-create-a-user-control-for-sharepoint"></a>为 SharePoint 创建用户控件

1. 在 Visual Studio 中打开或创建一个 SharePoint 项目。

     请参阅[SharePoint 项目和项目项模板](../sharepoint/sharepoint-project-and-project-item-templates.md)。

2. 在 **“解决方案资源管理器”** 中，选择项目节点。

3. 在菜单栏上，依次选择“项目” > “添加新项”。

     此时将打开“添加新项”对话框。

4. 在 "**已安装**" 窗格中，选择 " **Office/SharePoint** " 节点。

5. 在 SharePoint 模板列表中，选择 "**用户控件" "仅 (场解决方案**" ") "。

    > [!NOTE]
    > 用户控件仅适用于场解决方案。

6. 在 " **名称** " 框中，指定用户控件的名称，然后选择 " **添加** " 按钮。

     Visual Studio 将多个文件夹和文件添加到项目。 有关这些文件的详细信息，请参阅 [为 web 部件或应用程序页创建可重用控件](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)。

     默认情况下，用户控件文件将显示在 Visual Web Developer 设计器的 " **源** " 视图中。 在此视图中，您可以编辑该控件的 XML 标记。 如果希望通过从工具箱中拖动控件来以可视方式设计控件，则可以切换到 **"****设计**" 视图。 请参阅 [设计视图网页设计器](/previous-versions/aspnet/ms178149\(v\=vs.100\))。

7. 如果要处理控件中发生的事件，请将代码添加到此用户控件的代码文件。

     此文件将显示在用户控件文件下 **解决方案资源管理器** 中，并具有 *.cs* 或 *.vb* 扩展名（具体取决于项目的语言）。

## <a name="see-also"></a>另请参阅
- [为 Web 部件或应用程序页创建可重用控件](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)
- [为 SharePoint 创建应用程序页](../sharepoint/creating-application-pages-for-sharepoint.md)
- [为 SharePoint 创建 Web 部件](../sharepoint/creating-web-parts-for-sharepoint.md)

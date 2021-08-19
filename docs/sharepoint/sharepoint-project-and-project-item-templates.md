---
title: SharePoint Project和Project项模板|Microsoft Docs
description: 查看项目和项目SharePoint模板的可用说明及其使用方式。
ms.custom: SEO-VS-2020
ms.date: 02/22/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.SPE.FirstWizardPage
- VS.SharePointTools.SPE.ListInstance
- VS.SharePointTools.SPE.ListDefinition
- VS.SharePointTools.SPE.ListDefFromContentType
- VS.SharePointTools.SPE.ContentType
- SPE.Wizard
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, project and project item templates
- SharePoint development in Visual Studio, templates
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 2949bf27910f90cee2e109e64d0d6741439806fc
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122115559"
---
# <a name="sharepoint-project-and-project-item-templates"></a>SharePoint项目和项目项模板
  以下部分介绍了项目和SharePoint模板的可用模板及其使用方式。

## <a name="project-and-project-item-templates-overview"></a>Project和项目项模板概述
 在 SharePoint 项目Visual Studio，SharePoint项目与该项目类型所需的所有项目项一起添加到解决方案中。 例如，如果创建 Silverlight Web 部件项目，Visual Studio 将创建一个解决方案，其中包含 Visual Web 部件项目项和 Silverlight 应用程序项目项以及这些项目项所需的所有文件。 Project项模板用于将项目项添加到现有SharePoint项目，例如添加事件接收器、站点列或列表。

 有关基础SharePoint，请参阅 SharePoint Foundation[构建基块](/previous-versions/office/developer/sharepoint-2010/ee534971(v=office.14))。 高级用户可以创建自定义项目和项目项模板。 有关详细信息，请参阅[扩展 SharePoint 项目系统](../sharepoint/extending-the-sharepoint-project-system.md)。

## <a name="project-templates"></a>项目模板
 下面是一系列SharePoint模板。 若要查看 Visual Studio 中的 SharePoint 项目模板，在"新建 Project"对话框中，展开 **Visual C#** 或 Visual Basic 下的 **SharePoint** 节点，然后选择 **"2010"。** 

### <a name="sharepoint-2010-project"></a>SharePoint 2010 项目
 *2010 SharePoint 2010* Project的内容包含在每个SharePoint模板中。 2010 SharePoint 2010 Project包含：

- 项目文件。

- 项目属性页。

- 列出 **项目中** 所有程序集引用的 References 文件夹。

- 包含 **.feature** 配置文件 *的 Features* 文件夹，用于将功能部署到SharePoint服务器。

- 包含 *Package.package 文件的 Package* 文件夹，用于将解决方案部署到SharePoint。

- key.snk (强名称密钥) 文件，该文件用于使用强名称对程序集进行签名，以增强安全性。

### <a name="sharepoint-2010-silverlight-web-part"></a>SharePoint 2010 Silverlight Web 部件
 *SharePoint 2010 Silverlight Web 部件* 项目，你可以为显示 Silverlight SharePoint创建 Web 部件。 创建此项目时，可以指定是向它添加新的 Silverlight 应用程序还是引用现有的 Silverlight 应用程序。 有关详细信息，请参阅[为](../sharepoint/creating-web-parts-for-sharepoint.md)SharePoint 创建 Web 部件和演练：创建显示 OData 的 Silverlight web[部件SharePoint。](../sharepoint/walkthrough-creating-a-silverlight-web-part-that-displays-odata-for-sharepoint.md)

### <a name="sharepoint-2010-visual-web-part"></a>SharePoint 2010 视觉对象 Web 部件
 *2010 SharePoint 2010 Visual*  Web 部件项目包括Elements.xml定义文件 **、Web** 部件项和用户 **控件** 项。 可以通过将控件从"工具箱"Visual Studio拖动或复制到用户控件的图面上来设计可视 Web 部件的外观。 有关详细信息，请参阅[如何：](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md)使用设计器创建SharePoint Web 部件和构建基块[：Web 部件。](/previous-versions/office/developer/sharepoint-2010/ee535520(v=office.14))

### <a name="import-sharepoint-2010-solution-package"></a>导入SharePoint 2010 解决方案包
 *通过导入 SharePoint 2010* 解决方案包项目，你可以将现有 SharePoint 2010 站点（导出到 SharePoint 解决方案 (*.wsp*) 文件）的所有或部分导入到 Visual Studio。 导入到 Visual Studio，可以自定义其项并重新部署它们。 有关详细信息，请参阅[从现有数据库站点 导入SharePoint项](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)。

### <a name="import-reusable-sharepoint-2010-workflow"></a>导入可重用SharePoint 2010 工作流
 *导入可重用SharePoint 2010* 工作流项目，使你可以将 SharePoint Designer 2010 中创建的可重用声明性工作流导入Visual Studio。 工作流作为 *.wsp* SharePoint从站点导出。 导入到 Visual Studio后，可以对其进行自定义，向它添加代码，然后将它部署到SharePoint站点。 有关详细信息，请参阅演练：将 SharePoint[设计器可重用工作流导入 Visual Studio。](../sharepoint/walkthrough-import-a-sharepoint-designer-reusable-workflow-into-visual-studio.md)

## <a name="project-item-templates"></a>Project项模板
 下面是项目项SharePoint的列表。 Project模板将文件添加到 SharePoint 解决方案，SharePoint站点列、列表和内容类型等新功能。 例如，将站点列添加到解决方案会添加一个站点列项目，其中包含 *Elements.xml定义文件* 。 添加可视化 Web 部件会将可视化 Web 部件 *项目* 添加到解决方案，其中包含Elements.xml文件、用户控件项和可视 Web 部件项。

 若要查看项目SharePoint模板，解决方案资源管理器 **中，** 打开 SharePoint 项目的快捷菜单，然后选择 **"添加"** 和"新建项 **"。** 在 Visual **C#** **SharePoint** 下展开"Visual Basic"**节点**，然后选择 **"2010"。**

### <a name="application-page-farm-solution-only"></a>仅 (场解决方案的应用程序) 
 "**应用程序页 (场解决方案) "** 项可用于为 SharePoint [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] 网站设计网页。 应用程序页只能在场解决方案中使用。 只能将此项目项添加到场解决方案。 有关详细信息，请参阅 [如何：创建应用程序页](../sharepoint/how-to-create-an-application-page.md) 和应用程序 [_layouts页类型](/previous-versions/office/aa979604(v=office.14))。

### <a name="business-data-connectivity-model-farm-solution-only"></a>仅场解决方案 (业务数据连接) 
 "**仅场解决方案 (业务** 数据连接模型) 项使你能够将业务数据集成到SharePoint。 业务数据可能来自后端服务器应用程序，例如 、Siebel 和服务广告协议 ([!INCLUDE[ssNoVersion](../sharepoint/includes/ssnoversion-md.md)] SAP) 。 业务数据连接模型只能在场解决方案中使用。 只能将此项目项添加到场解决方案。 有关详细信息，请参阅如何：创建[BDC](../sharepoint/how-to-create-a-bdc-model.md)模型、如何[：](../sharepoint/how-to-use-a-resource-file-to-specify-localized-names-properties-and-permissions.md)使用资源文件指定本地化名称、属性和权限和新增功能[：业务连接服务](/previous-versions/office/developer/sharepoint-2010/ee534979(v=office.14))。

### <a name="content-type"></a>内容类型
 *使用"* 内容类型"项，可基于现有内容类型 (文档) 公告或任务等基本内容类型创建自定义内容类型。 自定义内容类型提供与基本内容类型相同的属性和字段，以及定义 (字段) 站点列。 例如，可以创建基于"联系人"内容类型（基于"联系人"内容类型）的自定义"联系人"内容SharePoint。 可以通过更改现有站点列或将更多站点列添加到已包含在基本内容类型中的站点列来自定义内容类型。

> [!NOTE]
> 由于存在SharePoint限制，无法基于沙盒解决方案内容类型创建场解决方案内容类型。

 有关详细信息，请参阅[演练：](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md)创建站点列、内容类型和列表SharePoint构建基块[：内容类型](/previous-versions/office/developer/sharepoint-2010/ee535063(v=office.14))。

### <a name="empty-element"></a>空元素
 *空* 元素通常用于定义SharePoint中缺少项目或项目项模板的项目Visual Studio。 向项目添加空元素时，将创建名为 EmptyElement[x] (其中 [x] 是唯一 \) 数字的节点。 EmptyElement[x] 包含名为 *Elements.xml。* 使用 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 语句在 中定义Elements.xml。 **

### <a name="event-receiver"></a>事件接收器
 *事件接收器* 处理 SharePoint 站点中的项的事件，例如将项添加到列表、删除 Web 项时或工作流启动时。 事件接收器项目项模板允许处理

- 列出事件

- 列出项事件

- 列出电子邮件事件

- Web 事件

- 列出工作流事件

  事件接收器项目项创建一个事件接收器文件夹，其中包含一个类文件，其中包含在自定义向导 中创建项目时指定的SharePoint **的事件处理程序**。 当添加、更新、删除或删除文件、字段、项、列表、附件、Web 部件和工作流等项时，事件接收器类可以处理 SharePoint 站点上发生的事件。 有关详细信息，请参阅 [如何：创建事件接收器](../sharepoint/how-to-create-an-event-receiver.md) 和 [构建基块：事件处理](/previous-versions/office/developer/sharepoint-2010/ee535057(v=office.14))。

### <a name="list"></a>列出
 列表是可重用的基类SharePoint列表定义（如日历或任务列表）的实例。 将列表添加到解决方案后，使用列表设计器可以将站点列添加到列表中并创建自定义列表列。 这包括来自内容类型的站点列。 可以指定列表 *的* 视图，该视图确定列表中将显示的列。 有关详细信息，请参阅[演练：](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md)创建站点列、内容类型和列表SharePoint构建基块：列表和[文档库](/previous-versions/office/developer/sharepoint-2010/ee534985(v=office.14))。

### <a name="module"></a>模块
 *模块* (与模块混淆) 模块包含要部署到 SharePoint 服务器的任何文件，例如 [!include[vbprvb](../sharepoint/includes/vbprvb-md.md)] 映像或便笺。 模块项目项 **包含模块节点** 。 模块节点包含两个项目项模板：一个 XML 定义文件（充当模块的清单）和一个 *sample.txt文件（* 占位符文件）。 有关详细信息，请参阅使用[模块在解决方案和模块中包括](../sharepoint/using-modules-to-include-files-in-the-solution.md)[文件](/previous-versions/office/developer/sharepoint-2010/ms453137(v=office.14))。

### <a name="sequential-workflow-farm-solution-only"></a>顺序工作流 (场解决方案) 
 顺序 *工作流* 是一系列业务逻辑步骤，按顺序执行，直到最后一个步骤完成。 顺序工作流用于管理涉及列表SharePoint文档等项目的进程。 可以创建站点级 (全局) 工作流或列表级别 (本地) 工作流，还可以选择是自动还是手动启动工作流。 此项目项只能在场解决方案中使用。 只能将此项目项添加到场解决方案。 有关详细信息，请参阅[创建SharePoint](../sharepoint/creating-sharepoint-workflow-solutions.md)解决方案[、SharePoint Server 2010](/previous-versions/office/developer/sharepoint-2010/ms549489(v=office.14))中的工作流和[新增功能：工作流改进](/previous-versions/office/developer/sharepoint-2010/ee537015(v=office.14))。

### <a name="silverlight-web-part"></a>Silverlight Web 部件
 *silverlight web 部件* 项目项使你可以为显示 Silverlight 应用程序 SharePoint 创建 web 部件。 将此项目项添加到解决方案中时，可以选择是添加新的 Silverlight 应用程序还是稍后引用现有的 Silverlight 应用程序。 有关详细信息，请参阅为[SharePoint 创建 web 部件](../sharepoint/creating-web-parts-for-sharepoint.md)和[演练：创建显示 OData 的 Silverlight web 部件 SharePoint](../sharepoint/walkthrough-creating-a-silverlight-web-part-that-displays-odata-for-sharepoint.md)。

### <a name="site-column"></a>网站列
 *网站列* 也称为 *字段*，是可添加到 SharePoint 项目中的最基本的元素之一。 网站列代表一种类型的数据，例如电话号码、文本注释或联系人列表中联系人的城市名称。 有关详细信息，请参阅为 SharePoint 和[列](/previous-versions/office/developer/sharepoint-2010/ms196085(v=office.14))[创建网站列、内容类型和列表](../sharepoint/creating-site-columns-content-types-and-lists-for-sharepoint.md)。

### <a name="site-definition-farm-solution-only"></a>站点定义 (场解决方案仅) 
 *网站定义* 项目项包含包含以下文件的站点定义文件夹：

- Default.aspx 页，用作站点的默认网页。

- 定义站点组件的 *onet.xml* 文件。

- 一个 webtemp xml 文件，该文件指定在 "**新建 SharePoint 网站**" 页的 "**模板选择**" 部分中显示的站点定义配置。

  添加站点定义后，添加代码和文件以引入功能。 此项目项只能用于场解决方案。 只能将此项目项添加到场解决方案。 有关详细信息，请参阅为 SharePoint 和[站点定义和配置](/previous-versions/office/developer/sharepoint-2010/aa978512(v=office.14))[创建站点定义](../sharepoint/creating-site-definitions-for-sharepoint.md)。

### <a name="state-machine-workflow-farm-solution-only"></a>状态机工作流 (场解决方案仅) 
 *状态机工作流* 是一组业务逻辑状态、转换和操作。 不按顺序执行状态机工作流中的步骤;相反，它们由操作和状态触发。 与顺序工作流一样，状态机工作流与列表和文档等 SharePoint 项相关联。 同样，你可以创建网站级 (全局) 工作流或列表级别 (本地) 工作流。 你还可以选择工作流是自动启动还是手动启动。 此项目项只能用于场解决方案。 只能将此项目项添加到场解决方案。 有关详细信息，请参阅[创建 SharePoint 工作流解决方案](../sharepoint/creating-sharepoint-workflow-solutions.md)、 [SharePoint 服务器2010中的工作流](/previous-versions/office/developer/sharepoint-2010/ms549489(v=office.14))和[新增功能：工作流改进](/previous-versions/office/developer/sharepoint-2010/ee537015(v=office.14))。

### <a name="user-control-farm-solution-only"></a>仅限用户控件 (场解决方案) 
 *用户控件* 是一种自定义的可重用控件，可以将其他 ASP.NET 控件和 SharePoint 控件添加到该控件。 可以将用户控件添加到 SharePoint 中运行的应用程序页和 web 部件。 此项目项只能用于场解决方案。 只能将此项目项添加到场解决方案。 有关详细信息，请参阅为[Web 部件或应用程序页创建可重用控件](creating-reusable-controls-for-web-parts-or-application-pages.md)。

### <a name="visual-web-part"></a>可视 web 部件
 *可视 web 部件* 项目项包含 *Elements.xml* 定义文件、 **Web 部件** 项和 **用户控件** 项。 您可以通过将控件从 "Visual Studio" 工具箱拖到用户控件的表面来设计可视 web 部件的外观。 有关详细信息，请参阅[如何：使用设计器和构建块创建 SharePoint web 部件](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md) [： Web 部件](/previous-versions/office/developer/sharepoint-2010/ee535520(v=office.14))。

### <a name="web-part"></a>Web 部件
 *Web 部件* 是在一种称为 Web 部件页的特殊类型的页中运行的服务器端控件。 它们是显示在 SharePoint 网站上的页面的构建基块。 web 部件项目提供了一些文件，使您能够为 SharePoint 站点设计 web 部件。 有关详细信息，请参阅[如何：创建 SharePoint web 部件](../sharepoint/how-to-create-a-sharepoint-web-part.md)和[构建基块： Web 部件](/previous-versions/office/developer/sharepoint-2010/ee535520(v=office.14))。

## <a name="see-also"></a>请参阅
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
- [SharePoint Products and Technologies](/previous-versions/office/developer/sharepoint-2010/dd776256(v=office.12))

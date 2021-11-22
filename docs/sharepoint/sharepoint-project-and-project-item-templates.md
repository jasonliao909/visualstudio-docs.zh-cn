---
title: SharePoint 项目和项目项模板 | Microsoft Docs
description: 查看可用 SharePoint 项目和项目项模板的说明及其使用方式。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126663823"
---
# <a name="sharepoint-project-and-project-item-templates"></a>SharePoint 项目和项目项模板
  以下部分介绍可用 SharePoint 项目和项目项模板及其使用方式。

## <a name="project-and-project-item-templates-overview"></a>项目和项目项模板概述
 在 Visual Studio 中创建新的 SharePoint 项目时，SharePoint 项目会与该项目类型所需的所有项目项一起添加到解决方案。 例如，如果创建 Silverlight Web 部件项目，Visual Studio 将创建一个解决方案，其中包含 Visual Web 部件项目项和 Silverlight 应用程序项目项以及这些项目项所需的所有文件。 项目项模板用于将项目项添加到现有 SharePoint 项目，例如添加事件接收器、网站栏或列表。

 有关 SharePoint 基础知识的信息，请参阅 [SharePoint Foundation 构建基块](/previous-versions/office/developer/sharepoint-2010/ee534971(v=office.14))。 高级用户可以创建自定义项目和项目项模板。 有关详细信息，请参阅[扩展 SharePoint 项目系统](../sharepoint/extending-the-sharepoint-project-system.md)。

## <a name="project-templates"></a>项目模板
 下面列出了 SharePoint 项目模板。 若要在 Visual Studio 中查看 SharePoint 项目模板，请在“新建项目”对话框中，展开“Visual C#”或“Visual Basic”下的“SharePoint”节点，然后选择“2010”。

### <a name="sharepoint-2010-project"></a>SharePoint 2010 项目
 SharePoint 2010 项目的内容包含在每个 SharePoint 项目模板中。 SharePoint 2010 项目包含：

- 项目文件。

- 项目属性页。

- References 文件夹，列出项目中所有程序集引用。

- Features 文件夹，包含用于将功能部署到 SharePoint 服务器的 .feature 配置文件。

- Package 文件夹，包含用于将解决方案部署到 SharePoint 的 Package.package 配置文件。

- key.snk（强名称密钥）文件，用于使用强名称对程序集进行签名，以增强安全性。

### <a name="sharepoint-2010-silverlight-web-part"></a>SharePoint 2010 Silverlight Web 部件
 使用“SharePoint 2010 Silverlight Web 部件”项目可以为 SharePoint 创建显示 Silverlight 应用程序的 Web 部件。 创建此项目时，可以指定是向其添加新的 Silverlight 应用程序，还是引用现有的 Silverlight 应用程序。 有关详细信息，请参阅[为 SharePoint 创建 Web 部件](../sharepoint/creating-web-parts-for-sharepoint.md)和[演练：创建显示用于 SharePoint 的 OData 的 Silverlight Web 部件](../sharepoint/walkthrough-creating-a-silverlight-web-part-that-displays-odata-for-sharepoint.md)。

### <a name="sharepoint-2010-visual-web-part"></a>SharePoint 2010 可视 Web 部件
 SharePoint 2010 可视 Web 部件项目包括 Elements.xml 定义文件、Web 部件项和用户控件项。 可以通过将控件从 Visual Studio 工具箱拖放或复制到用户控件的图面上，设计可视 Web 部件的外观。 有关详细信息，请参阅[操作说明：使用设计器创建 SharePoint Web 部件](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md)和[构建基块：Web 部件](/previous-versions/office/developer/sharepoint-2010/ee535520(v=office.14))。

### <a name="import-sharepoint-2010-solution-package"></a>导入 SharePoint 2010 解决方案包
 使用“导入 SharePoint 2010 解决方案包”项目可以将导出到 SharePoint 解决方案 (.wsp) 文件的所有或部分现有 SharePoint 2010 网站导入 Visual Studio。 导入 Visual Studio 后，就可以自定义其项并重新部署它们。 有关详细信息，请参阅[从现有的 SharePoint 网站导入项](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)。

### <a name="import-reusable-sharepoint-2010-workflow"></a>导入可重用的 SharePoint 2010 工作流
 使用“导入可重用的 SharePoint 2010 工作流”项目可以将在 SharePoint Designer 2010 中创建的可重用声明性工作流导入 Visual Studio。 工作流作为 .wsp 文件从 SharePoint 网站导出。 导入 Visual Studio 后，就可以对其进行自定义，向其添加代码，然后将其部署到 SharePoint 网站。 有关详细信息，请参阅[演练：将 SharePoint Designer 可重用工作流导入 Visual Studio](../sharepoint/walkthrough-import-a-sharepoint-designer-reusable-workflow-into-visual-studio.md)。

## <a name="project-item-templates"></a>项目项模板
 下面列出了 SharePoint 项目项模板。 项目项模板将文件添加到 SharePoint 解决方案以支持网站栏、列表和内容类型等 SharePoint 功能。 例如，将网站栏添加到解决方案会添加一个网站栏项目，其中包含 Elements.xml 定义文件。 添加可视 Web 部件会将可视 Web 部件项目添加到解决方案，其中包含 Elements.xml 文件、用户控件项和可视 Web 部件项。

 若要查看 SharePoint 项目项模板，请在“解决方案资源管理器”中打开 SharePoint 项目的快捷菜单，然后选择“添加”、“新建项”。 展开“Visual C#”或“Visual Basic”下的“SharePoint”节点，然后选择“2010”。

### <a name="application-page-farm-solution-only"></a>应用程序页(仅场解决方案)
 使用“应用程序页(仅场解决方案)”项可以为 SharePoint 网站设计 [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] 网页。 应用程序页只能在场解决方案中使用。 只能将此项目项添加到场解决方案。 有关详细信息，请参阅[操作说明：创建应用程序页](../sharepoint/how-to-create-an-application-page.md)和[应用程序 _layouts 页类型](/previous-versions/office/aa979604(v=office.14))。

### <a name="business-data-connectivity-model-farm-solution-only"></a>业务数据连接模型(仅场解决方案)
 使用“业务数据连接模型(仅场解决方案)”项可以将业务数据集成到 SharePoint 中。 业务数据可以来自后端服务器应用程序，如 [!INCLUDE[ssNoVersion](../sharepoint/includes/ssnoversion-md.md)]、Siebel 和服务广告协议 (SAP)。 业务数据连接模型只能在场解决方案中使用。 只能将此项目项添加到场解决方案。 有关详细信息，请参阅[操作说明：创建 BDC 模型](../sharepoint/how-to-create-a-bdc-model.md)、[操作说明：使用资源文件指定本地化名称、属性和权限](../sharepoint/how-to-use-a-resource-file-to-specify-localized-names-properties-and-permissions.md)和[新增功能：Business Connectivity Services](/previous-versions/office/developer/sharepoint-2010/ee534979(v=office.14))。

### <a name="content-type"></a>内容类型
 使用“内容类型”项可以基于现有（基本）内容类型（如文档、公告或任务等）创建自定义内容类型。 自定义内容类型提供与基本内容类型相同的属性和字段，以及你定义的网站栏（字段）。 例如，可以基于来自 SharePoint 的基本联系人内容类型创建自定义联系人内容类型。 可以通过更改现有网站栏或将更多网站栏添加到已包含在基本内容类型中的网站栏来自定义内容类型。

> [!NOTE]
> 由于存在 SharePoint 限制，无法基于沙盒解决方案内容类型创建场解决方案内容类型。

 有关详细信息，请参阅[演练：创建 SharePoint 的网站栏、内容类型和列表](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md)和[构建基块：内容类型](/previous-versions/office/developer/sharepoint-2010/ee535063(v=office.14))。

### <a name="empty-element"></a>空元素
 空元素最常用于定义 Visual Studio 中缺少项目或项目项模板的 SharePoint 项目项。 向项目添加空元素时，将创建名为 EmptyElement[x]（其中 [x] 是唯一数字\)的节点。 EmptyElement[x] 包含名为 Elements.xml 的单个文件。 使用 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 语句在 Elements.xml 中定义所需的元素。

### <a name="event-receiver"></a>事件接收器
 事件接收器处理 SharePoint 网站中的项的事件，例如向列表添加项时、删除 Web 项时或启动工作流时。 事件接收器项目项模板允许处理

- 列出事件

- 列出项事件

- 列出电子邮件事件

- Web 事件

- 列出工作流事件

  事件接收器项目项创建带有单个类文件的“事件接收器”文件夹，其中包含在“SharePoint 自定义向导”中创建项目时指定的所有事件的事件处理程序。 当添加、更新、删除或移除文件、字段、项、列表、附件、Web 部件和工作流等项时，事件接收器类可以处理 SharePoint 网站上发生的事件。 有关详细信息，请参阅[操作说明：创建事件接收器](../sharepoint/how-to-create-an-event-receiver.md)和[构建基块：事件处理](/previous-versions/office/developer/sharepoint-2010/ee535057(v=office.14))。

### <a name="list"></a>列出
 列表是可重用基本 SharePoint 列表定义的实例，如日历或任务列表。 将列表添加到解决方案后，使用列表设计器可以将网站栏添加到列表并创建自定义列表栏。 这包括来自内容类型的网站栏。 可以指定列表的视图，该视图确定列表中将显示的栏。 有关详细信息，请参阅[演练：创建 SharePoint 的网站栏、内容类型和列表](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md)和[构建基块：列表和文档库](/previous-versions/office/developer/sharepoint-2010/ee534985(v=office.14))。

### <a name="module"></a>模块
 模块（不要与 [!include[vbprvb](../sharepoint/includes/vbprvb-md.md)] 模块混淆）包含要部署到 SharePoint 服务器的任何文件，例如图像或备注。 模块项目项包含模块节点。 模块节点包含两个项目项模板：XML 定义文件（充当模块的清单）和 sample.txt 文件（占位符文件）。 有关详细信息，请参阅[使用模块包括解决方案中的文件](../sharepoint/using-modules-to-include-files-in-the-solution.md)和[模块](/previous-versions/office/developer/sharepoint-2010/ms453137(v=office.14))。

### <a name="sequential-workflow-farm-solution-only"></a>顺序工作流(仅场解决方案)
 顺序工作流是一组业务逻辑步骤，这些步骤按顺序执行，直到最后一个步骤完成。 顺序工作流用于管理涉及列表和文档等 SharePoint 项的进程。 可以创建站点级别（全局）工作流或列表级别（本地）工作流，还可以选择工作流是自动启动还是手动启动。 此项目项只能在场解决方案中使用。 只能将此项目项添加到场解决方案。 有关详细信息，请参阅[创建 SharePoint 工作流解决方案](../sharepoint/creating-sharepoint-workflow-solutions.md)、[SharePoint Server 2010 中的工作流](/previous-versions/office/developer/sharepoint-2010/ms549489(v=office.14))和[新增功能：工作流改进](/previous-versions/office/developer/sharepoint-2010/ee537015(v=office.14))。

### <a name="silverlight-web-part"></a>Silverlight Web 部件
 使用“Silverlight Web 部件”项目项可以为 SharePoint 创建显示 Silverlight 应用程序的 Web 部件。 将此项目项添加到解决方案时，可以选择是添加新的 Silverlight 应用程序，还是引用现有的 Silverlight 应用程序。 有关详细信息，请参阅[为 SharePoint 创建 Web 部件](../sharepoint/creating-web-parts-for-sharepoint.md)和[演练：创建显示用于 SharePoint 的 OData 的 Silverlight Web 部件](../sharepoint/walkthrough-creating-a-silverlight-web-part-that-displays-odata-for-sharepoint.md)。

### <a name="site-column"></a>网站栏
 网站栏（也称为“字段”）是你可以向 SharePoint 项目添加的一种最基本元素。 网站栏表示数据的类型，例如联系人列表中某一联系人的电话号码、文本注释或者所在城市的名称。 有关详细信息，请参阅[创建 SharePoint 的站点栏、内容类型和列表](../sharepoint/creating-site-columns-content-types-and-lists-for-sharepoint.md)和[列](/previous-versions/office/developer/sharepoint-2010/ms196085(v=office.14))。

### <a name="site-definition-farm-solution-only"></a>网站定义(仅场解决方案)
 “网站定义”项目项包含网站定义文件夹，其中包含以下文件：

- 默认 .aspx 页，用作站点的默认网页。

- onet.xml 文件，用于定义网站的组件。

- webtemp xml 文件，用于指定在“新 SharePoint 网站”页的“模板选择”部分中显示的网站定义配置。

  添加网站定义后，添加代码和文件以引入功能。 此项目项只能在场解决方案中使用。 只能将此项目项添加到场解决方案。 有关详细信息，请参阅[创建 SharePoint 网站定义](../sharepoint/creating-site-definitions-for-sharepoint.md)和[网站定义和配置](/previous-versions/office/developer/sharepoint-2010/aa978512(v=office.14))。

### <a name="state-machine-workflow-farm-solution-only"></a>状态机工作流(仅场解决方案)
 状态机工作流是一组业务逻辑状态、转换和操作。 状态机工作流中的步骤不按顺序执行；而是由操作和状态触发。 与顺序工作流一样，状态机工作流与列表和文档等 SharePoint 项关联。 可以再次创建站点级别（全局）工作流或列表级别（本地）工作流。 还可以选择工作流是自动启动还是手动启动。 此项目项只能在场解决方案中使用。 只能将此项目项添加到场解决方案。 有关详细信息，请参阅[创建 SharePoint 工作流解决方案](../sharepoint/creating-sharepoint-workflow-solutions.md)、[SharePoint Server 2010 中的工作流](/previous-versions/office/developer/sharepoint-2010/ms549489(v=office.14))和[新增功能：工作流改进](/previous-versions/office/developer/sharepoint-2010/ee537015(v=office.14))。

### <a name="user-control-farm-solution-only"></a>用户控件(仅场解决方案)
 用户控件是可重用的自定义控件，可以向其添加其他 ASP.NET 控件和 SharePoint 控件。 用户控件可以添加到 SharePoint 中运行的应用程序页和 Web 部件。 此项目项只能在场解决方案中使用。 只能将此项目项添加到场解决方案。 有关详细信息，请参阅[为 Web 部件或应用程序页创建可重用控件](creating-reusable-controls-for-web-parts-or-application-pages.md)。

### <a name="visual-web-part"></a>可视 Web 部件
 “可视 Web 部件”项目项包括 Elements.xml 定义文件、Web 部件项和用户控件项。 可以通过将控件从 Visual Studio 工具箱拖放或复制到用户控件的图面上，设计可视 Web 部件的外观。 有关详细信息，请参阅[操作说明：使用设计器创建 SharePoint Web 部件](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md)和[构建基块：Web 部件](/previous-versions/office/developer/sharepoint-2010/ee535520(v=office.14))。

### <a name="web-part"></a>Web 部件
 Web 部件是在称为“Web 部件页”的特殊类型页面中运行的服务器端控件。 它们是在 SharePoint 网站上显示的页的构建基块。 Web 部件项提供可用于为 SharePoint 网站设计 Web 部件的文件。 有关详细信息，请参阅[操作说明：创建 SharePoint Web 部件](../sharepoint/how-to-create-a-sharepoint-web-part.md)和[构建基块：Web 部件](/previous-versions/office/developer/sharepoint-2010/ee535520(v=office.14))。

## <a name="see-also"></a>另请参阅
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
- [SharePoint Products and Technologies](/previous-versions/office/developer/sharepoint-2010/dd776256(v=office.12))

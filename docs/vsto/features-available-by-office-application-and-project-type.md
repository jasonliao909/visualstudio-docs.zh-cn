---
title: 应用程序类型和Office可用的功能
description: 了解Visual Studio有多种类型的项目模板，这些模板支持应用程序的不同业务Microsoft Office方案。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application-level add-ins [Office development in Visual Studio]
- Office development in Visual Studio, features
- Ribbon [Office development in Visual Studio]
- Office applications [Office development in Visual Studio], features available
- document-level customizations [Office development in Visual Studio]
- Office projects [Office development in Visual Studio], features available
- add-ins [Office development in Visual Studio]
- form regions [Office development in Visual Studio], features available
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: bb532244198a26da0106652f3c1167ef111c91ed
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122106349"
---
# <a name="features-available-by-office-application-and-project-type"></a>应用程序类型和Office可用的功能
  Visual Studio 具有几种类型的项目模板，它们支持 Microsoft Office 应用程序的不同业务方案，包括以下类型：

- 文档级自定义项。

- VSTO 外接程序

  并非所有应用程序都可以使用所有项目类型。 例如，文档级项目仅可用于 Microsoft Office Word 和 Microsoft Office Excel。 同样，某些功能仅可用于特定类型的项目或应用程序。 例如，操作窗格仅在文档级项目中可用，而功能区扩展仅可用于某些应用程序。 有关不同项目类型的更多信息，请参阅 Office[解决方案开发&#40;VSTO&#41;。 ](../vsto/office-solutions-development-overview-vsto.md)

> [!NOTE]
> Office 项目模板仅在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 的某些版本中可用。 有关详细信息，请参阅[配置计算机以开发Office解决方案](../vsto/configuring-a-computer-to-develop-office-solutions.md)。

## <a name="project-types-available-for-different-microsoft-office-applications"></a>Project应用程序可用的Microsoft Office类型
 下表显示了可使用所有项目类型的应用程序。

|项目类型|Microsoft Office 应用程序|
|-------------------|----------------------------------|
|文档级自定义项|Excel<br /><br /> 单词|
|VSTO 外接程序|Excel<br /><br /> InfoPath（仅 InfoPath 2013 和 InfoPath 2010）<br /><br /> Outlook<br /><br /> PowerPoint<br /><br /> Project<br /><br /> Visio<br /><br /> Word<br /><br /> Excel|

## <a name="features-available-in-different-project-types"></a>不同项目类型中提供的功能
 下表显示了提供每项功能的项目类型。

|特征|提供该功能的项目类型|延伸阅读|
|-------------|--------------------------------------------|---------------------|
|操作窗格。|文档级项目。|[操作窗格概述](../vsto/actions-pane-overview.md)|
|ClickOnce 部署。|VS 与文档级项目。|[部署 Office 解决方案](../vsto/deploying-an-office-solution.md)|
|自定义任务窗格。|以下应用程序的 VSTO 外接程序项目：<br /><br /> - Excel<br />- InfoPath (InfoPath 2013 和 InfoPath 2010) <br />- Outlook<br />- PowerPoint<br />- Word|[自定义任务窗格](../vsto/custom-task-panes.md)|
|自定义 XML 部件。|文档级项目。<br /><br /> 以下应用程序的应用程序级项目：<br /><br /> - Excel<br />- PowerPoint<br />- Word|[自定义 XML 部件概述](../vsto/custom-xml-parts-overview.md)|
|数据缓存。|文档级项目。|[文档级自定义项中的缓存数据](../vsto/cached-data-in-document-level-customizations.md)|
|将外接程序中的VSTO公开给其他 Microsoft Office 解决方案。|VSTO 外接程序项目。|[从其他 VSTO 解决方案调用外接程序Office代码](../vsto/calling-code-in-vsto-add-ins-from-other-office-solutions.md)|
|以下主机控件：<br /><br /> - 图表<br />- ListObject<br />- NamedRange<br />- 内容控件<br />- 书签|文档级项目。<br /><br /> 用于 Word 和 Excel 的 VSTO 外接程序项目。|[主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)|
|以下主机控件：<br /><br /> - XMLMappedRange<br />- XMLNode<br />- XMLNodes|文档级项目。|[主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)|
|多项目部署。|文档级项目。<br /><br /> VSTO 外接程序项目。|[演练：在单个 Office 安装程序中部署多个 ClickOnce 解决方案](/previous-versions/dd465290(v=vs.110))|
|Outlook 窗体区域。|用于 Outlook 的 VSTO 外接程序项目。|[创建Outlook窗体区域](../vsto/creating-outlook-form-regions.md)|
|部署后操作。|文档级项目。<br /><br /> VSTO 外接程序项目。|[演练：在安装后将文档复制到最终用户ClickOnce计算机](/previous-versions/dd465291(v=vs.110))|
|功能区自定义。|文档级项目。<br /><br /> 以下应用程序的 VSTO 外接程序项目：<br /><br /> - Excel<br />- InfoPath (InfoPath 2013 和 InfoPath 2010) <br />- Outlook<br />- PowerPoint<br />- Project<br />- Visio<br />- Word|[功能区概述](../vsto/ribbon-overview.md)|
|可视化文档设计器。|文档级项目。|[Visual Studio 环境中的 Office 项目](../vsto/office-projects-in-the-visual-studio-environment.md)|

## <a name="see-also"></a>请参阅
- [&#40;Visual Studio 中的 Office 开发入门&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
- [Office 解决方案开发概述 &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)
- [操作窗格概述](../vsto/actions-pane-overview.md)
- [功能区概述](../vsto/ribbon-overview.md)
- [创建 Outlook 窗体区域](../vsto/creating-outlook-form-regions.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [文档级自定义项中的缓存数据](../vsto/cached-data-in-document-level-customizations.md)
- [部署 Office 解决方案](../vsto/deploying-an-office-solution.md)
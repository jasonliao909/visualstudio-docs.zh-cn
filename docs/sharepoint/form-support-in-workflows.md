---
title: 工作流中的窗体支持 | Microsoft Docs
description: 阅读有关 SharePoint 工作流中的窗体支持的信息。 可以在工作流中使用四种类型的窗体：关联、启动、任务和修改。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, workflows
- workflows [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: c10373f0c04a6c68faff795d08ff0e288ce02836
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122106908"
---
# <a name="form-support-in-workflows"></a>工作流中的窗体支持
  可以在工作流中使用四种类型的窗体：关联、启动、任务和修改。 这些窗体类型可以基于 ASPX 窗体或 InfoPath 窗体。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 为特定窗体提供的支持级别取决于几个因素，如下表所示。 有关工作流窗体类型的详细信息，请参阅[工作流窗体概述](/previous-versions/office/developer/sharepoint-2010/ms457061(v=office.14))。

## <a name="xml-refactoring"></a>XML 重构
 将 ASPX 关联或启动窗体添加到 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 工作流项目项时，[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 会自动重构工作流的 Elements.xml 文件中的 XML，以便在更新窗体名称或部署路径或删除窗体时，使引用关联或启动窗体的属性保持同步。 但是，在工作流中使用其他窗体类型（例如，任务或修改窗体）时，不会重构 Elements.xml 文件。

## <a name="form-support-in-new-visual-studio-workflows"></a>新 Visual Studio 工作流中的窗体支持
 下表列出了对工作流（在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中创建）中的 ASPX 或 InfoPath 窗体上的不同窗体类型的 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 支持。

|窗体类型|在 Visual Studio 中使用 ASPX 窗体创建的工作流|在 Visual Studio 中使用 InfoPath 窗体创建的工作流|
|---------------|---------------------------------------------------------|-----------------------------------------------------------------|
|关联|-   通过使用“工作流关联窗体”项模板，可以将 ASPX 关联窗体添加到工作流中。<br />-   当添加、重命名或删除窗体，或者当窗体的部署路径发生更改时，将重构工作流的 Elements.xml 文件。<br />-   有关详细信息，请参阅[演练：创建带有关联窗体和启动窗体的工作流](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)。|-   [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中没有 InfoPath 关联窗体模板。<br />-   [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 和 InfoPath 设计器之间没有集成。<br />-   工作流的 Elements.xml 文件未重构。|
|启动|-   通过使用“工作流启动窗体”项模板，可以将 ASPX 启动窗体添加到工作流中。<br />-   当添加、重命名或删除窗体，或者当窗体的部署路径发生更改时，将重构工作流的 Elements.xml 文件。<br />-   有关详细信息，请参阅[演练：创建带有关联窗体和启动窗体的工作流](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)。|-   [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中没有 InfoPath 关联窗体模板。<br />-   [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 和 InfoPath 设计器之间没有集成。<br />-   工作流的 Elements.xml 文件未重构。|
|任务|-   [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中没有可用的 ASPX 任务窗体模板。 必须创建一个应用程序页并将代码添加到其中。<br />-   工作流的 Elements.xml 文件未重构。<br />-   有关详细信息，请参阅[工作流任务窗体 (SharePoint Foundation)](/previous-versions/office/developer/sharepoint-2010/ms438856(v=office.14))|-   [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中没有 InfoPath 任务窗体模板。<br />-   [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 和 InfoPath 设计器之间没有集成。<br />-   工作流的 Elements.xml 文件未重构。|
|修改|-   [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中没有可用的 ASPX 修改窗体模板。 若要添加修改窗体，必须创建应用程序页并将代码添加到其中。<br />-   工作流的 Elements.xml 文件未重构。 必须根据需要手动对其进行编辑。<br />-   有关详细信息，请参阅[工作流修改窗体 (SharePoint Foundation)](/previous-versions/office/developer/sharepoint-2010/ms480794(v=office.14))|-   [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中没有 InfoPath 修改窗体模板。<br />-   [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 和 InfoPath 设计器之间没有集成。<br />-   工作流的 Elements.xml 文件未重构。|

## <a name="form-support-in-imported-sharepoint-reusable-workflows"></a>导入的 SharePoint 可重用的工作流中的窗体支持
 下表列出了对 SharePoint 可重用工作流（导入到 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中）中的 ASPX 或 InfoPath 窗体上的不同窗体类型的 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 支持。

|窗体类型|具有从 SharePoint 设计器导入的 ASPX 窗体的可重用工作流|具有从 SharePoint 设计器导入的 InfoPath 窗体的可重用工作流|
|---------------|-------------------------------------------------------------------------------| - |
|关联|-   窗体是在工作流的 Elements.xml 文件中引用的。<br />-   当重命名或删除窗体，或者当窗体的部署路径发生更改时，将重构工作流的 Elements.xml 文件。|-   窗体是在工作流的 Elements.xml 文件中导入的，而不是在其中引用的。<br />-   工作流的 Elements.xml 文件未重构。|
|启动|-   窗体由工作流的 Elements.xml 文件中的工作流引用。<br />-   当重命名或删除窗体，或者当窗体的部署路径发生更改时，将重构工作流的 Elements.xml 文件。|-   窗体是在工作流的 Elements.xml 中导入的，而不是在其中引用的。<br />-   工作流的 Elements.xml 文件未重构。 注意：若要运行此方案，必须添加和更改该方案的规则和属性。|
|任务|-   窗体是在工作流的 Elements.xml 文件中引用的。<br />-   工作流的 Elements.xml 文件未重构。|-   窗体是在工作流的 Elements.xml 中导入的，而不是在其中引用的。<br />-   工作流的 Elements.xml 文件未重构。 注意：若要运行此方案，必须添加和更改该方案的规则和属性。|
|修改|不适用。 无法在 SharePoint 设计器中创建 ASPX 修改窗体。|不适用。 无法在 SharePoint 设计器中创建 InfoPath 修改窗体，内置 SharePoint 服务器工作流除外，导出工作流时，该工作流不包含在 .wsp 文件中。|

## <a name="see-also"></a>另请参阅
- [演练：使用关联和启动窗体创建工作流](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)
- [创建 SharePoint 工作流解决方案](../sharepoint/creating-sharepoint-workflow-solutions.md)
- [从现有的 SharePoint 网站导入项](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)

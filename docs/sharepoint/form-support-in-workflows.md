---
title: 工作流中的窗体|Microsoft Docs
description: 了解工作流中的表单SharePoint支持。 工作流中可以使用四种类型的窗体：关联、启动、任务和修改。
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
ms.openlocfilehash: 1f755943b643d945f70f71707a01aacce2cf534574623e5b96e2e2543149243c
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121269192"
---
# <a name="form-support-in-workflows"></a>工作流中的窗体支持
  工作流中可以使用四种类型的窗体：关联、启动、任务和修改。 这些窗体类型可以基于 ASPX 窗体或 InfoPath 窗体。 为特定窗体 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 提供的支持级别取决于下表中所述的几个因素。 有关工作流窗体类型详细信息，请参阅 [工作流窗体概述](/previous-versions/office/developer/sharepoint-2010/ms457061(v=office.14))。

## <a name="xml-refactoring"></a>XML 重构
 将 ASPX 关联或启动窗体添加到工作流项目项时，在工作流的Elements.xml文件中自动重构 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] XML，使引用关联或启动窗体的属性在更新窗体名称或部署路径或删除窗体时保持同步。 但是，在工作流中使用其他窗体类型（如任务或修改窗体） *时* ，Elements.xml文件不会重构。

## <a name="form-support-in-new-visual-studio-workflows"></a>新工作流中的窗体Visual Studio支持
 下表列出了在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中创建的工作流中对 ASPX 或 InfoPath 窗体上不同窗体类型的支持 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。

|窗体类型|使用 ASPX Visual Studio中创建的工作流|使用 InfoPath Visual Studio在 Visual Studio 中创建的工作流|
|---------------|---------------------------------------------------------|-----------------------------------------------------------------|
|关联|- 可以使用工作流关联窗体项模板将 ASPX 关联 **窗体** 添加到工作流。<br />- *Elements.xml、* 重命名或删除窗体时，或者当其部署路径更改时，将重构工作流的配置文件。<br />- 有关详细信息，请参阅 [演练：使用关联和启动窗体 创建工作流](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)。|- 中没有 InfoPath 关联窗体模板 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。<br />- 和 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] InfoPath 设计器之间没有集成。<br />- *Elements.xml* 重构工作流的配置文件。|
|启动|- 可以使用工作流启动窗体项模板将 ASPX 启动 **窗体** 添加到工作流。<br />- *Elements.xml、* 重命名或删除窗体时，或者当其部署路径更改时，将重构工作流的配置文件。<br />- 有关详细信息，请参阅 [演练：使用关联和启动窗体 创建工作流](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)。|- 中没有 InfoPath 关联窗体模板 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。<br />- 和 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] InfoPath 设计器之间没有集成。<br />- *Elements.xml* 重构工作流的配置文件。|
|任务|- 中未提供 ASPX 任务窗体模板 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。 必须创建应用程序页并添加代码。<br />- *Elements.xml* 重构工作流的配置文件。<br />- 有关详细信息，请参阅[工作流任务窗体 (SharePoint Foundation) ](/previous-versions/office/developer/sharepoint-2010/ms438856(v=office.14))|- 中没有任何 InfoPath 任务窗体模板 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。<br />- 和 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] InfoPath 设计器之间没有集成。<br />- *Elements.xml* 重构工作流的配置文件。|
|修改|- 中未提供 ASPX 修改表单模板 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。 若要添加修改窗体，必须创建应用程序页并添加代码。<br />- *Elements.xml* 重构工作流的配置文件。 必须适当地手动编辑它。<br />- 有关详细信息，请参阅工作流[修改窗体 (SharePoint Foundation) ](/previous-versions/office/developer/sharepoint-2010/ms480794(v=office.14))|- 中没有 InfoPath 修改窗体模板 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。<br />- 和 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] InfoPath 设计器之间没有集成。<br />- *Elements.xml* 重构工作流的配置文件。|

## <a name="form-support-in-imported-sharepoint-reusable-workflows"></a>导入的可重用工作流SharePoint窗体支持
 下表列出了对 ASPX 或 InfoPath 窗体中不同窗体SharePoint导入到 的可重用 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 工作流的支持 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。

|窗体类型|从设计器导入 ASPX 窗体的可重用SharePoint工作流|从设计器导入 InfoPath 窗体的可重用SharePoint工作流|
|---------------|-------------------------------------------------------------------------------| - |
|关联|- 在工作流的 *Elements.xml文件中引用* 窗体。<br />- *Elements.xml* 窗体重命名或删除时，或者当其部署路径更改时，将重构工作流的配置文件。|- 导入窗体，但不在工作流 *Elements.xml引用。*<br />- *Elements.xml* 重构工作流的配置文件。|
|启动|- 该窗体由工作流的Elements.xml *文件中工作流* 引用。<br />- *Elements.xml* 窗体重命名或删除时，或者当其部署路径更改时，将重构工作流的配置文件。|- 导入窗体，但不在工作流 *Elements.xml引用。*<br />- *Elements.xml* 重构工作流的配置文件。 **注意：**  必须添加和更改规则和属性，使此方案正常工作。|
|任务|- 在工作流的 *Elements.xml文件中引用* 窗体。<br />- *Elements.xml* 重构工作流的配置文件。|- 导入窗体，但不在工作流 *Elements.xml引用。*<br />- *Elements.xml* 重构工作流的配置文件。 **注意：**  必须添加和更改规则和属性，使此方案正常工作。|
|修改|不适用。 无法在设计器中创建 ASPX SharePoint窗体。|不适用。 InfoPath 修改窗体不能在 SharePoint 设计器中创建，但内置的 SharePoint Server 工作流除外，在导出工作流时，该工作流不包含在 .wsp 文件中。|

## <a name="see-also"></a>另请参阅
- [演练：使用关联和启动窗体创建工作流](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)
- [创建 SharePoint 工作流解决方案](../sharepoint/creating-sharepoint-workflow-solutions.md)
- [从现有的 SharePoint 网站导入项](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)

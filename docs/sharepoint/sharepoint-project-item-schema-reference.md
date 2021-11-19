---
title: SharePoint 项目项架构参考 | Microsoft Docs
description: 请参阅 SharePoint 项目项 XML 架构参考概述 (ProjectItemModelSchema.xsd)，此架构用于验证 .spdata 文件的内容。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- FeatureProperty element
- SafeControls element
- SafeControl element
- .spdata files
- ExtensionData element
- FeatureProperties element
- ProjectOutputFile element
- Files element
- ProjectItemFolder element
- ProjectItemFile element
- ExtensionDataItem element
- ProjectItem element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 5dbeefe02cf917ac03aeb558acdb5c609543952e
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126663824"
---
# <a name="sharepoint-project-item-schema-reference"></a>SharePoint 项目项架构参考
  Visual Studio 使用 SharePoint 项目项架构来验证 .spdata 文件内容。 .spdata 文件指定 SharePoint 项目项的内容和行为。 有关 SharePoint 项目项的详细信息，请参阅[为 SharePoint 项目项创建项模板和项目模板](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)。

 SharePoint 项目项架构名为 ProjectItemModelSchema.xsd，默认情况下安装在 %Program Files (x86)%\Microsoft Visual Studio 11.0\Xml\Schemas 中。

 根元素为 [ProjectItem](../sharepoint/projectitem-element.md) 元素。 下表描述了架构定义的所有元素。

|元素|说明|
|-------------|-----------------|
|[ExtensionData](../sharepoint/extensiondata-element.md)|表示与 SharePoint 项目项关联的自定义数据项的集合。|
|[ExtensionDataItem](../sharepoint/extensiondataitem-element.md)|表示与 SharePoint 项目项关联的自定义数据项（采用键/值格式）。 键和值都必须为字符串。|
|[FeatureProperties](../sharepoint/featureproperties-element.md)|表示在部署到 SharePoint 时包含在 Feature 中的属性值集合。 部署 Feature 后，可在代码中访问属性值。|
|[FeatureProperty](../sharepoint/featureproperty-element.md)|表示在部署到 SharePoint 时包含在 Feature 中的自定义属性。 部署 Feature 后，可在代码中访问属性。|
|[文件](../sharepoint/files-element.md)|指定要与 SharePoint 项目项一起部署的文件，例如 Feature 元素文件或项目输出。|
|[ProjectItem](../sharepoint/projectitem-element.md)|表示 SharePoint 项目项。|
|[ProjectItemFile](../sharepoint/projectitemfile-element.md)|表示在部署到 SharePoint 时要包含在项目项中的 SharePoint 文件，如 Feature 元素文件。|
|[ProjectItemFolder](../sharepoint/projectitemfolder-element.md)|表示映射的文件夹。|
|[ProjectOutputFile](../sharepoint/projectoutputfile-element.md)|表示在部署到 SharePoint 时要包含在项目项中的项目的输出。|
|[SafeControl](../sharepoint/safecontrol-element.md)|表示 ASPX 控件或 Web 部件，指定为可供任何用户在 SharePoint 站点上的任何 ASPX 页面上安全访问。|
|[SafeControls](../sharepoint/safecontrols-element.md)|表示 ASPX 控件和 Web 部件集合，这些控件和对象被指定为可供任何用户在 SharePoint 站点的任何 ASPX 页面上安全访问。|

## <a name="see-also"></a>另请参阅
- [为 SharePoint 项目项创建项模板和项目模板](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)

---
title: SharePoint Project项架构参考|Microsoft Docs
description: 请参阅 ProjectItemModelSchema.xs) d SharePoint项目项 XML 架构参考 (概述，该引用用于验证 .spdata 文件的内容。
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
# <a name="sharepoint-project-item-schema-reference"></a>SharePoint项目项架构引用
  Visual Studio项目SharePoint架构来验证 *.spdata 文件* 的内容。 *.spdata* 文件指定项目项SharePoint和行为。 有关项目项SharePoint的详细信息，请参阅为项目项 创建SharePoint[模板](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)。

 SharePoint项目项架构名为 ProjectItemModelSchema.xsd，默认情况下安装在 %Program Files (x86) %\Microsoft Visual Studio 11.0\Xml\Schemas 中。

 根元素是 [ProjectItem](../sharepoint/projectitem-element.md) 元素。 下表描述了架构定义的所有元素。

|元素|说明|
|-------------|-----------------|
|[ExtensionData](../sharepoint/extensiondata-element.md)|表示与项目项关联的自定义数据SharePoint的集合。|
|[ExtensionDataItem](../sharepoint/extensiondataitem-element.md)|表示与项目项关联的自定义数据SharePoint键/值格式。 键和值都必须是字符串。|
|[FeatureProperties](../sharepoint/featureproperties-element.md)|表示一个属性值集合，这些属性值包含在功能部署到 SharePoint。 部署功能后，可以访问代码中的属性值。|
|[FeatureProperty](../sharepoint/featureproperty-element.md)|表示一个自定义属性，该属性在部署到功能时随功能SharePoint。 部署功能后，可以访问代码中的 属性。|
|[文件](../sharepoint/files-element.md)|指定要与项目SharePoint一起部署的文件，例如 Feature 元素文件或项目的输出。|
|[ProjectItem](../sharepoint/projectitem-element.md)|表示SharePoint项。|
|[ProjectItemFile](../sharepoint/projectitemfile-element.md)|表示SharePoint项目项时要与项目项一起包含的一个SharePoint。|
|[ProjectItemFolder](../sharepoint/projectitemfolder-element.md)|表示映射的文件夹。|
|[ProjectOutputFile](../sharepoint/projectoutputfile-element.md)|表示将项目项部署到项目项时要包含的项目SharePoint。|
|[SafeControl](../sharepoint/safecontrol-element.md)|表示一个 ASPX 控件或 Web 部件，该控件或 Web 部件被指定为安全，任何用户都有权访问该站点的任何 ASPX SharePoint页。|
|[SafeControls](../sharepoint/safecontrols-element.md)|表示 ASPX 控件和Web 部件集合，这些控件和对象被指定为安全，任何用户都有权访问 SharePoint 站点上的任何 ASPX 页。|

## <a name="see-also"></a>另请参阅
- [为项目项创建项模板SharePoint模板](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)

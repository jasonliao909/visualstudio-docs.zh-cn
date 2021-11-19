---
title: ProjectItemFile 元素 | Microsoft Docs
description: 获取有关 ProjectItemFile 元素的参考信息，该元素表示 SharePoint 项目项 XML 架构参考中的项目项文件。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ProjectItemFile element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 065bb202420549462597ccea7cece0a3c3485c4b
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664778"
---
# <a name="projectitemfile-element"></a>ProjectItemFile 元素
  表示在部署到 SharePoint 时要包含在项目项中的 SharePoint 文件，如 Feature 元素文件。

## <a name="syntax"></a>语法

```xml
<ProjectItemFile Source = "Name of the file"
    Target = "Deployment path of the file"
    Type = "Type of deployment for the file" />
```

## <a name="type"></a>类型
 ProjectItemFileType

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|属性|说明|
|---------------|-----------------|
|**Source**|必需的 xs:string 属性。<br /><br /> 要与项目项一起部署的文件名称。|
|**Target**|可选 xs:string 属性。<br /><br /> 文件将在 SharePoint 上部署的路径与部署根文件夹相关。 部署根文件夹由“类型”属性指定的部署类型决定。 如果未指定“目标”属性，那么文件将部署到在“源”属性中指定其名称的文件夹中。 <br /><br /> 有关详细信息，请参阅[开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)中 SharePoint 项目项的“部署路径”和“部署根”属性的说明。|
|类型|必需的 xs:string 属性。<br /><br /> 文件的部署类型。 有关可能值的详细信息，请参阅[开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)中 SharePoint 项目项的“部署类型”属性的说明。|

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[文件](../sharepoint/files-element.md)|指定在部署到 SharePoint 时要包含在 SharePoint 项目项中的文件。|

## <a name="remarks"></a>备注
 ProjectItemFile 元素中通常引用的 SharePoint 文件包含“功能”元素文件 (Elements.xml)、列表定义的架构文件 (Schema.xml) 和 Web 部件的“Web 部件”定义文件 (.webpart)。

## <a name="element-information"></a>元素信息

|属性|值|
|-|-|
|**Namespace**|http:\/\/schemas.microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|
|**架构名称**|SharePoint 项目项架构|
|验证文件|ProjectItemModelSchema.xsd|
|可为空|否|

## <a name="see-also"></a>另请参阅
- [SharePoint 项目项架构参考](../sharepoint/sharepoint-project-item-schema-reference.md)

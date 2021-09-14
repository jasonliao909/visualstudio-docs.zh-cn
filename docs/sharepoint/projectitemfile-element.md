---
title: ProjectItemFile 元素|Microsoft Docs
description: 获取有关 ProjectItemFile 元素的参考信息，该元素表示项目项 XML 架构SharePoint中的项目项文件。
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
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664778"
---
# <a name="projectitemfile-element"></a>ProjectItemFile 元素
  表示SharePoint项目项时要包含的一个属性文件，例如 Feature 元素SharePoint。

## <a name="syntax"></a>语法

```xml
<ProjectItemFile Source = "Name of the file"
    Target = "Deployment path of the file"
    Type = "Type of deployment for the file" />
```

## <a name="type"></a>类型
 **ProjectItemFileType**

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|属性|说明|
|---------------|-----------------|
|**Source**|必需的 **xs：string** 属性。<br /><br /> 要与项目项一起部署的文件的名称。|
|**Target**|可选的 **xs：string** 属性。<br /><br /> 文件将部署在 SharePoint相对于部署根文件夹的路径。 部署根文件夹由 Type 属性指定的部署 **类型** 确定。 如果 **未指定 Target** 属性，则文件将部署到具有 Source 属性中指定名称 **的文件夹** 。<br /><br /> 有关详细信息，请参阅开发解决方案 中的项目SharePoint部署路径和部署SharePoint[属性的说明](../sharepoint/developing-sharepoint-solutions.md)。|
|类型|必需的 **xs：string** 属性。<br /><br /> 文件的部署类型。 有关可能值的更多信息，请参阅开发解决方案中的SharePoint项目项的部署[SharePoint说明](../sharepoint/developing-sharepoint-solutions.md)。|

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[文件](../sharepoint/files-element.md)|指定在项目项SharePoint项目项时要包含的文件SharePoint。|

## <a name="remarks"></a>备注
 **SharePoint ProjectItemFile** 元素中引用的 SharePoint 文件包括 Feature 元素文件 (*Elements.xml*) 、列表定义 (*Schema.xml*) 的架构文件和 Web 部件 (*.webpart*) 的 Web 部件定义文件。

## <a name="element-information"></a>元素信息

|Property|值|
|-|-|
|**Namespace**|\/ \/ http：schemas.microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|
|**架构名称**|SharePoint Project项架构|
|**验证文件**|ProjectItemModelSchema.xsd|
|**可以为空**|否|

## <a name="see-also"></a>另请参阅
- [SharePoint项目项架构引用](../sharepoint/sharepoint-project-item-schema-reference.md)

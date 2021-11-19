---
title: Files 元素|Microsoft Docs
description: 查看有关 Files 元素的参考信息，该元素是项目SharePoint架构中的元素。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Files element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 84c3ab0837680fe815f644d6b0456ce0fe066326
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600643"
---
# <a name="files-element"></a>Files 元素
  指定要与项目SharePoint一起部署的文件，例如 Feature 元素文件和依赖的非SharePoint的输出。

## <a name="syntax"></a>语法

```xml
<Files>
  <ProjectItemFile.../>
  <ProjectOutputFile.../>
</Files>
```

## <a name="type"></a>类型
 **FileCollectionType**

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性
 无。

### <a name="child-elements"></a>子元素

|元素|说明|
|-------------|-----------------|
|[ProjectItemFile](../sharepoint/projectitemfile-element.md)|可选的 **ProjectItemFileType** 元素。<br /><br /> 表示SharePoint项目项时要与项目项一起包含的一个SharePoint。|
|[ProjectOutputFile](../sharepoint/projectoutputfile-element.md)|可选的 **ProjectOutputFileType** 元素。<br /><br /> 表示将项目项部署到项目项时要包含的项目SharePoint。|

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[ProjectItem](../sharepoint/projectitem-element.md)|表示SharePoint项。 此元素是文件必需的根 `.spdata` 元素。|

## <a name="element-information"></a>元素信息

|属性|值|
|-|-|
|**Namespace**|\/ \/ http：schemas.microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|
|**架构名称**|SharePoint Project项架构|
|**验证文件**|ProjectItemModelSchema.xsd|
|**可以为空**|否|

## <a name="see-also"></a>另请参阅
- [SharePoint项目项架构引用](../sharepoint/sharepoint-project-item-schema-reference.md)

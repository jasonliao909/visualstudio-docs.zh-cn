---
title: ProjectItemFolder 元素|Microsoft Docs
description: 获取有关 ProjectItemFolder 元素的参考信息，该元素表示项目SharePoint XML 架构引用中的映射文件夹。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ProjectItemFolder element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 3873a4cbf50d216f3574c2ef8ce90255d3eb5d7b
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664777"
---
# <a name="projectitemfolder-element"></a>ProjectItemFolder 元素
  表示映射的文件夹。

## <a name="syntax"></a>语法

```xml
<ProjectItemFolder Target = "Path of SharePoint folder the mapped folder corresponds to"
    Type = "Type of deployment for the mapped folder" />
```

## <a name="type"></a>类型
 **ProjectItemFolderType**

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|属性|说明|
|---------------|-----------------|
|**Target**|必需的 **xs：字符串** 属性。<br /><br /> 映射文件夹所对应的SharePoint文件夹相对于部署根文件夹的安装路径。 部署根文件夹由 Type 属性指定的部署 **类型** 确定。<br /><br /> 有关详细信息，请参阅开发解决方案 中的项目SharePoint部署路径和部署SharePoint[属性的说明](../sharepoint/developing-sharepoint-solutions.md)。|
|类型|必需的 **xs：string** 属性。<br /><br /> 映射文件夹的部署类型。 有关可能值的更多信息，请参阅开发解决方案 中的SharePoint项的部署[SharePoint说明](../sharepoint/developing-sharepoint-solutions.md)。|

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[ProjectItem](../sharepoint/projectitem-element.md)|表示SharePoint项。 此元素是 *.spdata* 文件所需的根元素。|

## <a name="remarks"></a>备注
 有关映射文件夹的信息，请参阅 [如何：添加和删除映射的文件夹](../sharepoint/how-to-add-and-remove-mapped-folders.md)。

## <a name="element-information"></a>元素信息

|属性|值|
|-|-|
|**Namespace**|\/ \/ http：schemas.microsoft.com/VisualStudio/2010/<br>SharePointTools/SharePointProjectItemModel|
|**架构名称**|SharePoint Project项架构|
|**验证文件**|ProjectItemModelSchema.xsd|
|**可以为空**|否|

## <a name="see-also"></a>另请参阅
- [SharePoint项目项架构引用](../sharepoint/sharepoint-project-item-schema-reference.md)
- [如何：添加和删除映射的文件夹](../sharepoint/how-to-add-and-remove-mapped-folders.md)

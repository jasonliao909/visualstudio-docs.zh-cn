---
title: ExtensionDataItem 元素 | Microsoft Docs
description: 查看有关 ExtensionDataItem 元素的参考信息，该元素是 SharePoint 项目项架构中的一个元素。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ExtensionDataItem element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: b99d9a267b8fb18ec8e238191382d71f558fc3d3
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600655"
---
# <a name="extensiondataitem-element"></a>ExtensionDataItem 元素
  与 SharePoint 项目项关联的自定义数据项，采用键/值格式。 键和值都必须为字符串。

## <a name="syntax"></a>语法

```xml
<ExtensionDataItem Key = "Key of the data item"
    Value = "Value of the data item" />
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|属性|说明|
|---------------|-----------------|
|**键**|必需的 xs: string 属性。<br /><br /> 用于存储和检索数据项的键。|
|值|必需的 xs:string 属性。<br /><br /> 数据项的值。|

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[ExtensionData](../sharepoint/extensiondata-element.md)|表示与 SharePoint 项目项关联的自定义数据项的集合。|

## <a name="remarks"></a>备注
 使用 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem> 对象的 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A> 属性将自定义数据与 SharePoint 项目项关联时，Visual Studio 会将数据保存到项目项的 `.spdata` 文件中的新 ExtensionDataItem 元素。 有关详细信息，请参阅[在 SharePoint 项目系统的扩展中保存数据](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)。

## <a name="element-information"></a>元素信息

|属性|值|
|-|-|
|**Namespace**|http:\/\/schemas.microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|
|**架构名称**|SharePoint 项目项架构|
|**验证文件**|ProjectItemModelSchema.xsd|
|**可为空**|否|

## <a name="see-also"></a>另请参阅
- [SharePoint 项目项架构参考](../sharepoint/sharepoint-project-item-schema-reference.md)

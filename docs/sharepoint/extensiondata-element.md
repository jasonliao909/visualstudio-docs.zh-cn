---
title: ExtensionData 元素|Microsoft Docs
description: 查看有关 ExtensionData 元素的参考信息，该元素是项目SharePoint架构中的元素。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ExtensionData element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: ec317073601f766dab2042ab6c77542914e87b59
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600656"
---
# <a name="extensiondata-element"></a>ExtensionData 元素
  表示与项目项关联的自定义数据SharePoint的集合。

## <a name="syntax"></a>语法

```xml
<ExtensionData>
  <ExtensionDataItem.../>
</ExtensionData>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性
 无。

### <a name="child-elements"></a>子元素

|元素|说明|
|-------------|-----------------|
|[ExtensionDataItem](../sharepoint/extensiondataitem-element.md)|可选元素。<br /><br /> 表示与项目项关联的自定义数据SharePoint键/值格式。 键和值都必须是字符串。|

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[ProjectItem](../sharepoint/projectitem-element.md)|表示SharePoint项。 此元素是文件必需的根 `.spdata` 元素。|

## <a name="remarks"></a>备注
 使用 对象的 属性SharePoint自定义数据与项目项关联时，Visual Studio将数据保存到项目项的 文件的 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem> **ExtensionData** `.spdata` 元素。 有关详细信息，请参阅[将数据保存在项目系统的](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)扩展SharePoint中。

## <a name="element-information"></a>元素信息

|Property|值|
|-|-|
|**Namespace**|\/ \/ http：schemas.microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|
|**架构名称**|SharePoint Project项架构|
|**验证文件**|ProjectItemModelSchema.xsd|
|**可以为空**|否|

## <a name="see-also"></a>另请参阅
- [SharePoint项目项架构引用](../sharepoint/sharepoint-project-item-schema-reference.md)

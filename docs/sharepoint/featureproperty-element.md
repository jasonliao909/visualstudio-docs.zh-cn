---
title: FeatureProperty 元素|Microsoft Docs
description: 查看有关 FeatureProperty 元素的参考信息，该元素是项目SharePoint架构中的元素。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- FeatureProperty element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 01536094bdb9fd084b32ce56429d085f5f377f8f
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600644"
---
# <a name="featureproperty-element"></a>FeatureProperty 元素
  表示一个自定义属性，该属性在部署到功能时随功能SharePoint。 部署功能后，可以访问代码中的 属性。

## <a name="syntax"></a>语法

```xml
<FeatureProperty Key = "Key of the property value"
    Value = "Property value" />
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|属性|说明|
|---------------|-----------------|
|**键**|必需的 **xs：string** 属性。<br /><br /> 用于存储和检索属性值的键。 每个属性必须具有在功能中唯一的键。|
|**值**|必需的 **xs：string** 属性。<br /><br /> 属性值。|

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[FeatureProperties](../sharepoint/featureproperties-element.md)|表示一个属性值集合，这些属性值在部署到功能时随功能SharePoint。|

## <a name="remarks"></a>备注
 有关功能属性详细信息，请参阅 [在项目项 中提供包和部署信息](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)。

## <a name="element-information"></a>元素信息

|Property|值|
|-|-|
|**Namespace**|\/ \/ http：schemas.microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|
|**架构名称**|SharePoint Project项架构|
|**验证文件**|ProjectItemModelSchema.xsd|
|**可以为空**|否|

## <a name="see-also"></a>另请参阅
- [SharePoint项目项架构引用](../sharepoint/sharepoint-project-item-schema-reference.md)
- [在项目项中提供打包和部署信息](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)

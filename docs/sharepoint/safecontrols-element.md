---
title: SafeControls 元素 | Microsoft Docs
description: 了解有关 SafeControls 元素的信息，该元素包含 ASPX 控件或 Web 部件的集合，被标记为可在 SharePoint 站点的 ASPX 页面上安全访问。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SafeControls element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 063da0761f15c1a3b39468a810fd5d3055cece62
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602535"
---
# <a name="safecontrols-element"></a>SafeControls 元素
  ASPX 控件和 Web 部件集合，这些控件和对象被指定为可供任何用户在 SharePoint 站点的任何 ASPX 页面上安全访问。

## <a name="syntax"></a>语法

```xml
<SafeControls>
  <SafeControl.../>
</SafeControls>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性
 无。

### <a name="child-elements"></a>子元素

|元素|说明|
|-------------|-----------------|
|[SafeControl](../sharepoint/safecontrol-element.md)|可选元素。<br /><br /> 表示 ASPX 控件或 Web 部件，被指定为可供任何用户在 SharePoint 站点上的任何 ASPX 页面上安全访问。|

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[ProjectItem](../sharepoint/projectitem-element.md)|表示 SharePoint 项目项。 此元素是 .spdata 文件必需的根元素。|

## <a name="remarks"></a>备注
 有关安全控件的详细信息，请参阅[在项目项中提供打包和部署信息](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)。

## <a name="element-information"></a>元素信息

|属性|值|
|-|-|
|**Namespace**|http:\/\/schemas.microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|
|**架构名称**|SharePoint 项目项架构|
|**验证文件**|ProjectItemModelSchema.xsd|
|**可为空**|否|

## <a name="see-also"></a>另请参阅
- [SharePoint 项目项架构参考](../sharepoint/sharepoint-project-item-schema-reference.md)
- [在项目项中提供打包和部署信息](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)

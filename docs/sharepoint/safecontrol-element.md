---
title: SafeControl 元素 |Microsoft Docs
description: 获取有关 SafeControl 元素的信息，该元素表示一个被标记为 "安全" 的 aspx 控件或 web 部件，以便用户在 SharePoint 站点的 ASPX 页上访问。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SafeControl element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 04db1be46cbc2ff3830b00f9c3866e2859485a6f755514ea28333cada757190d
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121244168"
---
# <a name="safecontrol-element"></a>SafeControl 元素
  表示一个 ASPX 控件或 Web 部件，它被指定为在 SharePoint 站点上的任何 ASPX 页上访问的安全。

## <a name="syntax"></a>语法

```xml
<SafeControl Assembly = "Name of assembly that contains the safe control"
    IsSafe = "true/false"
    IsSafeAgainstScript = "true/false"
    Name = "Name of this safe control entry"
    Namespace = "Namespace of the safe control"
    TypeName = "Type of the safe control" />
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|属性|说明|
|---------------|-----------------|
|**程序集**|可选 **xs： string** 特性。<br /><br /> 其中定义了 ASPX 控件或 Web 部件的程序集的名称。 默认情况下，此属性使用 **$ SharePoint Project。** 程序集名称的 AssemblyFullName $ 可替换参数。 有关详细信息，请参阅[可替换参数](../sharepoint/replaceable-parameters.md)。|
|**IsSafe**|可选 **xs： boolean** 属性。<br /><br /> 指定 ASPX 控件或 Web 部件对于不受信任的用户的访问是安全的。|
|**IsSafeAgainstScript**|可选 **xs： boolean** 属性。<br /><br /> 指定不受信任的用户是否可以查看或编辑 ASPX 控件或 Web 部件的属性。|
|**名称**|可选 **xs： string** 特性。<br /><br /> 此安全控件项在集合中的名称。|
|**命名空间**|可选 **xs： string** 特性。<br /><br /> ASPX 控件或 Web 部件的命名空间。|
|**TypeName**|可选 **xs： string** 特性。<br /><br /> ASPX 控件或 Web 部件的类型名称。|

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[SafeControls](../sharepoint/safecontrols-element.md)|表示 ASPX 控件和 Web 部件的集合，这些控件和在 SharePoint 站点上的任何 ASPX 页上被指定为安全以供任何用户访问。|

## <a name="remarks"></a>备注
 有关安全控件的详细信息，请参阅 [在项目项中提供打包和部署信息](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)。

## <a name="element-information"></a>元素信息

|属性|值|
|-|-|
|**Namespace**|http： \/ \/ schemas.microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|
|**架构名称**|SharePoint Project 项架构|
|**验证文件**|ProjectItemModelSchema|
|**可以为空**|否|

## <a name="see-also"></a>另请参阅
- [SharePoint 项目项架构参考](../sharepoint/sharepoint-project-item-schema-reference.md)
- [在项目项中提供打包和部署信息](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)

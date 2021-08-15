---
title: 项目项元素 |Microsoft Docs
description: 获取有关项目项元素的参考信息，该元素表示 SharePoint 项目项 XML 架构引用中的 SharePoint 项目项。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ProjectItem element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: da3645e6d8a0f8ae7568aa1e68a3ccf114a4f96f56bb25350a26f6c0dd0b7931
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121367468"
---
# <a name="projectitem-element"></a>ProjectItem 元素
  表示 SharePoint 项目项。 此元素是 *spdata* 文件必需的根元素。

## <a name="syntax"></a>语法

```xml
<ProjectItem DefaultFile = "File that opens in the editor when you open the project item"
    FeatureReceiverClass = "Class that implements a feature receiver for the project item"
    FeatureReceiverAssembly = "Assembly that defines a feature receiver for the project item"
    SupportedTrustLevels = "Trust levels that the project item supports"
    SupportedDeploymentScopes = "Deployment scopes that the project item supports"
    Type="Identifier for the project item">
  <Files>...</Files>
  <ProjectItemFolder>...</ProjectItemFolder>
  <SafeControls>...</SafeControls>
  <FeatureProperties>...</FeatureProperties>
  <ExtensionData>...</ExtensionData>
</ProjectItem>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|属性|说明|
|---------------|-----------------|
|**DefaultFile**|可选 **xs： string** 特性。<br /><br /> 在 **解决方案资源管理器** 打开 SharePoint 项目项时，在 Visual Studio 编辑器中打开的文件的相对路径（包括文件名）。 路径相对于包含 *spdata* 文件的文件夹。|
|**FeatureReceiverClass**|可选 **xs： string** 特性。<br /><br /> 此 SharePoint 项目项的功能接收器类的完全限定名称。 有关功能接收器的详细信息，请参阅 [在项目项中提供打包和部署信息](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)。|
|**FeatureReceiverAssembly**|可选 **xs： string** 特性。<br /><br /> 指定一个程序集的完全限定名称，该程序集定义此 SharePoint 项目项的功能接收器。 有关功能接收器的详细信息，请参阅 [在项目项中提供打包和部署信息](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)。 有关完全限定的程序集名称的详细信息，请参阅 [程序集名称](/dotnet/framework/app-domains/assembly-names)。|
|**SupportedTrustLevels**|可选 **xs： string** 特性。<br /><br /> 指定此 SharePoint 项目项支持的信任级别。 此值可以为以下字符串之一：沙盒、FullTrust 或 All。 值 All 同时指定沙盒和 FullTrust。<br /><br /> 在自定义 SharePoint 项目项类型中，此特性的值对应于你在实现方法时分配给该属性的值 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition.SupportedTrustLevels%2A> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A> 。 如果为此属性指定一个不同的值，Visual Studio 将覆盖值，以便它指定在属性中指定的相同信任级别 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition.SupportedTrustLevels%2A> 。|
|**SupportedDeploymentScopes**|可选 **xs： string** 特性。<br /><br /> 指定此 SharePoint 项目项支持的部署范围。 此值是一个以逗号分隔的字符串，其中包含一个或多个以下字符串：场、站点、Web、WebApplication 或包。 例如：`Web, Site`<br /><br /> 在自定义 SharePoint 项目项类型中，此特性的值对应于你在实现方法时分配给该属性的值 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition.SupportedDeploymentScopes%2A> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A> 。 如果为此属性指定一个不同的值，Visual Studio 将覆盖值，以便它指定在属性中指定的相同信任级别 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition.SupportedDeploymentScopes%2A> 。|
|**类型**|必需的 **xs： string** 特性。<br /><br /> SharePoint 项目项的标识符。 在自定义 SharePoint 项目项类型中，标识符是传递到的字符串 <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute> 。 有关详细信息，请参阅[如何：定义 SharePoint 项目项类型](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)。<br /><br /> 有关 Visual Studio 附带的内置 SharePoint 项目项的标识符列表，请参阅[扩展 SharePoint 项目项](../sharepoint/extending-sharepoint-project-items.md)。|

### <a name="child-elements"></a>子元素

|元素|说明|
|-------------|-----------------|
|[ExtensionData](../sharepoint/extensiondata-element.md)|可选元素。<br /><br /> 表示与 SharePoint 项目项关联的自定义数据项的集合。<br /><br /> 只能包含一个 **ExtensionData** 元素。|
|[FeatureProperties](../sharepoint/featureproperties-element.md)|可选元素。<br /><br /> 表示在将某个功能部署到 SharePoint 时包含的属性值的集合。<br /><br /> 只能包含一个 **FeatureProperties** 元素。|
|[文件](../sharepoint/files-element.md)|可选的 **FileCollectionType** 元素。<br /><br /> 指定要与 SharePoint 项目项一起部署的文件，例如功能元素文件和依赖非 SharePoint 项目的输出。<br /><br /> 包括 **文件** 或 **ProjectItemFolder** 元素，但不能同时包含两者。|
|[ProjectItemFolder](../sharepoint/projectitemfolder-element.md)|可选的 **ProjectItemFolderType** 元素。<br /><br /> 表示映射文件夹。<br /><br /> 包括 **文件** 或 **ProjectItemFolder** 元素，但不能同时包含两者。|
|[SafeControls](../sharepoint/safecontrols-element.md)|可选元素。<br /><br /> 表示 ASPX 控件和 Web 部件的集合，这些控件和在 SharePoint 站点上的任何 ASPX 页上被指定为安全以供任何用户访问。<br /><br /> 只能包含一个 **SafeControls** 元素。|

### <a name="parent-elements"></a>父元素
 无。

## <a name="element-information"></a>元素信息

|属性|值|
|-|-|
|**Namespace**|http： \/ \/ schemas.microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|
|**架构名称**|SharePoint Project 项架构|
|**验证文件**|ProjectItemModelSchema|
|**可以为空**|否|

## <a name="see-also"></a>另请参阅
[SharePoint 项目项架构 rseference](../sharepoint/sharepoint-project-item-schema-reference.md)

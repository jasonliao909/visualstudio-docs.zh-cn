---
title: ProjectItem 元素|Microsoft Docs
description: 获取有关 ProjectItem 元素的参考信息，该元素表示SharePoint项目项 XML 架构引用SharePoint项目项。
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
ms.openlocfilehash: e755df78078e4fc601cd4a596813d6acd71eb781
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122084189"
---
# <a name="projectitem-element"></a>ProjectItem 元素
  表示SharePoint项。 此元素是 *.spdata* 文件所需的根元素。

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
|**DefaultFile**|可选 **xs：字符串** 属性。<br /><br /> 在 中打开项目项目项时，在 Visual Studio 编辑器中打开的文件的相对路径 **SharePoint文件名** 解决方案资源管理器。 路径相对于包含 *.spdata* 文件的文件夹。|
|**FeatureReceiverClass**|可选的 **xs：string** 属性。<br /><br /> 此对象项目项的功能接收器类的SharePoint名称。 有关功能接收器详细信息，请参阅 [在项目项 中提供打包和部署信息](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)。|
|**FeatureReceiverAssembly**|可选的 **xs：string** 属性。<br /><br /> 指定程序集的完全限定名称，该程序集定义此项目项SharePoint接收者。 有关功能接收器详细信息，请参阅 [在项目项 中提供打包和部署信息](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)。 有关完全限定程序集名称的信息，请参阅 [程序集名称](/dotnet/framework/app-domains/assembly-names)。|
|**SupportedTrustLevels**|可选的 **xs：string** 属性。<br /><br /> 指定此项目项SharePoint信任级别。 此值可以是以下字符串之一：Sandboxed、FullTrust 或 All。 值 All 同时指定 Sandboxed 和 FullTrust。<br /><br /> 在自定义SharePoint项类型中，此属性的值对应于在 方法的实现 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition.SupportedTrustLevels%2A> 中分配给 属性 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A> 的值。 如果为此特性指定了其他值，则Visual Studio覆盖该值，以便它指定在 属性中指定的相同信任 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition.SupportedTrustLevels%2A> 级别。|
|**SupportedDeploymentScopes**|可选的 **xs：string** 属性。<br /><br /> 指定此项目项支持的SharePoint范围。 此值是一个逗号分隔字符串，由以下一个或多个字符串组成：场、站点、Web、WebApplication 或 Package。 例如：`Web, Site`<br /><br /> 在自定义SharePoint项类型中，此属性的值对应于在 方法的实现 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition.SupportedDeploymentScopes%2A> 中分配给 属性 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A> 的值。 如果为此特性指定了其他值，则Visual Studio覆盖该值，以便它指定在 属性中指定的相同信任 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition.SupportedDeploymentScopes%2A> 级别。|
|**类型**|必需的 **xs：string** 属性。<br /><br /> 项目项SharePoint标识符。 在自定义SharePoint项类型中，标识符是传递给 的字符串 <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute> 。 有关详细信息，请参阅[如何：定义SharePoint项目项类型](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)。<br /><br /> 有关内置项目项的标识符列表SharePoint包含Visual Studio，请参阅扩展SharePoint[项目项](../sharepoint/extending-sharepoint-project-items.md)。|

### <a name="child-elements"></a>子元素

|元素|说明|
|-------------|-----------------|
|[ExtensionData](../sharepoint/extensiondata-element.md)|可选元素。<br /><br /> 表示与项目项关联的自定义数据SharePoint的集合。<br /><br /> 只能包含一个 **ExtensionData** 元素。|
|[FeatureProperties](../sharepoint/featureproperties-element.md)|可选元素。<br /><br /> 表示一个属性值集合，这些属性值包含在功能部署到 SharePoint。<br /><br /> 只能包含一个 **FeatureProperties** 元素。|
|[文件](../sharepoint/files-element.md)|可选的 **FileCollectionType** 元素。<br /><br /> 指定要与项目SharePoint一起部署的文件，例如 Feature 元素文件和依赖的非SharePoint的输出。<br /><br /> 包括 **Files** 或 **ProjectItemFolder 元素** ，但不能同时包含这两者。|
|[ProjectItemFolder](../sharepoint/projectitemfolder-element.md)|可选的 **ProjectItemFolderType** 元素。<br /><br /> 表示映射的文件夹。<br /><br /> 包括 **Files** 或 **ProjectItemFolder 元素** ，但不能同时包含这两者。|
|[SafeControls](../sharepoint/safecontrols-element.md)|可选元素。<br /><br /> 表示 ASPX 控件和Web 部件集合，这些控件和对象被指定为安全，任何用户都有权访问 SharePoint 站点上的任何 ASPX 页。<br /><br /> 只能包含一个 **SafeControls** 元素。|

### <a name="parent-elements"></a>父元素
 无。

## <a name="element-information"></a>元素信息

|属性|值|
|-|-|
|**Namespace**|\/ \/ http：schemas.microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|
|**架构名称**|SharePoint Project项架构|
|**验证文件**|ProjectItemModelSchema.xsd|
|**可以为空**|否|

## <a name="see-also"></a>另请参阅
[SharePoint项目项架构 rseference](../sharepoint/sharepoint-project-item-schema-reference.md)

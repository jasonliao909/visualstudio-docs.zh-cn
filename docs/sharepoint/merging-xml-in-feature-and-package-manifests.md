---
title: 合并功能和包清单中的 XML | Microsoft Docs
description: 在 SharePoint 功能和包清单中合并由设计器生成且由用户添加的 XML 代码。 了解功能和包清单元素，以及合并异常。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, packaging
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 1e2150995946039bef9dbb4d77c64f8bbb33bf8f
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122156287"
---
# <a name="merge-xml-in-feature-and-package-manifests"></a>合并功能和包清单中的 XML
  功能和包由 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 清单文件定义。 这些打包的清单由设计器生成数据和用户在清单模板中输入的自定义 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 组合而成。 在打包时，[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将自定义的 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 语句与设计器提供的 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 合并，以便组成打包的 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 清单文件。 类似的元素与稍后在“合并异常”中说明的异常合并，以避免在将文件部署到 SharePoint 后出现 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 验证错误，还可以使清单文件更小且更高效。

## <a name="modify-the-manifests"></a>修改清单
 在禁用功能或包设计器之前，无法直接修改打包的清单文件。 但是，可以通过功能和包设计器或 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 编辑器手动将自定义 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 元素添加到清单模板中。 有关详细信息，请参阅[如何：自定义 SharePoint 功能](../sharepoint/how-to-customize-a-sharepoint-feature.md)和[如何：自定义 SharePoint 解决方案包](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)。

## <a name="feature-and-package-manifest-merge-process"></a>功能清单和包清单合并过程
 将自定义元素与设计器提供的元素组合在一起时，[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 使用以下过程。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 检查每个元素是否都具有唯一键值。 如果元素没有唯一的键值，则会将其追加到打包的清单文件。 同样，具有多个键的元素也无法合并。 因此，它们将被追加到清单文件。

 如果元素具有唯一键，[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 会将设计器的值和自定义键的值进行比较。 如果值匹配，则它们合并为单个值。 如果值不同，则放弃设计器键值，并使用自定义键值。 集合也会合并。 例如，如果设计器生成的 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 和自定义的 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 都包含“程序集”集合，则打包的清单仅包含一个“程序集”集合。

## <a name="merge-exceptions"></a>合并异常
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将大多数设计器 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 元素与类似的自定义 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 元素合并（只要它们具有单个唯一的标识数据）。 但是，某些元素缺少 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 合并所需的唯一标识符。 这些元素称为合并异常。 在这些情况下，[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 不会将自定义 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 元素与设计器提供的 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 元素合并在一起，而是将它们追加到打包的清单文件中。

 以下是功能和包 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 清单文件的合并异常列表。

|设计器|XML 元素|
|--------------|-----------------|
|功能设计器|ActivationDependency|
|功能设计器|UpgradeAction|
|包设计器|SafeControl|
|包设计器|CodeAccessSecurity|

## <a name="feature-manifest-elements"></a>功能清单元素
 下表列出了可合并的所有功能清单元素及其用于匹配的唯一键。

|元素名称|唯一键|
|------------------|----------------|
|功能（所有属性）|“属性名称”（“功能”元素的每个属性名称都是唯一键。）|
|ElementFile|位置|
|ElementManifests/ElementManifest|位置|
|Properties/Property|密钥|
|CustomUpgradeAction|名称|
|CustomUpgradeActionParameter|名称|

> [!NOTE]
> 由于修改 CustomUpgradeAction 元素的唯一方法位于自定义 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 编辑器中，因此不合并的效率较低。

## <a name="package-manifest-elements"></a>包清单元素
 下表列出了可合并的所有包清单元素及其用于匹配的唯一键。

|元素名称|唯一键|
|------------------|----------------|
|解决方案（所有属性）|“属性名称”（“解决方案”元素的每个属性名称都是唯一键。）|
|ApplicationResourceFiles/ApplicationResourceFile|位置|
|Assemblies/Assembly|位置|
|ClassResources/ClassResource|位置|
|DwpFiles/DwpFile|位置|
|FeatureManifests/FeatureManifest|位置|
|Resources/Resource|位置|
|RootFiles/RootFile|位置|
|SiteDefinitionManifests/SiteDefinitionManifest|位置|
|WebTempFile|位置|
|TemplateFiles/TemplateFile|位置|
|SolutionDependency|SolutionID|

## <a name="manually-add-deployed-files"></a>手动添加已部署的文件
 某些清单元素（如 ApplicationResourceFile 和 DwpFiles）指定包含文件名的位置。 但是，将文件名条目添加到清单模板不会将基础文件添加到包。 必须将文件添加到项目以将其包括在包中，并相应地设置其“部署类型”属性。

## <a name="see-also"></a>另请参阅
- [打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
- [生成和调试 SharePoint 解决方案](../sharepoint/building-and-debugging-sharepoint-solutions.md)

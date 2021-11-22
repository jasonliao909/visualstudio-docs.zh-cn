---
title: SharePoint 支持的 MSBuild 属性 | Microsoft Docs
description: 阅读 SharePoint 支持和特定于 SharePoint 的 MSBuild 属性名称和说明的列表。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, MSBuild properties
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 66024105ac41c6c72d7eec019d507183fdd7479a
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122115546"
---
# <a name="msbuild-properties-supported-by-sharepoint"></a>SharePoint 支持的 MSBuild 属性
  可以在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] SharePoint 项目中使用在 Microsoft.VisualStudio.SharePoint.targets 文件、项目文件或项目用户文件中定义的任何 [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] 属性。 除了项目提供的公共 [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] 属性以外，SharePoint 还定义了特定于 SharePoint 项目的其他属性。

 有关通用 [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] 属性的列表，请参阅[通用 MSBuild 项目属性](/previous-versions/dotnet/netframework-4.0/bb629394(v=vs.100))。 有关编程语言支持的属性的完整列表，请查看 .targets 文件、项目文件（.csproj 或 .vbproj），或项目用户文件（csproj.user 或 .vbproj.user）。

## <a name="msbuild-properties-specific-to-sharepoint"></a>特定于 SharePoint 的 MsBuild 属性
 下表列出了专门适用于 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中 SharePoint 项目的 [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] 属性。 存在其他属性，但它们供内部使用。

|属性名称|说明|
|-------------------|-----------------|
|SharePointSiteUrl|表示指向 SharePoint 站点的 [!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)] 的字符串。|
|SandboxedSolution|指示解决方案是否为沙盒解决方案的布尔值。|
|ActiveDeploymentConfiguration|活动部署配置|
|IncludeAssemblyInPackage|指示程序集是否包含在包文件中的布尔值。|
|PreDeploymentCommand|一个字符串值，该值表示要在部署前命令步骤中执行的命令。|
|PreDeploymentCommand|一个字符串值，该值表示要在部署后命令步骤中执行的命令。|
|CustomBeforeSharePointTargets|表示 [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] 目标文件的路径的字符串。 如果目标文件存在并且已定义，则表示它已在任何 SharePoint 目标数据之前导入。 此属性使你可以通过预定义与打包相关的属性来自定义包过程，而无需修改交付的 SharePoint 目标文件，但目标文件仍适用于所有 SharePoint 项目。|
|CustomAfterSharePointTargets|表示 [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] 目标文件的路径的字符串。 如果目标文件存在并且已定义，则表示它在所有 SharePoint 目标数据之后导入。 借助此属性，你可以通过重写与打包相关的属性和目标来自定义包过程，而不必修改交付的 SharePoint 目标文件，但目标文件仍适用于所有 SharePoint 项目。|
|LayoutPath|一个字符串，表示在将每个要打包的文件添加到 .wsp 文件之前临时放置的根目录。 当你重写 BeforeLayout 和 AfterLayout 目标以便添加、删除或修改要打包的文件时，了解此路径可能有所帮助，因为你可以使用它来更改 .wsp 文件的内容。|
|BasePackagePath|一个字符串，表示在其中放置包的文件夹。 此值使用项目的输出目录，例如 Bin\debug。|
|PackageExtension|一个字符串，表示要追加到包的文件扩展名。 默认值为 wsp。|
|AssemblyDeploymentTarget|一个字符串，表示项目程序集在 SharePoint 服务器上的部署位置。 其值为 GlobalAssemblyCache（默认）或 WebApplication。 还可以在“属性”窗口中设置此属性。|
|PackageWithValidation|一个布尔值，指定在打包之前是否执行验证。 此属性可让你在生成包时忽略验证错误。|
|ValidatePackageDependsOn|一个字符串，定义要在 ValidatePackage 目标之前执行的其他目标。|
|TokenReplacementFileExensions|一个字符串，用于定义打包期间替换其标记的文件。|

## <a name="use-msbuild-properties-in-the-properties-page"></a>在“属性”页中使用 MsBuild 属性
 出于灵活性考虑，你可以使用 SharePoint 属性作为参数，而不是使用“SharePoint 属性”页上的“部署前命令行”和“部署后命令行”框中的硬编码字符串。 例如，与其为 SharePoint 站点指定特定的 [!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)] 字符串，不如改用 `$(SharePointSiteUrl)`。

> [!NOTE]
> 可以使用 [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] 变量语法 `$(` propertyName`)` 或环境变量语法 `%`propertyName`%` 来指定属性。

## <a name="see-also"></a>另请参阅

- [MSBuild 参考](../msbuild/msbuild-reference.md)
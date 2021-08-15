---
title: MSBuild支持的属性SharePoint |Microsoft Docs
description: 阅读特定于MSBuild 和 支持的属性名称和说明的列表SharePoint。
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
ms.openlocfilehash: a0d180dae17ac6e905fa5eedf6bef27e41f3d96661e25474f791bac3d08d5cbd
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121331983"
---
# <a name="msbuild-properties-supported-by-sharepoint"></a>项目支持的 MsBuild SharePoint
  Microsoft.VisualStudio.SharePoint.targets 文件、项目文件或项目用户文件中定义的任何属性都可用于SharePoint [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 项目。 除了项目提供的常见属性，SharePoint定义特定于项目 [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] 的其他SharePoint属性。

 有关常见属性 [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] 的列表，请参阅[Common MSBuild Project Properties](/previous-versions/dotnet/netframework-4.0/bb629394(v=vs.100))。 有关编程语言支持的属性的完整列表，请查找 *.targets* 文件、项目文件 (*.csproj* 或 *.vbproj*) ，或项目用户文件 (*csproj.user* 或 *.vbproj.user*) 。

## <a name="msbuild-properties-specific-to-sharepoint"></a>特定于属性的 MsBuild SharePoint
 下表列出了专用于 [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] 中的项目SharePoint属性 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。 存在其他属性，但它们供内部使用。

|属性名称|说明|
|-------------------|-----------------|
|SharePointSiteUrl|一个字符串，表示SharePoint [!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)] 站点。|
|SandboxedSolution|一个布尔值，指示解决方案是否是沙盒解决方案。|
|ActiveDeploymentConfiguration|活动部署配置。|
|IncludeAssemblyInPackage|一个布尔值，指示程序集是否包含在包文件中。|
|PreDeploymentCommand|一个字符串值，表示在部署前命令步骤中执行的命令。|
|PostDeploymentCommand|一个字符串值，该值表示在部署后命令步骤中执行的命令。|
|CustomBeforeSharePointTargets|一个表示目标文件路径 [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] 的字符串。 如果目标文件存在且已定义，则在任何目标文件以数据SharePoint该文件。 使用此属性，无需修改附带的 SharePoint 目标文件即可预定义与打包相关的属性，以自定义包过程，但目标文件仍适用于所有SharePoint项目。|
|CustomAfterSharePointTargets|一个表示目标文件路径 [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] 的字符串。 如果目标文件存在且已定义，则在所有目标文件以数据SharePoint该文件。 此属性允许通过重写与打包相关的属性和目标来自定义包过程，而无需修改附带的 SharePoint 目标文件，但目标文件仍应用于所有SharePoint项目。|
|LayoutPath|一个字符串，表示要打包的每个文件在添加到 *.wsp* 文件之前临时放置的根目录。 此路径可用于了解何时重写 BeforeLayout 和 AfterLayout 目标以添加、删除或修改要打包的文件，因为可以使用它来更改 *.wsp* 文件的内容。|
|BasePackagePath|一个字符串，表示放置包的文件夹。 此值使用项目的输出目录，例如 Bin\Debug。|
|PackageExtension|一个字符串，表示要追加到包的文件扩展名。 默认值为 wsp。|
|AssemblyDeploymentTarget|一个字符串，表示项目程序集部署在 SharePoint 服务器上的位置。 其值为 GlobalAssemblyCache (默认值) WebApplication。 此属性还可以在 属性窗口 中设置。|
|PackageWithValidation|一个布尔值，指定是否在打包之前执行验证。 此属性允许你在生成包时忽略验证错误。|
|ValidatePackageDependsOn|一个字符串，定义在 ValidatePackage 目标之前要执行的其他目标。|
|TokenReplacementFileExensions|一个字符串，用于定义在打包过程中替换其令牌的文件。|

## <a name="use-msbuild-properties-in-the-properties-page"></a>在属性页使用 MsBuild 属性
 为灵活地使用 SharePoint 属性页上的"预部署命令行"和"部署后命令行"框中的硬编码字符串，可以使用 SharePoint 属性作为参数。 例如，可以改为使用 ，而不是为SharePoint [!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)] 指定特定字符串 `$(SharePointSiteUrl)` 。

> [!NOTE]
> 可以使用变量语法 [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] `$(` *propertyName* `)` 或环境变量语法 `%` *propertyName* `%` 来指定属性。

## <a name="see-also"></a>另请参阅

- [MSBuild 参考](../msbuild/msbuild-reference.md)
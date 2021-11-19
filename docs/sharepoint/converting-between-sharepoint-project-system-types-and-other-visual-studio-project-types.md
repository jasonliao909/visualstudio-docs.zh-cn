---
title: 转换：SharePoint项目系统类型与其他类型相互转换
titleSuffix: ''
description: 在项目SharePoint类型和其他项目类型Visual Studio转换。 查看一个列表，该列表详细说明了可转换的类型。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint project service
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: c6624295dfb43a15a9ae2235b15a658de4eea76d
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602316"
---
# <a name="convert-between-sharepoint-project-system-types-and-other-visual-studio-project-types"></a>在项目SharePoint类型与其他项目类型Visual Studio转换
  在某些情况下，你可能在 SharePoint 项目中有一个对象，并且想要在 Visual Studio 自动化对象模型或集成对象模型中使用相应对象的功能，反之亦然。 在这些情况下，可以使用对象的 方法 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService.Convert%2A> SharePoint 项目服务对象转换为其他对象模型。

 例如，你可能有一个 对象，但你想要使用仅在 或 对象 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject> 上 <xref:EnvDTE.Project> 可用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject> 的方法。 在这种情况下，可以使用 方法 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService.Convert%2A> 将 转换为 或 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject> <xref:EnvDTE.Project> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject> 。

 有关自动化对象模型Visual Studio集成对象模型Visual Studio，请参阅 SharePoint[工具扩展的编程模型概述](../sharepoint/overview-of-the-programming-model-of-sharepoint-tools-extensions.md)。

## <a name="types-of-conversions"></a>转换类型
 下表列出了此方法可以在项目系统和其他对象模型SharePoint转换Visual Studio类型。

|SharePoint项目系统类型|自动化和集成对象模型中的相应类型|
|------------------------------------|-------------------------------------------------------------------------|
|<xref:Microsoft.VisualStudio.SharePoint.ISharePointProject>|<xref:EnvDTE.Project><br /><br /> 或<br /><br /> 项目中的任何接口Visual Studio由项目的基础 COM 对象实现的集成对象模型。 这些接口包括 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject> 、 (或派生接口) 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> 。 有关由项目实现的主要接口的列表，请参阅 Project[模型核心组件](../extensibility/internals/project-model-core-components.md)。|
|<xref:Microsoft.VisualStudio.SharePoint.IMappedFolder><br /><br /> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem><br /><br /> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemFile><br /><br /> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectFeature><br /><br /> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectFeatureResourceFile><br /><br /> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectPackage>|<xref:EnvDTE.ProjectItem><br /><br /> 或<br /><br /> 值 <xref:System.UInt32> (一个 VSITEMID) ，用于标识包含它的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 中的项目成员。 此值可以传递给某些 *方法的 itemid* <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 参数。|

## <a name="example"></a>示例
 下面的代码示例演示如何使用 方法将 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService.Convert%2A> 对象 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject> 转换为 <xref:EnvDTE.Project> 。

:::code language="csharp" source="../sharepoint/codesnippet/CSharp/spprojectserviceaddin/connect.cs" id="Snippet2":::
:::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spprojectserviceaddin/connect.vb" id="Snippet2":::

 此示例需要：

- 具有对SharePoint程序集的引用的EnvDTE.dll *扩展。* 有关详细信息，请参阅[扩展 SharePoint 项目系统](../sharepoint/extending-the-sharepoint-project-system.md)。

- 注册 方法以处理 `projectService_ProjectAdded` 对象 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectAdded> 事件 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService> 的代码。 有关示例，请参阅[如何：创建SharePoint扩展。](../sharepoint/how-to-create-a-sharepoint-project-extension.md)

## <a name="see-also"></a>另请参阅

- [使用SharePoint 项目服务](../sharepoint/using-the-sharepoint-project-service.md)
- [如何：检索SharePoint 项目服务](../sharepoint/how-to-retrieve-the-sharepoint-project-service.md)
- [SharePoint 工具扩展的编程模型概述](../sharepoint/overview-of-the-programming-model-of-sharepoint-tools-extensions.md)

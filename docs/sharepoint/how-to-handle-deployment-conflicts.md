---
title: 如何：处理部署冲突 |Microsoft Docs
description: 查看一个示例，了解如何实现自己的代码来处理 SharePoint 项目项的部署冲突。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
helpviewer_keywords:
- SharePoint development in Visual Studio, extending deployment
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 4f5e6bbf7326b768e0f6cd0fe48e6501e5ad0b4efca2ece75a0df5b781c0a6fa
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121352911"
---
# <a name="how-to-handle-deployment-conflicts"></a>如何：处理部署冲突
  你可以提供自己的代码来处理 SharePoint 项目项的部署冲突。 例如，你可能确定当前项目项中的任何文件是否已存在于部署位置，然后在部署当前项目项之前删除已部署的文件。 有关部署冲突的详细信息，请参阅[扩展 SharePoint 打包和部署](../sharepoint/extending-sharepoint-packaging-and-deployment.md)。

### <a name="to-handle-a-deployment-conflict"></a>处理部署冲突

1. 创建项目项扩展、项目扩展或新项目项类型的定义。 有关详细信息，请参阅以下主题：

    - [如何：创建 SharePoint 项目项扩展](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)

    - [如何：创建 SharePoint 项目扩展](../sharepoint/how-to-create-a-sharepoint-project-extension.md)

    - [如何：定义 SharePoint 项目项类型](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)

2. 在扩展中，处理 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepStarted> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemType> 项目项扩展或项目扩展) 的对象的事件，或在 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition> 新项目项类型) 的定义中 (对象 (。

3. 在事件处理程序中，根据应用于方案的条件，确定正在部署的项目项与 SharePoint 站点上部署的解决方案之间是否存在冲突。 您可以使用 <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemEventArgs.ProjectItem%2A> 事件参数参数的属性来分析正在部署的项目项，还可以通过调用为此目的定义的 SharePoint 命令，在部署位置分析文件。

     对于许多类型的冲突，你可能首先需要确定正在执行的部署步骤。 可以通过使用事件参数参数的属性来执行此操作 <xref:Microsoft.VisualStudio.SharePoint.DeploymentStepStartedEventArgs.DeploymentStepInfo%2A> 。 尽管在内置部署步骤中检测冲突通常很有意义 <xref:Microsoft.VisualStudio.SharePoint.Deployment.DeploymentStepIds.AddSolution> ，但你可以在任何部署步骤中检查冲突。

4. 如果存在冲突，则使用 <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentConflictCollection.Add%2A> <xref:Microsoft.VisualStudio.SharePoint.DeploymentStepStartedEventArgs.Conflicts%2A> 事件参数的属性的方法来创建新的 <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentConflict> 对象。 此对象表示部署冲突。 在对方法的调用中 <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentConflictCollection.Add%2A> ，还应指定用于解决冲突的方法。

## <a name="example"></a>示例
 下面的代码示例演示了在项目项扩展中处理列表定义项目项的部署冲突的基本过程。 若要处理其他类型的项目项的部署冲突，请将不同的字符串传递给 <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute> 。 有关详细信息，请参阅[扩展 SharePoint 项目项](../sharepoint/extending-sharepoint-project-items.md)。

 为简单起见， <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepStarted> 此示例中的事件处理程序假设存在部署冲突 (也就是说，它始终向添加一个新的 <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentConflict> 对象) ， `Resolve` 方法只返回 **true** 以指示冲突已解决。 在实际情况下， <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepStarted> 事件处理程序首先确定当前项目项中的文件与部署位置的文件之间是否存在冲突，然后 <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentConflict> 仅在存在冲突时添加对象。 例如，你可以使用 `e.ProjectItem.Files` 事件处理程序中的属性分析项目项中的文件，并且可以调用 SharePoint 命令来分析部署位置的文件。 同样，在实际情况下，该 `Resolve` 方法可能调用 SharePoint 命令来解决 SharePoint 网站上的冲突。 有关创建 SharePoint 命令的详细信息，请参阅[如何：创建 SharePoint 命令](../sharepoint/how-to-create-a-sharepoint-command.md)。

 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/deploymentconflict/extension/deploymentconflictextension.vb" id="Snippet1":::
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/deploymentconflict/extension/deploymentconflictextension.cs" id="Snippet1":::

## <a name="compile-the-code"></a>编译代码
 此示例需要引用以下程序集：

- VisualStudio。SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>部署扩展
 若要部署该扩展，请为 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 该程序集创建一个扩展 (VSIX) 包，并为您要使用该扩展分发的任何其他文件创建该扩展。 有关详细信息，请参阅[Visual Studio 中的 SharePoint 工具的部署扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>请参阅
- [扩展 SharePoint 打包和部署](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
- [扩展 SharePoint 项目项](../sharepoint/extending-sharepoint-project-items.md)
- [如何：在执行部署步骤时运行代码](../sharepoint/how-to-run-code-when-deployment-steps-are-executed.md)
- [如何：创建 SharePoint 命令](../sharepoint/how-to-create-a-sharepoint-command.md)

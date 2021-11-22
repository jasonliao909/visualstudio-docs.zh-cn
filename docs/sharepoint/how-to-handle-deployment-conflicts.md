---
title: 如何：处理部署冲突 | Microsoft Docs
description: 请参阅示例了解如何实施自己的代码以便为 SharePoint 项目项处理部署冲突。
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
ms.openlocfilehash: 8da6e8bd908466b8314ab9ff6cf3e9d998644a77
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664159"
---
# <a name="how-to-handle-deployment-conflicts"></a>如何：处理部署冲突
  可以提供自己的代码以便为 SharePoint 项目项处理部署冲突。 例如，可以确定当前项目项中的任何文件是否已存在部署位置中，然后在部署当前项目项志群删除已部署的文件。 有关部署冲突的详细信息，请参阅[扩展 SharePoint 打包和部署](../sharepoint/extending-sharepoint-packaging-and-deployment.md)。

### <a name="to-handle-a-deployment-conflict"></a>若要处理部署冲突

1. 创建项目项扩展、项目扩展或新项目项类型的定义。 有关详细信息，请参阅以下主题：

    - [如何：创建 SharePoint 项目项扩展](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)

    - [如何：创建 SharePoint 项目扩展](../sharepoint/how-to-create-a-sharepoint-project-extension.md)

    - [如何：定义 SharePoint 项目项类型](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)

2. 在扩展中，处理 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemType> 对象（项目项扩展或项目扩展中）或 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition> 对象（新的项目项类型的定义中）的 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepStarted> 事件。

3. 在事件处理程序中，根据应用到方案的条件，确定正在部署的项目项和 SharePoint 站点上的已部署解决方案之间是否存在冲突。 可以使用事件自变量参数的 <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemEventArgs.ProjectItem%2A> 属性来分析正在部署的项目项，还可以通过调用为此目的定义的 SharePoint 命令来分析部署位置的文件。

     对于多种类型的冲突，首先可能需要确定正在执行的部署步骤。 可以使用事件自变量参数的 <xref:Microsoft.VisualStudio.SharePoint.DeploymentStepStartedEventArgs.DeploymentStepInfo%2A> 属性来执行此操作。 虽然在内置 <xref:Microsoft.VisualStudio.SharePoint.Deployment.DeploymentStepIds.AddSolution> 部署步骤中删除冲突尤其起效，但是可以在任意部署步骤中检查冲突。

4. 如果存在冲突，则使用事件自变量的 <xref:Microsoft.VisualStudio.SharePoint.DeploymentStepStartedEventArgs.Conflicts%2A> 属性的 <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentConflictCollection.Add%2A> 方法来创建新的 <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentConflict> 对象。 该对象表示部署冲突。 在调用 <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentConflictCollection.Add%2A> 方法时，还指定调用来解决冲突的方法。

## <a name="example"></a>示例
 下面的代码示例演示了为列表定义项目项处理项目项扩展中的部署冲突的基本流程。 若要为不同类型的项目项处理部署冲突，请将不同的字符串传递到 <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute>。 有关详细信息，请参阅[扩展 SharePoint 项目项](../sharepoint/extending-sharepoint-project-items.md)。

 简单起见，本示例中的 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepStarted> 事件处理程序假设存在部署冲突（即，它始终添加新的 <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentConflict> 对象），且 `Resolve` 简单返回 true 以指示冲突已解决。 在真实方案中，<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepStarted> 事件处理程序会首先确定当前项目项中的文件和部署位置的文件之间是否存在冲突，只有存在冲突时才会添加 <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentConflict> 对象。 例如，可能在事件处理程序中使用 `e.ProjectItem.Files` 属性来分析项目项中的文件，还可能调用 SharePoint 命令来分析部署位置的文件。 同样，在真实方案中，`Resolve` 方法可能会调用 SharePoint 命令来解决 SharePoint 站点上的冲突。 有关创建 SharePoint 命令的详细信息，请参阅[如何：创建 SharePoint 命令](../sharepoint/how-to-create-a-sharepoint-command.md)。

 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/deploymentconflict/extension/deploymentconflictextension.vb" id="Snippet1":::
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/deploymentconflict/extension/deploymentconflictextension.cs" id="Snippet1":::

## <a name="compile-the-code"></a>编译代码
 本示例需要引用以下程序集：

- Microsoft.VisualStudio.SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>部署扩展
 若要部署扩展，请为程序集以及要随扩展分发的任何其他文件创建 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 扩展 (VSIX) 包。 有关详细信息，请参阅[在 Visual Studio 中部署 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>另请参阅
- [扩展 SharePoint 打包和部署](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
- [扩展 SharePoint 项目项](../sharepoint/extending-sharepoint-project-items.md)
- [如何：在执行部署步骤时运行代码](../sharepoint/how-to-run-code-when-deployment-steps-are-executed.md)
- [操作说明：创建 SharePoint 命令](../sharepoint/how-to-create-a-sharepoint-command.md)

---
title: 如何：处理部署|Microsoft Docs
description: 请参阅一个示例，了解如何实现自己的代码来处理项目项的SharePoint冲突。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122047694"
---
# <a name="how-to-handle-deployment-conflicts"></a>如何：处理部署冲突
  可以提供自己的代码来处理项目项的SharePoint冲突。 例如，可以确定部署位置中当前项目项中是否存在任何文件，然后在部署当前项目项之前删除已部署的文件。 有关部署冲突的信息，请参阅[扩展SharePoint打包和部署](../sharepoint/extending-sharepoint-packaging-and-deployment.md)。

### <a name="to-handle-a-deployment-conflict"></a>处理部署冲突

1. 创建项目项扩展、项目扩展或新项目项类型的定义。 有关详细信息，请参阅以下主题：

    - [如何：创建SharePoint项目项扩展](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)

    - [如何：创建SharePoint扩展](../sharepoint/how-to-create-a-sharepoint-project-extension.md)

    - [如何：定义SharePoint项类型](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)

2. 在扩展中，处理 (项目项扩展或项目扩展) 或 (项目项类型定义中的对象 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepStarted> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemType> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition>) 。

3. 在事件处理程序中，根据适用于方案的条件，确定正在部署的项目项与 SharePoint 站点上部署的解决方案之间是否发生冲突。 可以使用事件参数参数的 属性来分析正在部署的项目项，并且可以通过调用为此目的定义的 SharePoint 命令来分析部署位置的文件。 <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemEventArgs.ProjectItem%2A>

     对于多种类型的冲突，可能首先需要确定正在执行的部署步骤。 为此，可以使用事件 <xref:Microsoft.VisualStudio.SharePoint.DeploymentStepStartedEventArgs.DeploymentStepInfo%2A> 参数参数的 属性。 尽管在内置部署步骤中检测冲突通常有意义，但可以在任何部署步骤中 <xref:Microsoft.VisualStudio.SharePoint.Deployment.DeploymentStepIds.AddSolution> 检查冲突。

4. 如果存在冲突，请使用 <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentConflictCollection.Add%2A> 事件参数 <xref:Microsoft.VisualStudio.SharePoint.DeploymentStepStartedEventArgs.Conflicts%2A> 的 属性的 方法来创建新 <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentConflict> 对象。 此对象表示部署冲突。 在调用 方法 <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentConflictCollection.Add%2A> 时，还指定调用以解决冲突的方法。

## <a name="example"></a>示例
 下面的代码示例演示了处理列表定义项目项的项目项扩展中的部署冲突的基本过程。 若要处理不同类型的项目项的部署冲突，请向 传递其他字符串 <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute> 。 有关详细信息，请参阅[扩展SharePoint项目项](../sharepoint/extending-sharepoint-project-items.md)。

 为简单起见，此示例中的事件处理程序假定存在部署冲突 (也就是说，它始终添加新对象) ，并且 方法仅返回 true 以指示冲突已 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepStarted> <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentConflict> `Resolve` 解决。 在真实方案中，事件处理程序将首先确定当前项目项中的文件与部署位置的文件之间是否存在冲突，然后仅在存在冲突时添加 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepStarted> <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentConflict> 对象。 例如，可以使用事件处理程序中的 属性分析项目项中的文件，并且可以调用 SharePoint 命令来分析部署位置 `e.ProjectItem.Files` 的文件。 同样，在真实方案中， `Resolve` 方法可能会调用 SharePoint 命令来解决该站点SharePoint冲突。 有关创建命令SharePoint，请参阅[如何：创建SharePoint命令](../sharepoint/how-to-create-a-sharepoint-command.md)。

 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/deploymentconflict/extension/deploymentconflictextension.vb" id="Snippet1":::
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/deploymentconflict/extension/deploymentconflictextension.cs" id="Snippet1":::

## <a name="compile-the-code"></a>编译代码
 此示例需要引用以下程序集：

- Microsoft.VisualStudio。SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>部署扩展
 若要部署扩展，请为程序集 (VSIX) 包以及要随扩展一起分发的其他任何文件 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 创建扩展。 有关详细信息，请参阅在 Visual Studio 中为 SharePoint[工具部署Visual Studio。](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)

## <a name="see-also"></a>请参阅
- [扩展SharePoint打包和部署](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
- [扩展SharePoint项目项](../sharepoint/extending-sharepoint-project-items.md)
- [如何：执行部署步骤时运行代码](../sharepoint/how-to-run-code-when-deployment-steps-are-executed.md)
- [如何：创建SharePoint命令](../sharepoint/how-to-create-a-sharepoint-command.md)

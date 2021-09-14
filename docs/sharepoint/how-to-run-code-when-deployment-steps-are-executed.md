---
title: 如何：在执行部署步骤时运行|Microsoft Docs
description: 运行代码以处理执行部署步骤之前SharePoint之后由Visual Studio项目项引发的事件。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, extending deployment
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 72e104e25bdb17433e76ee1f52bdf56570afdacf
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665280"
---
# <a name="how-to-run-code-when-deployment-steps-are-executed"></a>如何：执行部署步骤时运行代码
  如果要对 SharePoint 项目中的部署步骤执行其他任务，可以在执行每个部署步骤之前和之后处理 SharePoint 项目项Visual Studio的事件。 有关详细信息，请参阅扩展[SharePoint和部署](../sharepoint/extending-sharepoint-packaging-and-deployment.md)。

### <a name="to-run-code-when-deployment-steps-are-executed"></a>在执行部署步骤时运行代码

1. 创建项目项扩展、项目扩展或新项目项类型的定义。 有关详细信息，请参阅以下主题：

    - [如何：创建SharePoint项目项扩展](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)

    - [如何：创建SharePoint扩展](../sharepoint/how-to-create-a-sharepoint-project-extension.md)

    - [如何：定义SharePoint项类型](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)

2. 在扩展中，处理项目项扩展 (扩展或项目扩展) 或 (项目项类型定义中的对象) 。 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepStarted> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepCompleted> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemType> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition>

3. 在事件处理程序中，使用 <xref:Microsoft.VisualStudio.SharePoint.DeploymentStepStartedEventArgs> 和 <xref:Microsoft.VisualStudio.SharePoint.DeploymentStepCompletedEventArgs> 参数获取有关部署步骤的信息。 例如，可以确定正在执行哪个部署步骤，以及解决方案是部署还是收回。

## <a name="example"></a>示例
 下面的代码示例演示如何在列表实例项目项的扩展中处理 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepStarted> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepCompleted> 和 事件。 此扩展在部署和收回解决方案Visual Studio回收应用程序池时，会将其他消息写入"输出"窗口。

 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/handledeploymentstepevents.vb" id="Snippet4":::
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/handledeploymentstepevents.cs" id="Snippet4":::

## <a name="compile-the-code"></a>编译代码
 此示例需要引用以下程序集：

- Microsoft.VisualStudio。SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>部署扩展
 若要部署扩展，请为程序集 (VSIX) 包以及要随扩展一起分发的其他任何文件 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 创建扩展。 有关详细信息，请参阅 在 SharePoint 中为 Visual Studio[工具部署Visual Studio。](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)

## <a name="see-also"></a>另请参阅
- [扩展SharePoint打包和部署](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
- [演练：为项目创建SharePoint步骤](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)
- [如何：部署或收回SharePoint时运行代码](../sharepoint/how-to-run-code-when-a-sharepoint-project-is-deployed-or-retracted.md)

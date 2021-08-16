---
title: 如何：在执行部署步骤时运行代码 |Microsoft Docs
description: 运行代码，处理 Visual Studio 执行部署步骤之前和之后 SharePoint 项目项引发的事件。
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
ms.openlocfilehash: 7d23b6d2bfdc3cbf619dcad4e96fc4a577bf8f90ec864292cb7aac2b3a2ebf26
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121352885"
---
# <a name="how-to-run-code-when-deployment-steps-are-executed"></a>如何：在执行部署步骤时运行代码
  如果要为 SharePoint 项目中的部署步骤执行其他任务，则可以在 Visual Studio 执行每个部署步骤之前和之后处理 SharePoint 项目项引发的事件。 有关详细信息，请参阅[扩展 SharePoint 打包和部署](../sharepoint/extending-sharepoint-packaging-and-deployment.md)。

### <a name="to-run-code-when-deployment-steps-are-executed"></a>执行部署步骤时运行代码

1. 创建项目项扩展、项目扩展或新项目项类型的定义。 有关详细信息，请参阅以下主题：

    - [如何：创建 SharePoint 项目项扩展](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)

    - [如何：创建 SharePoint 项目扩展](../sharepoint/how-to-create-a-sharepoint-project-extension.md)

    - [如何：定义 SharePoint 项目项类型](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)

2. 在扩展中，处理 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepStarted> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepCompleted> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemType> 项目项扩展或项目扩展中 (的对象的和事件) 或 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition> (在新项目项类型) 定义中的对象。

3. 在事件处理程序中，使用 <xref:Microsoft.VisualStudio.SharePoint.DeploymentStepStartedEventArgs> 和 <xref:Microsoft.VisualStudio.SharePoint.DeploymentStepCompletedEventArgs> 参数获取有关部署步骤的信息。 例如，你可以确定正在执行的部署步骤以及是否正在部署或收回解决方案。

## <a name="example"></a>示例
 下面的代码示例演示如何 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepStarted> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepCompleted> 在列表实例项目项的扩展中处理和事件。 当 Visual Studio 在部署和收回解决方案时回收应用程序池时，此扩展会向 "**输出**" 窗口中写入一条额外的消息。

 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/handledeploymentstepevents.vb" id="Snippet4":::
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/handledeploymentstepevents.cs" id="Snippet4":::

## <a name="compile-the-code"></a>编译代码
 此示例需要引用以下程序集：

- VisualStudio。SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>部署扩展
 若要部署该扩展，请为 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 该程序集创建一个扩展 (VSIX) 包，并为您要使用该扩展分发的任何其他文件创建该扩展。 有关详细信息，请参阅[Visual Studio 中的 SharePoint 工具的部署扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>另请参阅
- [扩展 SharePoint 打包和部署](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
- [演练：为 SharePoint 项目创建自定义部署步骤](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)
- [如何：在部署或收回 SharePoint 项目时运行代码](../sharepoint/how-to-run-code-when-a-sharepoint-project-is-deployed-or-retracted.md)

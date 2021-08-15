---
title: 扩展SharePoint打包和部署|Microsoft Docs
description: 扩展SharePoint和部署。 创建部署步骤和配置。 处理部署冲突。 自定义验证规则。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: eac554fbfb1d7558b7d705e46aba3430fb97171141304e9685d36241872edcff
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121353017"
---
# <a name="extend-sharepoint-packaging-and-deployment"></a>扩展SharePoint打包和部署
  可以扩展 SharePoint 项目的打包和部署过程。

## <a name="create-deployment-steps"></a>创建部署步骤
 部署 SharePoint 项目时，[!INCLUDE[vs_current_short](../sharepoint/includes/vs-current-short-md.md)] 会执行一系列部署步骤。 Visual Studio 包含用于很多任务的内置部署步骤，如收回和添加解决方案。 但是，还可以创建自己的部署步骤。

 有关演示如何创建部署步骤的演练，请参阅演练：为项目[创建自定义SharePoint步骤](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)。

## <a name="create-deployment-configurations"></a>创建部署配置
 部署配置是一组针对给定项目执行，但可能会影响所有 SharePoint 项目项的部署步骤。 每个部署配置都包含一组在部署项目时执行的步骤，以及在收回项目时执行的另一组步骤。 [!INCLUDE[vs_current_short](../sharepoint/includes/vs-current-short-md.md)] 包括两个内置部署配置，但也可以创建自己的部署配置。 创建部署配置时，可以包含内置部署步骤和你创建的部署步骤。

 有关演示如何创建部署配置的演练，请参阅演练：为项目[创建自定义SharePoint步骤](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)。

## <a name="run-code-when-a-sharepoint-solution-is-deployed-or-retracted"></a>部署或收回SharePoint时运行代码
 可以处理事件以在部署或收回 SharePoint 解决方案时执行其他任务。 Visual Studio 会在以下情况下引发你可以处理的事件：

- 为 SharePoint 项目项执行每个部署步骤之前和之后。 有关详细信息，请参阅 [如何：在执行部署步骤时运行代码](../sharepoint/how-to-run-code-when-deployment-steps-are-executed.md)。

- 在部署或收回 SharePoint 项目之前和之后 有关详细信息，请参阅如何：在部署或收回SharePoint[时运行代码](../sharepoint/how-to-run-code-when-a-sharepoint-project-is-deployed-or-retracted.md)。

## <a name="handle-deployment-conflicts"></a>处理部署冲突
 某些类型的 SharePoint 项目项（包括模块、Web 部件、列表实例和内容类型）提供了内置部署冲突解决方法。 部署包含这些项目项之一的解决方案时，Visual Studio 会首先检查 SharePoint 站点上是否已存在与所部署项中的文件具有相同名称、URL 或 ID 的文件。 如果存在冲突，则 Visual Studio 可以自动解决冲突，或者它可以提示你以确定你是要让 Visual Studio 解决冲突还是取消部署。 有关详细信息，请参阅 [Troubleshooting SharePoint Packaging and Deployment](../sharepoint/troubleshooting-sharepoint-packaging-and-deployment.md)。

 可以通过提供自己的检查和解决部署冲突的代码，来扩展此功能。 有关详细信息，请参阅 [如何：处理部署冲突](../sharepoint/how-to-handle-deployment-conflicts.md)。

## <a name="run-command-line-operations-before-or-after-a-project-is-deployed"></a>在部署项目之前或之后运行命令行操作
 如果要在部署 SharePoint 解决方案时运行命令行操作，则可以设置 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject> 对象的 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject.PreDeploymentCommand%2A> 和 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject.PostDeploymentCommand%2A> 属性。 Visual Studio 会在部署项目之前和之后执行这些命令。

 在某些情况下，可能会发生部署冲突。 可通过多种不同的方式来解决冲突。 有关详细信息，请参阅对打包[SharePoint进行故障排除](../sharepoint/troubleshooting-sharepoint-packaging-and-deployment.md)。

## <a name="customize-validation-rules"></a>自定义验证规则
 部署解决方案包 (.wsp) 之前，可以创建自定义功能和包验证规则来验证功能或包是否有效。 例如，可以向开发人员报告信息、警告或错误以帮助他们解决验证问题。 有关详细信息，请参阅[如何：为 SharePoint 解决方案创建自定义功能和包验证规则](../sharepoint/how-to-create-custom-feature-and-package-validation-rules-for-sharepoint-solutions.md)。

## <a name="see-also"></a>另请参阅
- [如何：执行部署步骤时运行代码](../sharepoint/how-to-run-code-when-deployment-steps-are-executed.md)
- [演练：为项目创建SharePoint步骤](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)
- [如何：为解决方案创建自定义功能SharePoint验证规则](../sharepoint/how-to-create-custom-feature-and-package-validation-rules-for-sharepoint-solutions.md)
- [扩展 SharePoint 项目系统](../sharepoint/extending-the-sharepoint-project-system.md)

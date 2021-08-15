---
title: 创建 Workflow Foundation 项目
description: 了解如何使用中提供的项目模板创建库Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 06/25/2018
ms.topic: conceptual
helpviewer_keywords:
- Workflow Designer, creating a workflow project
- creating a workflow project
ms.assetid: 235a125e-ebe7-4a98-bf77-86c8558728fb
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: 14fbaa5cd309bf048fa5c09fbb4b9521b3b3bf9b0fa09977751077d535d9fa70
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121440586"
---
# <a name="workflow-project-templates"></a>工作流项目模板

可以使用项目模板创建工作流、Windows Communication Foundation (WCF) 工作流服务、自定义活动和Visual Studio设计器。 本文介绍如何使用中提供的项目模板创建库Visual Studio。

## <a name="create-a-workflow-project"></a>创建工作流项目

Visual Studio提供了四个不同的工作流项目模板：

- 工作流控制台应用

- WCF 工作流服务应用

- 活动库

- 活动设计器库

若要访问这些模板，请首先安装 Windows **的 Workflow Foundation** Visual Studio。 有关详细说明，请参阅[Install Windows Workflow Foundation](developing-applications-with-the-workflow-designer.md#install-windows-workflow-foundation)。

1. 安装 Workflow Foundation 组件 **Windows，****选择"文件**  >  **""** 新建  >  **Project"。**

1. 搜索并选择工作流项目模板，例如工作流 **控制台应用程序** 模板。

1. 继续创建项目。

   > [!NOTE]
   > 如果要将新项目添加到现有解决方案，请在 Visual Studio 中打开该解决方案，右键单击 解决方案资源管理器 **中的解决方案**，然后选择"添加新  >  **Project"。**

## <a name="workflow-console-app"></a>工作流控制台应用

如果选择"工作流 **控制台应用程序"** 模板，Visual Studio XAML 创建工作流定义。 该工作流设计器打开并显示所创建的工作流的画布。 若要撰写工作流，请将活动或其他工作流项从 **"** 工具箱"拖动到设计图面。

## <a name="wcf-workflow-service-app"></a>WCF 工作流服务应用

如果选择 **"WCF 工作流服务应用程序"** 模板，Visual Studio创建一个作为 XAML 的服务定义。 该工作流设计器将打开设计视图，其中包含一组 <xref:System.Activities.Statements.Sequence> 和 <xref:System.ServiceModel.Activities.Receive> <xref:System.ServiceModel.Activities.SendReply> 活动。

## <a name="activity-library"></a>活动库

如果选择"活动 **库"** 模板，Visual Studio XAML 创建活动定义。 工作流设计器打开并显示自定义活动的画布。 将活动从 **"工具箱"** 拖动到设计图面，以将其包括在自定义活动中。

> [!NOTE]
> 自定义活动的正文中只允许有一个子活动。 但是，该子活动可以是复合活动，例如 <xref:System.Activities.Statements.Sequence> 活动或 <xref:System.Activities.Statements.Flowchart> 活动。

## <a name="activity-designer-library"></a>活动设计器库

如果选择"活动 **设计器库"** 模板，Visual Studio XAML 和代码隐藏实现文件创建活动设计器定义。 该工作流设计器打开并显示活动设计器的画布。 将Windows Presentation Foundation (WPF) 控件从 **"** 工具箱"拖动到设计图面，以在自定义活动设计器中使用它们。

有关实现自定义活动设计器的示例，请参阅 [如何：创建自定义活动设计器](/dotnet/framework/windows-workflow-foundation/how-to-create-a-custom-activity-designer)。

> [!NOTE]
> 自定义活动设计器可用于自定义活动和默认 .NET 活动。

## <a name="see-also"></a>另请参阅

- [使用工作流设计器](developing-applications-with-the-workflow-designer.md)
- [设计工作流 (.NET Framework) ](/dotnet/framework/windows-workflow-foundation/designing-workflows)

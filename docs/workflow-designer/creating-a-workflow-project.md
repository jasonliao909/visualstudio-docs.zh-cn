---
title: 创建 Workflow Foundation 项目
description: 了解如何通过 Visual Studio 中提供的项目模板来创建库和应用程序。
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
ms.openlocfilehash: adb28a3ffd44e1cfcd744ab603d9c7e8555cafc3
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126667583"
---
# <a name="workflow-project-templates"></a>工作流项目模板

可以使用 Visual Studio 项目模板创建工作流、Windows Communication Foundation (WCF) 工作流服务、自定义活动和自定义活动设计器。 本文介绍如何通过 Visual Studio 中提供的项目模板来创建库和应用程序。

## <a name="create-a-workflow-project"></a>创建工作流项目

Visual Studio 提供四种不同的工作流项目模板：

- 工作流控制台应用

- WCF 工作流服务应用

- 活动库

- 活动设计器库

若要访问这些模板，请首先安装 Visual Studio 的 Windows Workflow Foundation 组件。 有关详细说明，请参阅[安装 Windows Workflow Foundation](developing-applications-with-the-workflow-designer.md#install-windows-workflow-foundation)。

1. 安装 Windows Workflow Foundation 组件后，选择“文件” > “新建” > “项目”   。

1. 搜索并选择工作流项目模板，例如“工作流控制台应用程序”模板。

1. 继续执行以创建项目。

   > [!NOTE]
   > 若要向现有解决方案添加新项目，请在 Visual Studio 中打开该解决方案，在解决方案资源管理器中右键单击该解决方案，然后选择“添加” > “新建项目”  。

## <a name="workflow-console-app"></a>工作流控制台应用

如果选择“工作流控制台应用程序”模板，Visual Studio 将采用 XAML 创建工作流定义。 工作流设计器将打开并显示所创建工作流的画布。 若要撰写工作流，请将活动或其他工作流项从“工具箱”拖到设计图面。

## <a name="wcf-workflow-service-app"></a>WCF 工作流服务应用

如果选择“WCF 工作流服务应用程序”模板，Visual Studio 会采用 XAML 创建服务定义。 工作流设计器将打开设计视图，其中显示一个 <xref:System.Activities.Statements.Sequence> 活动，该活动包含一组 <xref:System.ServiceModel.Activities.Receive> 和 <xref:System.ServiceModel.Activities.SendReply> 活动。

## <a name="activity-library"></a>活动库

如果选择“活动库”模板，Visual Studio 会采用 XAML 创建活动定义。 工作流设计器将打开并显示自定义活动的画布。 将活动从“工具箱”拖到设计图面以使其包含在自定义活动中。

> [!NOTE]
> 自定义活动的主体中只能有一个子活动。 但是，该子活动可以是一个复合活动，如 <xref:System.Activities.Statements.Sequence> 活动或 <xref:System.Activities.Statements.Flowchart> 活动。

## <a name="activity-designer-library"></a>活动设计器库

如果选择“活动设计器库”模板，Visual Studio XAML 会采用 XAML 创建活动设计器定义和代码隐藏实现文件。 工作流设计器将打开并显示活动设计器的画布。 将 Windows Presentation Foundation (WPF) 控件从“工具箱”拖到设计图面以在自定义活动设计器中使用它们。

有关如何实现自定义活动设计器的示例，请参阅[如何：创建自定义活动设计器](/dotnet/framework/windows-workflow-foundation/how-to-create-a-custom-activity-designer)。

> [!NOTE]
> 自定义活动设计器可用于自定义活动以及默认的 .NET 活动。

## <a name="see-also"></a>另请参阅

- [使用工作流设计器](developing-applications-with-the-workflow-designer.md)
- [设计工作流 (.NET Framework)](/dotnet/framework/windows-workflow-foundation/designing-workflows)

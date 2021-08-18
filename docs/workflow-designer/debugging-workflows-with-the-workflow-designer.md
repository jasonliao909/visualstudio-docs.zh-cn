---
title: 使用工作流设计器调试工作流
description: 了解工作流设计器如何使用类似于默认调试器的进程来调试工作流和Visual Studio活动。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio Workflow Designer [WFD], debugging workflows
- Workflow Designer [WFD], debugging workflows
ms.assetid: d71308cf-d464-4536-8711-0d0a8eadb255
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: 454f916a80cda1b2b485cc6385218bfc88fb0490
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122155234"
---
# <a name="debug-workflows-with-the-workflow-designer"></a>使用命令调试工作流设计器

该 **工作流设计器** 提供了调试工作流和自定义活动的能力。 进程和行为类似于默认调试器Visual Studio的行为。

## <a name="invoke-the-workflow-debugger"></a>调用工作流调试器

通常，您可以像调试用其他 Visual Studio 编程语言编写的程序那样调试工作流。 可通过以下方法启动工作流调试器：

- 在 **"调试"菜单** 上 **选择** "附加到进程"，为工作流实例选择正在运行的主机进程。 此过程与附加到以托管代码编写的托管进程的过程相同。

- 按 **F5** 开始运行工作流的实例，或在命中断点后继续运行。

- 使用远程调试。 有关使用远程调试的信息，请参阅 [如何：启用远程调试](/previous-versions/visualstudio/visual-studio-2010/febz73k0(v=vs.100))。

   > [!NOTE]
   > 如果工作流应用程序面向 x86 体系结构，并且托管在运行 64 位操作系统的计算机上，则远程调试将不起作用，除非远程计算机上安装 Visual Studio 或工作流应用程序的目标更改为"任何 **CPU"。**

## <a name="step-through-code"></a>逐行执行代码

- **步骤输入**：按 **F11** 进入活动。 此调试器可以单步执行任何定义的处理程序。 如果未定义处理程序，则可以逐过程执行该活动，或者对于包含其他活动的复合活动，您可以单步执行第一个要执行的活动。

- **逐步执行：** 按 Shift  + **F11** 退出活动。 如果跳出某个活动，则会运行当前活动及其所有同级活动，直到这些活动完成为止。 然后调试器将在当前活动的父项处中断。 从代码处理程序中跳出时，调试器将在与此处理程序关联的活动处中断。

- **逐过程**：按 **F10 逐过程执行活动**。 逐过程执行复合活动时，调试器将在此复合活动的第一个可执行的子活动处中断。 逐过程执行非复合活动（例如 <xref:System.Activities.Statements.Assign> 活动）时，调试器将执行此活动及其关联的处理程序并在下一个活动处中断。 如果执行的活动是复合活动中的最后一个子活动，则在执行之后，调试器将在父活动处中断。

## <a name="debug-with-f5"></a>使用 F5 进行调试

如果要生成工作流控制台应用，只需按 **F5** 开始调试应用程序和工作流。 如果要自行生成活动库，则必须将可执行主机应用程序指定为启动项目。 若要在 解决方案资源管理器 中设置启动 **项目**，请右键单击主机的项目名称，然后选择"设置为启动 **Project"**。

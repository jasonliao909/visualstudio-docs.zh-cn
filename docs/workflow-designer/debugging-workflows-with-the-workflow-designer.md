---
title: 使用工作流设计器调试工作流
description: 了解工作流设计器如何使用类似于默认 Visual Studio 调试程序的进程来调试工作流和自定义活动。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126667582"
---
# <a name="debug-workflows-with-the-workflow-designer"></a>使用工作流设计器调试工作流

通过工作流设计器可以调试工作流和自定义活动。 其过程和行为与默认 Visual Studio 调试器的过程和行为类似。

## <a name="invoke-the-workflow-debugger"></a>调用工作流调试器

通常，您可以像调试用其他 Visual Studio 编程语言编写的程序那样调试工作流。 可通过以下方法启动工作流调试器：

- 选择“调试”菜单上的“附加到进程”，以选择正在运行的工作流实例托管进程。 此过程与附加到以托管代码编写的托管进程的过程相同。

- 按 F5 以开始运行工作流实例，或者在命中断点后继续运行。

- 使用远程调试。 有关使用远程调试的信息，请参见[如何启用远程调试](/previous-versions/visualstudio/visual-studio-2010/febz73k0(v=vs.100))。

   > [!NOTE]
   > 如果工作流应用程序针对 x86 体系结构并托管在运行 64 位操作系统的计算机上，远程调试将无法工作，除非在远程计算机上安装了 Visual Studio 或将工作流应用程序的目标更改为“任意 CPU”。

## <a name="step-through-code"></a>逐行执行代码

- 单步执行：可以通过按 F11 来单步执行某个活动。 此调试器可以单步执行任何定义的处理程序。 如果未定义处理程序，则可以逐过程执行该活动，或者对于包含其他活动的复合活动，您可以单步执行第一个要执行的活动。

- 单步跳出：可以通过按 Shift+F11  来单步跳出某个活动。 如果跳出某个活动，则会运行当前活动及其所有同级活动，直到这些活动完成为止。 然后调试器将在当前活动的父项处中断。 从代码处理程序中跳出时，调试器将在与此处理程序关联的活动处中断。

- 逐过程：可以使用按 F10 逐过程执行某个活动。 逐过程执行复合活动时，调试器将在此复合活动的第一个可执行的子活动处中断。 逐过程执行非复合活动（例如 <xref:System.Activities.Statements.Assign> 活动）时，调试器将执行此活动及其关联的处理程序并在下一个活动处中断。 如果执行的活动是复合活动中的最后一个子活动，则在执行之后，调试器将在父活动处中断。

## <a name="debug-with-f5"></a>使用 F5 调试

如果要生成工作流控制台应用，只需按 F5 开始调试应用程序和工作流。 如果要生成活动库自身，必须指定可执行的宿主应用程序作为启动项目。 若要在“解决方案资源管理器”中设置启动项目，请右键单击宿主的项目名称，然后选择“设为启动项目”。

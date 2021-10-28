---
title: 历史调试 | Microsoft Docs
description: 通过在应用的执行过程中前后移动时检查其状态来排查应用故障。 IntelliTrace 收集此功能的信息。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 7cc5ddf2-2f7c-4f83-b7ca-58e92e9bfdd2
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 0d3198e5fb784cac999097167ef2499004823781
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126736358"
---
# <a name="historical-debugging-c-visual-basic-c"></a>历史调试（C#、Visual Basic、C++）

历史调试是取决于 IntelliTrace 所收集信息的调试模式。 它允许你向前和前后移动应用程序的执行，并检查其状态。

 可以在 Visual Studio 企业版（但不可在专业版或社区版）中使用 IntelliTrace。

## <a name="why-use-historical-debugging"></a>为什么要使用历史调试？

 设置断点来查找 Bug 是一件没有太多确定性的事。 在你怀疑代码中可能存在 Bug 的位置附近设置断点，然后在调试器中运行应用程序，希望断点发挥作用，执行中断的位置就可以揭露 Bug 的来源。 如果不起作用，需要在代码的其他位置尝试设置一个断点，然后重新运行调试器，反复执行测试步骤，直到找到问题。

 ![设置断点](../debugger/media/breakpointprocesa.png "BreakpointProcesa")

 可以使用 IntelliTrace 和历史调试，在你的应用程序中四处漫游，以查看其状态 （调用堆栈和局部变量），而无需设置断点、重新启动调试、重复测试步骤。 这可以为你节省大量时间，特别是在 Bug 位于需要很长时间才能完成执行的测试方案的深处时。

## <a name="how-do-i-start-using-historical-debugging"></a>如何开始使用历史调试？

默认启用 IntelliTrace。 你需要确定感兴趣的事件和函数调用，以及是否希望查看完整应用程序状态的快照。 要详细了解如何定义想查看的内容，请参阅 [IntelliTrace 功能](../debugger/intellitrace-features.md)。 功能支持因语言和应用类型而异。

- 若要使用历史调试来查看快照，请参阅[使用 IntelliTrace 检查以前的应用状态](../debugger/view-historical-application-state.md)
- 若要了解如何检查变量和导航代码，请参阅[使用历史调试检查应用](../debugger/historical-debugging-inspect-app.md)
- 若要详细了解如何使用 IntelliTrace 事件进行调试，请参阅[演练：使用 IntelliTrace](../debugger/walkthrough-using-intellitrace.md)。
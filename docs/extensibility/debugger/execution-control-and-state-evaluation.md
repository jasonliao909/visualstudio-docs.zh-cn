---
title: 执行控件和状态计算 |Microsoft Docs
description: 了解 Visual Studio 调试如何将其执行控制置于调试器组件之间发送的事件上。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], execution control
- expression evaluation, control of execution
ms.assetid: 55adde38-1622-4b51-83cb-ce1b04c1ca7a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 598332ec1e9e1cb270360822ca32792b9a53f5c1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105096949"
---
# <a name="execution-control-and-state-evaluation"></a>执行控制和状态评估
调试应用程序需要实现此类执行控制功能，以单步执行函数，在断点处停止，继续执行。 Visual Studio 调试使其执行控制依赖于在调试器组件之间发送的事件。

## <a name="in-this-section"></a>本节内容
 [程序控制](../../extensibility/debugger/program-control.md) 列出在程序级别发生的以下例程：设置下一个语句、执行、单步执行、继续、挂起和恢复。

 [与断点相关的方法](../../extensibility/debugger/breakpoint-related-methods.md) 定义 Visual Studio 支持的绑定和挂起的断点类型。

 [调用堆栈计算](../../extensibility/debugger/call-stack-evaluation.md) 讨论在中断模式下允许查看调用堆栈堆栈帧的方法的实现。

 [表达式计算](../../extensibility/debugger/expression-evaluation-visual-studio-debugging-sdk.md) 说明如何在分析和评估在 IDE 的某个 windows 中输入的表达式时，调试引擎 (DE) 、表达式计算 (EE) 和会话调试管理器。

 [控件事件](../../extensibility/debugger/control-events.md) 讨论在程序的受控执行过程中用于发送事件的接口。

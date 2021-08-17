---
title: 执行控制和状态评估|Microsoft Docs
description: 了解如何Visual Studio调试基于调试器组件之间发送的事件执行控制。
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
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: dbde8bb527b29e2c303218236268a3730a0c8b68
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122096631"
---
# <a name="execution-control-and-state-evaluation"></a>执行控制和状态评估
调试应用程序需要实现诸如单步执行函数、在断点处停止以及继续执行等执行控制功能。 Visual Studio将执行控制基于调试器组件之间发送的事件。

## <a name="in-this-section"></a>本节内容
 [程序控制](../../extensibility/debugger/program-control.md) 列出在程序级别发生的以下例程：设置下一语句、执行、单步执行、继续、挂起和恢复。

 [与断点相关的方法](../../extensibility/debugger/breakpoint-related-methods.md)定义所支持的绑定和挂起的断Visual Studio类型。

 [调用堆栈评估](../../extensibility/debugger/call-stack-evaluation.md) 讨论方法的实现，这些方法允许在中断模式期间查看调用堆栈的堆栈帧。

 [表达式计算](../../extensibility/debugger/expression-evaluation-visual-studio-debugging-sdk.md)说明调试引擎 (DE) 、表达式计算 (企业版) 和会话调试管理器如何参与分析和计算输入到 IDE 窗口之一的表达式。

 [控制事件](../../extensibility/debugger/control-events.md) 讨论用于在程序的受控执行期间发送事件的接口。

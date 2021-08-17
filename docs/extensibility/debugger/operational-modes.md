---
title: 操作模式|Microsoft Docs
description: 了解 IDE 可以运行的三种模式，即设计模式、运行模式和中断模式。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debug engines, modes
ms.assetid: f69972d0-809d-40df-9da3-04738791391c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 0af5f083c54fbb587bcbed52bc59968ee0477e5f
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122073313"
---
# <a name="operational-modes"></a>操作模式
IDE 可以运行三种模式，如下所示：

- [设计模式](#vsconoperationalmodesanchor1)

- [运行模式](#vsconoperationalmodesanchor2)

- [中断模式](#vsconoperationalmodesanchor3)

  自定义调试引擎 (DE) 模式之间的转换是一个实现决策，要求你熟悉转换机制。 DE 可能直接实现这些模式，也可能不直接实现这些模式。 这些模式实际上就是调试包模式，这些模式基于用户操作或 DE 中的事件进行切换。 例如，从运行模式转换到中断模式是由 DE 中的停止事件启动的。 从中断模式到运行模式或步骤模式的转换由执行步骤或执行等操作的用户启动。 有关 DE 转换的信息，请参阅 [控制执行](../../extensibility/debugger/control-of-execution.md)。

## <a name="design-mode"></a><a name="vsconoperationalmodesanchor1"></a> 设计模式
 设计模式是调试的非Visual Studio状态，在此期间，可以在应用程序中设置调试功能。

 在设计模式期间，只会使用几个调试功能。 开发人员可以选择设置断点或创建监视表达式。 当 IDE 位于设计模式时，永远不会加载或调用 DE。 仅在运行模式和中断模式期间与 DE 交互。

## <a name="run-mode"></a><a name="vsconoperationalmodesanchor2"></a> 运行模式
 当程序在 IDE 中的调试会话中运行时，将发生运行模式。 应用程序将一直运行到终止、命中断点或引发异常。 当应用程序运行到终止时，DE 将转换为设计模式。 当断点命中或引发异常时，DE 将转换为中断模式。

## <a name="break-mode"></a><a name="vsconoperationalmodesanchor3"></a> 中断模式
 暂停调试程序的执行时，将发生中断模式。 中断模式在中断时为开发人员提供应用程序的快照，并允许开发人员分析应用程序的状态并更改应用程序的运行方式。 开发人员可以查看和编辑代码、检查或修改数据、重启应用程序、结束执行或从同一点继续执行。

 当 DE 发送同步停止事件时，将进入中断模式。 同步停止事件（也称为停止事件）通知会话调试管理器 (SDM) 和 IDE，指出正在调试的应用程序已停止执行代码。 [IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md)和[IDebugExceptionEvent2](../../extensibility/debugger/reference/idebugexceptionevent2.md)接口是停止事件的示例。

 停止事件通过调用以下方法之一继续，这些方法将调试器从中断模式转换为运行模式或单步模式：

- [执行](../../extensibility/debugger/reference/idebugprocess3-execute.md)

- [步骤](../../extensibility/debugger/reference/idebugprocess3-step.md)

- [继续](../../extensibility/debugger/reference/idebugprocess3-continue.md)

### <a name="step-mode"></a><a name="vsconoperationalmodesanchor4"></a> 步骤模式
 当程序进入下一行代码，或者进入、超过或退出函数时，将发生步骤模式。 通过调用 方法 Step 执行 [步骤](../../extensibility/debugger/reference/idebugprocess3-step.md)。 此方法需要 `DWORD` 将 [STEPUNIT](../../extensibility/debugger/reference/stepunit.md) 和 [STEPKIND](../../extensibility/debugger/reference/stepkind.md) 枚举指定为输入参数的 。

 当程序成功进入下一行代码或进入函数，或者运行到游标或设置断点时，DE 会自动转换回中断模式。

## <a name="see-also"></a>请参阅
- [控制执行](../../extensibility/debugger/control-of-execution.md)

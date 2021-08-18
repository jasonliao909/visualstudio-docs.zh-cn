---
title: 控制事件|Microsoft Docs
description: 了解如何使用 IDebugEvent2 接口在程序的受控执行期间发送事件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], events
ms.assetid: 0fc63484-5fb6-4887-9ea4-1905b459ca9d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 7ca8f78172613a41a6864490bedd99fc1f32393c
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122111770"
---
# <a name="control-events"></a>控制事件
必须在程序的受控执行期间发送事件。 所有事件都是使用 [IDebugEvent2](../../extensibility/debugger/reference/idebugevent2.md) 接口发送的，并且具有要求实现 [IDebugEvent2：：GetAttributes](../../extensibility/debugger/reference/idebugevent2-getattributes.md) 方法的属性。

## <a name="additional-methods"></a>其他方法
 某些事件需要实现其他方法，如下所示：

- 初始化调试引擎 (DE) 时发送 [IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md) 接口需要实现 [IDebugEngineCreateEvent2：：GetEngine](../../extensibility/debugger/reference/idebugenginecreateevent2-getengine.md) 方法。

- 执行控制需要实现 [IDebugBreakEvent2](../../extensibility/debugger/reference/idebugbreakevent2.md) 和[IDebugStepCompleteEvent2 接口等控制](../../extensibility/debugger/reference/idebugstepcompleteevent2.md) 事件。 **只有异步中断才需要 IDebugBreakEvent2。**

- 单步执行函数需要实现 [IDebugStepCompleteEvent2](../../extensibility/debugger/reference/idebugstepcompleteevent2.md) 接口及其方法。

  从断点派生的事件需要实现[IDebugBreakpointErrorEvent2、IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)和[IDebugBreakpointBoundEvent2](../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)接口，以及[IDebugBreakpointBoundEvent2：：GetPendingBreakpoint](../../extensibility/debugger/reference/idebugbreakpointboundevent2-getpendingbreakpoint.md) [和 EnumBoundBreakpoints](../../extensibility/debugger/reference/idebugbreakpointboundevent2-enumboundbreakpoints.md)方法。 [](../../extensibility/debugger/reference/idebugbreakpointevent2.md)

  异步表达式计算要求实现 [IDebugExpressionEvaluationCompleteEvent2](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md) 接口及其 [IDebugExpressionEvaluationCompleteEvent2：：GetExpression](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getexpression.md)[和 GetResult](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getresult.md) 方法。

  同步事件需要实现 [IDebugEngine2：：ContinueFromSynchronousEvent](../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md) 方法。

  若要让引擎编写字符串样式的输出，必须实现 [IDebugOutputStringEvent2：：GetString](../../extensibility/debugger/reference/idebugoutputstringevent2-getstring.md) 方法。

## <a name="see-also"></a>请参阅
- [执行控制和状态评估](../../extensibility/debugger/execution-control-and-state-evaluation.md)

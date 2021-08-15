---
title: 支持的事件|Microsoft Docs
description: 了解调试支持Visual Studio类型，包括异步事件、同步事件和停止事件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], supported events
ms.assetid: a3c0386d-551e-4734-9a0c-368d1c2e6671
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 1fdd8cde2628a76c700e29b58885e45ff608fe0b3043df8b26e161a748066eaa
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121388898"
---
# <a name="supported-event-types"></a>支持的事件类型
Visual Studio当前支持以下事件类型：

- 异步事件

   通知会话调试管理器 (SDM) 和 IDE，告知正在调试的应用程序的状态正在更改。 这些事件由 SDM 和 IDE 处理。 处理事件后，不会 (DE) 向调试引擎发送答复。 [IDebugOutputStringEvent2](../../extensibility/debugger/reference/idebugoutputstringevent2.md)和[IDebugMessageEvent2](../../extensibility/debugger/reference/idebugmessageevent2.md)接口是异步事件的示例。

- 同步事件

   通知 SDM 和 IDE 正在调试的应用程序的状态正在更改。 这些事件和异步事件之间的唯一区别是，通过 [ContinueFromSynchronousEvent](../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md) 方法发送答复。

   如果需要 DE 在 IDE 接收和处理事件后继续处理，则发送同步事件非常有用。

- 同步停止事件或停止事件

   通知 SDM 和 IDE 正在调试的应用程序已停止执行代码。 通过方法 Event 发送停止事件[时，](../../extensibility/debugger/reference/idebugeventcallback2-event.md)[需要 IDebugThread2](../../extensibility/debugger/reference/idebugthread2.md)参数。 停止事件通过调用以下方法之一继续：

  - [执行](../../extensibility/debugger/reference/idebugprogram2-execute.md)

  - [步骤](../../extensibility/debugger/reference/idebugprogram2-step.md)

  - [继续](../../extensibility/debugger/reference/idebugprogram2-continue.md)

    [IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md)和[IDebugExceptionEvent2](../../extensibility/debugger/reference/idebugexceptionevent2.md)接口是停止事件的示例。

  > [!NOTE]
  > 不支持异步停止事件。 发送异步停止事件是一个错误。

## <a name="discussion"></a>讨论区
 事件的实际实现取决于 DE 的设计。 发送的每个事件的类型取决于其属性，这些属性是在设计 DE 时设置的。 例如，一个 DE 可能会将 [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md) 作为异步事件发送，而另一个 DE 可能会将其发送为停止事件。

 下表指定哪些事件以及事件类型需要哪些程序参数和线程参数。 任何事件都可以是同步的。 无需同步任何事件。

> [!NOTE]
> 所有 [事件都需要 IDebugEngine2](../../extensibility/debugger/reference/idebugengine2.md) 接口。

|事件|IDebugProgram2|IDebugThread2|停止事件|
|-----------|--------------------|-------------------|---------------------|
|[IDebugActivateDocumentEvent2](../../extensibility/debugger/reference/idebugactivatedocumentevent2.md)|允许，但不是必需的|允许，但不是必需的|否|
|[IDebugBreakEvent2](../../extensibility/debugger/reference/idebugbreakevent2.md)|必需|必需|是|
|[IDebugBreakpointBoundEvent2](../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)|允许，但不是必需的|允许，但不是必需的|否|
|[IDebugBreakpointErrorEvent2](../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)|允许，但不是必需的|允许，但不是必需的|否|
|[IDebugBreakpointUnboundEvent2](../../extensibility/debugger/reference/idebugbreakpointunboundevent2.md)|允许，但不是必需的|允许，但不是必需的|否|
|[IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md)|必需|必需|是|
|[IDebugCanStopEvent2](../../extensibility/debugger/reference/idebugcanstopevent2.md)|必需|必选|否|
|[IDebugDocumentTextEvents2](../../extensibility/debugger/reference/idebugdocumenttextevents2.md)|不允许|不允许|否|
|[IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md)|不允许|不允许|否|
|[IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md)|必需|必需|是|
|[IDebugErrorEvent2](../../extensibility/debugger/reference/idebugerrorevent2.md)|允许，但不是必需的|允许，但不是必需的|可以|
|[IDebugExceptionEvent2](../../extensibility/debugger/reference/idebugexceptionevent2.md)|必需|必需|是|
|[IDebugExpressionEvaluationCompleteEvent2](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)|允许，但不是必需的|允许，但不是必需的|可以|
|[IDebugInterceptExceptionCompleteEvent2](../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2.md)|必需|必需|是|
|[IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md)|必需|必需|是|
|[IDebugMessageEvent2](../../extensibility/debugger/reference/idebugmessageevent2.md)|允许，但不是必需的|允许，但不是必需的|可以|
|[IDebugModuleLoadEvent2](../../extensibility/debugger/reference/idebugmoduleloadevent2.md)|必需|允许，但不是必需的|否|
|[IDebugOutputStringEvent2](../../extensibility/debugger/reference/idebugoutputstringevent2.md)|允许，但不是必需的|允许，但不是必需的|否|
|[IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md)|必需|允许，但不是必需的|否|
|[IDebugProgramDestroyEvent2](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)|必需|允许，但不是必需的|否|
|[IDebugPropertyCreateEvent2](../../extensibility/debugger/reference/idebugpropertycreateevent2.md)|必需|允许，但不是必需的|否|
|[IDebugPropertyDestroyEvent2](../../extensibility/debugger/reference/idebugpropertydestroyevent2.md)|必需|允许，但不是必需的|否|
|[IDebugReturnValueEvent2](../../extensibility/debugger/reference/idebugreturnvalueevent2.md)|允许，但不是必需的|允许，但不是必需的|否|
|IDebugStopCompleteEvent2|必需|必需|是|
|[IDebugStepCompleteEvent2](../../extensibility/debugger/reference/idebugstepcompleteevent2.md)|必需|必需|是|
|[IDebugSymbolSearchEvent2](../../extensibility/debugger/reference/idebugsymbolsearchevent2.md)|允许，但不是必需的|允许，但不是必需的|否|
|[IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md)|必需|必选|否|
|[IDebugThreadDestroyEvent2](../../extensibility/debugger/reference/idebugthreaddestroyevent2.md)|必需|必选|否|
|[IDebugThreadNameChangedEvent2](../../extensibility/debugger/reference/idebugthreadnamechangedevent2.md)|允许，但不是必需的|允许，但不是必需的|否|

## <a name="see-also"></a>另请参阅
- [发送事件](../../extensibility/debugger/sending-events.md)

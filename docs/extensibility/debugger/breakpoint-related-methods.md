---
title: Breakpoint-Related方法|Microsoft Docs
description: Visual Studio调试支持绑定断点（这些断点已成功绑定到代码中的位置）和挂起的断点（尚未绑定）。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], breakpoint methods
- breakpoints, methods
ms.assetid: a6f77bf0-bf81-443f-8683-5f12075bbe10
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ec218cea05dffc1c558cabdef47895da9ad7ba9c
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901495"
---
# <a name="breakpoint-related-methods"></a>与断点相关的方法
调试引擎 (DE) 必须支持断点设置。 Visual Studio调试支持以下类型的断点：

- Bound

     通过 UI 请求并成功绑定到指定的代码位置

- 挂起

     通过 UI 请求但尚未绑定到实际指令

## <a name="discussion"></a>讨论区
 例如，当尚未加载指令时，会出现挂起的断点。 加载代码时，挂起的断点会尝试绑定到指定位置的代码，即，在代码中插入中断指令。 事件将发送到会话调试管理器 (SDM) 以指示绑定成功或通知存在绑定错误。

 挂起的断点还管理其自己的相应绑定断点的内部列表。 一个挂起的断点可能会导致在代码中插入多个断点。 调试VISUAL STUDIO UI 显示挂起断点及其对应的绑定断点的树视图。

 创建和使用挂起断点需要实现 [IDebugEngine2：：CreatePendingBreakpoint](../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md) 方法以及 [以下 IDebugPendingBreakpoint2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md) 接口方法。

|方法|描述|
|------------|-----------------|
|[CanBind](../../extensibility/debugger/reference/idebugpendingbreakpoint2-canbind.md)|确定指定的挂起断点是否可以绑定到代码位置。|
|[绑定](../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)|将指定的挂起断点绑定到一个或多个代码位置。|
|[GetState](../../extensibility/debugger/reference/idebugpendingbreakpoint2-getstate.md)|获取挂起断点的状态。|
|[GetBreakpointRequest](../../extensibility/debugger/reference/idebugpendingbreakpoint2-getbreakpointrequest.md)|获取用于创建挂起断点的断点请求。|
|[启用](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enable.md)|切换挂起断点的启用状态。|
|[EnumBoundBreakpoints](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md)|枚举从挂起断点绑定的所有断点。|
|[EnumErrorBreakpoints](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md)|枚举由挂起断点导致的所有错误断点。|
|[删除](../../extensibility/debugger/reference/idebugpendingbreakpoint2-delete.md)|删除挂起的断点及其绑定的所有断点。|

 若要枚举绑定断点和错误断点，必须实现 [IEnumDebugBoundBreakpoints2](../../extensibility/debugger/reference/ienumdebugboundbreakpoints2.md) 和 [IEnumDebugErrorBreakpoints2](../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2.md)的所有方法。

 绑定到代码位置的挂起断点需要实现以下 [IDebugBoundBreakpoint2](../../extensibility/debugger/reference/idebugboundbreakpoint2.md) 方法。

|方法|描述|
|------------|-----------------|
|[GetPendingBreakpoint](../../extensibility/debugger/reference/idebugboundbreakpoint2-getpendingbreakpoint.md)|获取包含断点的挂起断点。|
|[GetState](../../extensibility/debugger/reference/idebugboundbreakpoint2-getstate.md)|获取绑定断点的状态。|
|[GetBreakpointResolution](../../extensibility/debugger/reference/idebugboundbreakpoint2-getbreakpointresolution.md)|获取描述断点的断点解析。|
|[启用](../../extensibility/debugger/reference/idebugboundbreakpoint2-enable.md)|启用或禁用断点。|
|[删除](../../extensibility/debugger/reference/idebugboundbreakpoint2-delete.md)|删除绑定断点。|

 解决和请求信息需要实现以下 [IDebugBreakpointResolution2](../../extensibility/debugger/reference/idebugbreakpointresolution2.md) 方法。

|方法|描述|
|------------|-----------------|
|[GetBreakpointType](../../extensibility/debugger/reference/idebugbreakpointresolution2-getbreakpointtype.md)|获取解析表示的断点的类型。|
|[GetResolutionInfo](../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md)|获取描述断点的断点解析信息。|

 解决绑定期间可能会发生的错误需要实现以下 [IDebugErrorBreakpoint2](../../extensibility/debugger/reference/idebugerrorbreakpoint2.md) 方法。

|方法|描述|
|------------|-----------------|
|[GetPendingBreakpoint](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getpendingbreakpoint.md)|获取包含错误断点的挂起断点。|
|[GetBreakpointResolution](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getbreakpointresolution.md)|获取描述错误断点的断点错误解决方法。|

 解决绑定期间可能会发生的错误还需要以下 [IDebugErrorBreakpointResolution2 方法](../../extensibility/debugger/reference/idebugerrorbreakpointresolution2.md)。

|方法|描述|
|------------|-----------------|
|[GetBreakpointType](../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getbreakpointtype.md)|获取断点的类型。|
|[GetResolutionInfo](../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getresolutioninfo.md)|获取断点的解析信息。|

 在断点查看源代码需要实现 [IDebugStackFrame2：：GetDocumentContext](../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md) 和/或 [IDebugStackFrame2：：GetCodeContext](../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md)的方法。

## <a name="see-also"></a>另请参阅
- [执行控制和状态评估](../../extensibility/debugger/execution-control-and-state-evaluation.md)

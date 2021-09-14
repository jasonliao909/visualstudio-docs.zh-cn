---
title: Breakpoint-Related 方法 |Microsoft Docs
description: Visual Studio 调试支持绑定的断点，这些断点已成功绑定到代码中的某个位置，并且仍未绑定挂起的断点。
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
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: ad634ddce8f42c8bf5e183ebdf8f75389553dba5
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126663811"
---
# <a name="breakpoint-related-methods"></a>与断点相关的方法
调试引擎 (DE) 必须支持断点设置。 Visual Studio 调试支持以下类型的断点：

- Bound

     通过 UI 请求并成功绑定到指定的代码位置

- 挂起的

     通过 UI 请求，但尚未绑定到实际说明

## <a name="discussion"></a>讨论 (Discussion)
 例如，如果尚未加载说明，则会发生挂起的断点。 当加载代码时，挂起的断点尝试绑定到指定位置的代码，即在代码中插入中断指令。 事件将发送到会话调试管理器 (SDM) ，以指示成功绑定或通知存在绑定错误。

 挂起的断点还管理其自己的相应绑定断点的内部列表。 一个挂起的断点可能导致在代码中插入多个断点。 Visual Studio 调试 UI 显示挂起断点及其对应绑定断点的树视图。

 创建和使用挂起的断点需要实现 [IDebugEngine2：： CreatePendingBreakpoint](../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md) 方法以及以下 [IDebugPendingBreakpoint2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md) 接口方法。

|方法|说明|
|------------|-----------------|
|[CanBind](../../extensibility/debugger/reference/idebugpendingbreakpoint2-canbind.md)|确定指定的挂起断点是否可以绑定到代码位置。|
|[绑定](../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)|将指定的挂起断点绑定到一个或多个代码位置。|
|[GetState](../../extensibility/debugger/reference/idebugpendingbreakpoint2-getstate.md)|获取挂起断点的状态。|
|[GetBreakpointRequest](../../extensibility/debugger/reference/idebugpendingbreakpoint2-getbreakpointrequest.md)|获取用于创建挂起断点的断点请求。|
|启用|切换挂起断点的已启用状态。|
|[EnumBoundBreakpoints](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md)|枚举从挂起断点绑定的所有断点。|
|[EnumErrorBreakpoints](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md)|枚举由挂起断点生成的所有错误断点。|
|[删除](../../extensibility/debugger/reference/idebugpendingbreakpoint2-delete.md)|删除挂起的断点以及从该断点绑定的所有断点。|

 若要枚举绑定的断点和错误断点，必须实现 [IEnumDebugBoundBreakpoints2](../../extensibility/debugger/reference/ienumdebugboundbreakpoints2.md) 和 [IEnumDebugErrorBreakpoints2](../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2.md)的所有方法。

 绑定到代码位置的挂起断点需要实现以下 [IDebugBoundBreakpoint2](../../extensibility/debugger/reference/idebugboundbreakpoint2.md) 方法。

|方法|说明|
|------------|-----------------|
|[GetPendingBreakpoint](../../extensibility/debugger/reference/idebugboundbreakpoint2-getpendingbreakpoint.md)|获取包含断点的挂起断点。|
|[GetState](../../extensibility/debugger/reference/idebugboundbreakpoint2-getstate.md)|获取绑定断点的状态。|
|[GetBreakpointResolution](../../extensibility/debugger/reference/idebugboundbreakpoint2-getbreakpointresolution.md)|获取描述断点的断点解析。|
|启用|启用或禁用断点。|
|[删除](../../extensibility/debugger/reference/idebugboundbreakpoint2-delete.md)|删除绑定断点。|

 解析和请求信息需要实现以下 [IDebugBreakpointResolution2](../../extensibility/debugger/reference/idebugbreakpointresolution2.md) 方法。

|方法|说明|
|------------|-----------------|
|[GetBreakpointType](../../extensibility/debugger/reference/idebugbreakpointresolution2-getbreakpointtype.md)|获取由解析表示的断点类型。|
|[GetResolutionInfo](../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md)|获取描述断点的断点解析信息。|

 在绑定过程中可能出现的错误的解决方法要求实现以下 [IDebugErrorBreakpoint2](../../extensibility/debugger/reference/idebugerrorbreakpoint2.md) 方法。

|方法|说明|
|------------|-----------------|
|[GetPendingBreakpoint](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getpendingbreakpoint.md)|获取包含错误断点的挂起断点。|
|[GetBreakpointResolution](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getbreakpointresolution.md)|获取描述错误断点的断点错误解析。|

 在绑定过程中可能出现的错误的解决方法还需要 [IDebugErrorBreakpointResolution2](../../extensibility/debugger/reference/idebugerrorbreakpointresolution2.md)的以下方法。

|方法|说明|
|------------|-----------------|
|[GetBreakpointType](../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getbreakpointtype.md)|获取断点的类型。|
|[GetResolutionInfo](../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getresolutioninfo.md)|获取断点的解析信息。|

 在断点处查看源代码需要实现 [IDebugStackFrame2：： GetDocumentContext](../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md) 和/或 [IDebugStackFrame2：： GetCodeContext](../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md)方法的方法。

## <a name="see-also"></a>另请参阅
- [执行控制和状态评估](../../extensibility/debugger/execution-control-and-state-evaluation.md)

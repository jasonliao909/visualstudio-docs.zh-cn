---
description: 此接口告知会话调试管理器 (SDM) 挂起的断点已成功绑定到已加载的程序。
title: IDebugBreakpointBoundEvent2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointBoundEvent2
helpviewer_keywords:
- IDebugBreakpointBoundEvent2
ms.assetid: 24ba362e-5be1-481a-b071-e1ebd3cae6e8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 63aa58209d2d2b96575e9f8c092f696757dcd661d2062a7ba1e0f22e79428d6f
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121292970"
---
# <a name="idebugbreakpointboundevent2"></a>IDebugBreakpointBoundEvent2
此接口告知会话调试管理器 (SDM) 挂起的断点已成功绑定到已加载的程序。

## <a name="syntax"></a>语法

```
IDebugBreakpointBoundEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 DE 实现此接口，作为对断点的支持的一部分。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)接口必须在与此接口相同的对象上实现 (SDM 使用[QueryInterface](/cpp/atl/queryinterface)访问接口 `IDebugEvent2`) 。

## <a name="notes-for-callers"></a>调用方说明
 当挂起的断点成功绑定到正在调试的程序时，DE 将创建并发送此事件对象。 事件是通过使用 SDM 在附加到正在调试的程序时提供的 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) 回调函数发送的。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法 `IDebugBreakpointBoundEvent2` 。

|方法|说明|
|------------|-----------------|
|[GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugbreakpointboundevent2-getpendingbreakpoint.md)|获取正在绑定的挂起断点。|
|[EnumBoundBreakpoints](../../../extensibility/debugger/reference/idebugbreakpointboundevent2-enumboundbreakpoints.md)|创建绑定到此事件的断点的枚举器。|

## <a name="remarks"></a>备注
 每当绑定断点时，都会向 SDM 发送事件。 如果无法绑定断点，则发送 [IDebugBreakpointErrorEvent2;](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md) 否则， `IDebugBreakpointBoundEvent2` 将发送 。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugBreakpointErrorEvent2](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)

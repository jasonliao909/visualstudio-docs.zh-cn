---
description: 此接口表示绑定到代码位置的断点。
title: IDebugBoundBreakpoint2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBoundBreakpoint2
helpviewer_keywords:
- IDebugBoundBreakpoint2 interface
ms.assetid: df33c52e-ded2-48a0-951d-1f36c8fc922e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 4865697e99071b59c0bc097500c91794ad882a830a9a031a680aa8692a1761a2
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121417595"
---
# <a name="idebugboundbreakpoint2"></a>IDebugBoundBreakpoint2
此接口表示绑定到代码位置的断点。

## <a name="syntax"></a>语法

```
IDebugBoundBreakpoint2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 调试引擎 (DE) 实现此接口作为其对断点的支持的一部分。

## <a name="notes-for-callers"></a>调用方说明
 调用 [Bind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md) 将创建此接口。 调用 [GetBreakpoint](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2-getbreakpoint.md) 和 [Next](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2-next.md) 会获得此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法 `IDebugBoundBreakpoint2` 。

|方法|说明|
|------------|-----------------|
|[GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugboundbreakpoint2-getpendingbreakpoint.md)|获取从中创建指定绑定断点的挂起断点。|
|[GetState](../../../extensibility/debugger/reference/idebugboundbreakpoint2-getstate.md)|获取此绑定断点的状态。|
|[GetHitCount](../../../extensibility/debugger/reference/idebugboundbreakpoint2-gethitcount.md)|获取此绑定断点的当前命中计数。|
|[GetBreakpointResolution](../../../extensibility/debugger/reference/idebugboundbreakpoint2-getbreakpointresolution.md)|获取描述此断点的断点解析。|
|启用|启用或禁用断点。|
|[SetHitCount](../../../extensibility/debugger/reference/idebugboundbreakpoint2-sethitcount.md)|设置此绑定断点的命中次数。|
|[SetCondition](../../../extensibility/debugger/reference/idebugboundbreakpoint2-setcondition.md)|设置或更改与此绑定断点关联的条件。|
|[SetPassCount](../../../extensibility/debugger/reference/idebugboundbreakpoint2-setpasscount.md)|设置或更改与此绑定断点关联的传递计数。|
|[删除](../../../extensibility/debugger/reference/idebugboundbreakpoint2-delete.md)|删除断点。|

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [GetBreakpoint](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2-getbreakpoint.md)
- [下一页](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2-next.md)
- [绑定](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)

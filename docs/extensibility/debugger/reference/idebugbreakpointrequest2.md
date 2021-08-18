---
description: IDebugBreakPointRequest2 接口表示创建和绑定任何类型的断点所必需的信息。
title: IDebugBreakpointRequest2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointRequest2
helpviewer_keywords:
- IDebugBreakpointRequest2 interface
ms.assetid: 01ac4013-96f9-4235-b289-f55f9e99558f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: df0b17c6a1696315e328121eaa305a65defe40ea
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122104230"
---
# <a name="idebugbreakpointrequest2"></a>IDebugBreakpointRequest2
此接口表示创建和绑定任何类型的断点所必需的信息。

## <a name="syntax"></a>语法

```
IDebugBreakpointRequest2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 SDM (会话) 通常实现此接口。

## <a name="notes-for-callers"></a>调用方说明
 DE 调试 (DE) 通过调用 [CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md) 接收此接口，以便创建挂起的断点。 调用 [GetBreakpointRequest](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getbreakpointrequest.md) 可以从 DE 检索此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法 `IDebugBreakpointRequest2` 。

|方法|说明|
|------------|-----------------|
|[GetLocationType](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getlocationtype.md)|获取此断点请求的断点位置类型。|
|[GetRequestInfo](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getrequestinfo.md)|获取描述此断点请求的断点请求信息。|

## <a name="remarks"></a>备注
 加载正在调试的程序后，对 [Bind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md) 的调用将挂起的断点绑定到程序中请求的位置。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)
- [GetBreakpointRequest](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getbreakpointrequest.md)
- [绑定](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)

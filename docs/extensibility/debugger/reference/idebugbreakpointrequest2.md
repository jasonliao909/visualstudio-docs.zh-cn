---
description: IDebugBreakPointRequest2 接口表示创建和绑定任何类型的断点所需的信息。
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
ms.openlocfilehash: dcf40e4fa60544662b7a825e7ab06825c25809b64d65c74acd3beff6bd8c492f
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121292957"
---
# <a name="idebugbreakpointrequest2"></a>IDebugBreakpointRequest2
此接口表示创建和绑定任何类型的断点所需的信息。

## <a name="syntax"></a>语法

```
IDebugBreakpointRequest2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 会话调试管理器 (SDM) 通常实现此接口。

## <a name="notes-for-callers"></a>调用方说明
 调试引擎 (DE) 通过调用 [CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md) 接收此接口，以便创建挂起断点。 调用 [GetBreakpointRequest](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getbreakpointrequest.md) 可以从 DE 检索此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法 `IDebugBreakpointRequest2` 。

|方法|说明|
|------------|-----------------|
|[GetLocationType](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getlocationtype.md)|获取此断点请求的断点位置类型。|
|[GetRequestInfo](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getrequestinfo.md)|获取描述此断点请求的断点请求信息。|

## <a name="remarks"></a>备注
 在加载正在调试的程序后，调用 [Bind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md) 会将挂起断点绑定到程序中请求的位置。

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)
- [GetBreakpointRequest](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getbreakpointrequest.md)
- [绑定](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)

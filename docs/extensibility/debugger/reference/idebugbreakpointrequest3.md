---
description: IDebugBreakpointRequest3 接口表示创建和绑定任何类型的断点所必需的信息。
title: IDebugBreakpointRequest3 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointRequest3
helpviewer_keywords:
- IDebugBreakpointRequest3
ms.assetid: 8a042beb-b319-48e3-b3c8-9c8336ab371b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 60f3900ccb8b1c502fce9c0af4288fc50ed9a63b2409207fd3a5878e0b6ff9e4
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121292879"
---
# <a name="idebugbreakpointrequest3"></a>IDebugBreakpointRequest3
此接口表示创建和绑定任何类型的断点所必需的信息。 它是 [IDebugBreakpointRequest2 的扩展](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)。

## <a name="syntax"></a>语法

```
IDebugBreakpointRequest3 : IDebugBreakpointRequest2
```

## <a name="notes-for-implementers"></a>实现者说明
 会话调试管理器 (SDM) 通常实现此接口。

## <a name="notes-for-callers"></a>调用方说明
 调试引擎 de (DE) 在调用[CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)时收到的 IDebugBreakpointRequest2 接口上调用[QueryInterface](/cpp/atl/queryinterface)来访问此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了从 [IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)继承的方法外， `IDebugBreakpointRequest3` 接口还公开了以下方法。

|方法|说明|
|------------|-----------------|
|[GetRequestInfo2](../../../extensibility/debugger/reference/idebugbreakpointrequest3-getrequestinfo2.md)|获取描述此断点请求的断点请求信息。|

## <a name="remarks"></a>备注
 此接口用于通过架构结构向 DE [BP_REQUEST_INFO2信息。](../../../extensibility/debugger/reference/bp-request-info2.md) 此附加信息包括 DE 的供应商 ID (GUID 格式) 跟踪点的名称以及断点约束的名称。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)
- [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)

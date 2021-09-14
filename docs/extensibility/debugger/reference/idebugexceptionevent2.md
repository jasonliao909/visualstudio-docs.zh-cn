---
description: 调试引擎 (DE) 将此接口发送到会话调试管理器 (SDM) 当前正在执行的程序中引发异常时。
title: IDebugExceptionEvent2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExceptionEvent2
helpviewer_keywords:
- IDebugExceptionEvent2 interface
ms.assetid: 53d32e59-a84b-4710-833e-c5ab08100516
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 0fe5176217e0c683c2a68b36b0276015ccdc16c0
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664825"
---
# <a name="idebugexceptionevent2"></a>IDebugExceptionEvent2
调试引擎 (DE) 将此接口发送到会话调试管理器 (SDM) 当前正在执行的程序中引发异常时。

## <a name="syntax"></a>语法

```
IDebugExceptionEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 DE 实现此接口以报告正在调试的程序中发生了异常。 必须在与此接口相同的对象上实现 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) 接口。 SDM 使用 [QueryInterface](/cpp/atl/queryinterface) 访问 `IDebugEvent2` 接口。

## <a name="notes-for-callers"></a>调用方说明
 DE 创建并发送此事件对象以报告异常。 事件是使用 SDM 在附加到正在调试的程序时提供的 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) 回调函数发送的。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法 `IDebugExceptionEvent2` 。

|方法|说明|
|------------|-----------------|
|[GetException](../../../extensibility/debugger/reference/idebugexceptionevent2-getexception.md)|获取有关触发此事件的异常的详细信息。|
|[GetExceptionDescription](../../../extensibility/debugger/reference/idebugexceptionevent2-getexceptiondescription.md)|获取触发此事件的异常的可读说明。|
|[CanPassToDebuggee](../../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md)|确定 DE (调试) 是否支持在继续执行时将此异常传递给正在调试的程序的选项。|
|[PassToDebuggee](../../../extensibility/debugger/reference/idebugexceptionevent2-passtodebuggee.md)|指定是应在继续执行时将异常传递给正在调试的程序，还是应放弃异常。|

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="remarks"></a>备注
 在发送事件之前，DE 会检查此异常事件是否已被前一次对 [SetException](../../../extensibility/debugger/reference/idebugengine2-setexception.md)的调用指定为第一机会或第二机会异常。 如果已指定为第一机会异常，则 `IDebugExceptionEvent2` 事件将发送到 SDM。 如果不是，DE 会为应用程序提供处理异常的机会。 如果未提供异常处理程序，并且异常已被指定为第二机会异常，则事件 `IDebugExceptionEvent2` 将发送到 SDM。 否则，DE 将恢复程序执行，操作系统或运行时将处理异常。

## <a name="see-also"></a>另请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [SetException](../../../extensibility/debugger/reference/idebugengine2-setexception.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)

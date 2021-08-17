---
description: 此接口由调试引擎 de (DE) 发送到会话调试管理器 (SDM) 当 DE 已完成截获事件的处理时。
title: IDebugInterceptExceptionCompleteEvent2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugInterceptExceptionCompleteEvent2
helpviewer_keywords:
- IDebugInterceptExceptionCompleteEvent2
ms.assetid: 8ebc256b-5428-4ed6-a505-6aedc8242b8e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: e7f8f49af391bafaa94745fa82c286e762dd2b91
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122096123"
---
# <a name="idebuginterceptexceptioncompleteevent2"></a>IDebugInterceptExceptionCompleteEvent2
此接口由调试引擎 de (DE) 发送到会话调试管理器 (SDM) 当 DE 已完成截获事件的处理时。

## <a name="syntax"></a>语法

```
IDebugInterceptExceptionCompleteEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 DE 实现此接口以报告已截获异常的处理已完成。 必须在与此接口相同的对象上实现 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) 接口。 SDM 使用 [QueryInterface](/cpp/atl/queryinterface) 访问 `IDebugEvent2` 接口。

## <a name="notes-for-callers"></a>调用方说明
 DE 创建并发送此事件对象，以报告已截获异常的完成情况。 事件是通过使用 SDM 在附加到正在调试的程序时提供的 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) 回调函数发送的。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 `IDebugInterceptExceptionCompleteEvent2`接口实现以下方法。

|方法|说明|
|------------|-----------------|
|[GetInterceptCookie](../../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2-getinterceptcookie.md)|返回与已处理的异常关联的唯一值。|

## <a name="remarks"></a>备注
 当该方法成功完成处理截获的异常时 [，InterceptCurrentException](../../../extensibility/debugger/reference/idebugstackframe3-interceptcurrentexception.md) 将发送此事件。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [InterceptCurrentException](../../../extensibility/debugger/reference/idebugstackframe3-interceptcurrentexception.md)

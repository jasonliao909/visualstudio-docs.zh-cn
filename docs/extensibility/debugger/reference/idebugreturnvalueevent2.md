---
description: 此接口由调试引擎 de (DE) 在单步执行或 (SDM) 发送到会话调试管理器。
title: IDebugReturnValueEvent2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugReturnValueEvent2
helpviewer_keywords:
- IDebugReturnValueEvent2
ms.assetid: 2daded43-e427-4fbb-a19e-f3834e3723af
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 8fb0c74c955ba27590916e3b48f801db4f6dc9ec
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122126305"
---
# <a name="idebugreturnvalueevent2"></a>IDebugReturnValueEvent2
此接口由调试引擎 de (DE) 在单步执行或 (SDM) 发送到会话调试管理器。

## <a name="syntax"></a>语法

```
IDebugReturnValueEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 DE 实现此接口，以报告已缩小或超过的函数的返回值。 必须在与此接口相同的对象上实现 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) 接口。 SDM 使用 [QueryInterface](/cpp/atl/queryinterface) 访问 `IDebugEvent2` 接口。

## <a name="notes-for-callers"></a>调用方说明
 DE 创建并发送此事件对象以报告函数的返回值。 事件是通过使用 SDM 在附加到正在调试的程序时提供的 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) 回调函数发送的。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的 方法 `IDebugReturnValueEvent2` 。

|方法|说明|
|------------|-----------------|
|[GetReturnValue](../../../extensibility/debugger/reference/idebugreturnvalueevent2-getreturnvalue.md)|获取单步执行函数时返回的值。|

## <a name="remarks"></a>备注
 可以通过调用 [GetReturnValue](../../../extensibility/debugger/reference/idebugreturnvalueevent2-getreturnvalue.md)来获取函数返回的值。 返回的值将显示在"自动 **"窗口中** 。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)

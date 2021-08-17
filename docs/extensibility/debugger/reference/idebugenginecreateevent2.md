---
description: 调试引擎 (DE) 创建 DE 实例时， (SDM) 将此接口发送到会话调试管理器。
title: IDebugEngineCreateEvent2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngineCreateEvent2
helpviewer_keywords:
- IDebugEngineCreateEvent2 interface
ms.assetid: 37c0a841-1c8d-4802-a990-36b54bca3ef7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: ef22f958783d5450b30b1b0940db043668ae43504ca5e3495ec15b06949f5bab
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121390068"
---
# <a name="idebugenginecreateevent2"></a>IDebugEngineCreateEvent2
调试引擎 (DE) 创建 DE 实例时， (SDM) 将此接口发送到会话调试管理器。

## <a name="syntax"></a>语法

```
IDebugEngineCreateEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 DE 在其正常操作中实现此接口。 必须在与此接口相同的对象上实现 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) 接口 (SDM 使用 方法访问接口 `QueryInterface` `IDebugEvent2`) 。

## <a name="notes-for-callers"></a>调用方说明
 DE 在实例化 DE 后创建并发送此事件对象。 事件是通过使用 SDM 在附加到正在调试的程序时提供的 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) 回调函数发送的。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法 `IDebugEngineCreateEvent2` 。

|方法|说明|
|------------|-----------------|
|[GetEngine](../../../extensibility/debugger/reference/idebugenginecreateevent2-getengine.md)|检索对象，该对象表示 DE (新创建的) 。|

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)

---
description: 当程序 (第) 指令时，调试引擎 DE) 将此接口发送到会话调试管理器 (SDM) 。
title: IDebugEntryPointEvent2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEntryPointEvent2
helpviewer_keywords:
- IDebugEntryPointEvent2 interface
ms.assetid: a15d1cc3-97b7-438c-8d24-c23149708f42
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: b41a6b95f0a7f0a842656e798f21aae1273cfc5a16869399de57d94604f180f0
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121389951"
---
# <a name="idebugentrypointevent2"></a>IDebugEntryPointEvent2
当程序 (第) 指令时，调试引擎 DE) 将此接口发送到会话调试管理器 (SDM) 。

## <a name="syntax"></a>语法

```
IDebugEntryPointEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 DE 在其正常操作中实现此接口。 必须在与此接口相同的对象上实现 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) 接口。 SDM 使用 [QueryInterface](/cpp/atl/queryinterface) 访问 `IDebugEvent2` 接口。

## <a name="notes-for-callers"></a>调用方说明
 当正在调试的程序已加载并准备好执行用户代码的第一个指令时，DE 将创建并发送此事件对象。 事件是通过使用 SDM 在附加到正在调试的程序时提供的 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) 回调函数发送的。

## <a name="remarks"></a>备注
- 当程序即将执行第一个指令时，将发送[IDebugLoadCompleteEvent2。](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md) 例如， `IDebugEntryPoint2` 在程序即将执行用户函数时 `main` 发送。

 当 DE 发送 `IDebugEntryPointEvent2` 时，当前代码位置应位于用户代码的第一个指令，如 `main` 。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md)

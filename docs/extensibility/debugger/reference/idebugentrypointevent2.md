---
description: 当程序要执行用户代码的第一个指令时，调试引擎 (DE) 将此接口发送到会话调试管理器 (SDM) 。
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
ms.openlocfilehash: 041d8f7d4237504ff0201bd0b5069293c0b59d63
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122089129"
---
# <a name="idebugentrypointevent2"></a>IDebugEntryPointEvent2
当程序要执行用户代码的第一个指令时，调试引擎 (DE) 将此接口发送到会话调试管理器 (SDM) 。

## <a name="syntax"></a>语法

```
IDebugEntryPointEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 DE 实现此接口作为其常规操作的一部分。 必须在与此接口相同的对象上实现 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) 接口。 SDM 使用 [QueryInterface](/cpp/atl/queryinterface) 访问 `IDebugEvent2` 接口。

## <a name="notes-for-callers"></a>调用方说明
 当正在调试的程序已加载并且已准备好执行用户代码的第一个指令时，DE 将创建并发送此事件对象。 使用 SDM 在附加到正在调试的程序时提供的 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) 回调函数发送事件。

## <a name="remarks"></a>备注
- 当程序将要执行第一个指令时，将发送[IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md) 。 例如，在 `IDebugEntryPoint2` 程序即将执行用户的函数时发送 `main` 。

 当取消发送时 `IDebugEntryPointEvent2` ，当前代码位置应位于用户代码的第一个指令上，如 `main` 。

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md)

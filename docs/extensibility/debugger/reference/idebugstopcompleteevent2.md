---
description: DE () 引擎可以在程序停止时 (SDM) 向会话调试管理器发送此可选事件。
title: IDebugStopCompleteEvent2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugStopCompleteEvent2 interface
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: f4a9531ba34729e6cdff78793520a9b3ba8d2d5312b90b2f75e7602ede1cdcb3
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121448814"
---
# <a name="idebugstopcompleteevent2"></a>IDebugStopCompleteEvent2

DE () 引擎可以在程序停止时 (SDM) 向会话调试管理器发送此可选事件。

## <a name="syntax"></a>语法

```
IDebugStopCompleteEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明

此接口是在 2005 Visual Studio引入的。 以前的版本不支持异步停止。

- [在](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md) 多进程或多程序方案中，SDM 调用 Stop。 当一个程序向 SDM 发送停止事件时，SDM 也请求其他程序停止。

Stop 用于异步通知 SDM 程序已停止。 通知 SDM 对于解释器调试引擎非常有用，有时调试程序内没有代码运行，因此无法同步完成停止。 [](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md) 如果调试引擎想要采用此异步通知，则必须从停止 返回 `S_ASYNC_STOP` 。 [](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md)

## <a name="requirements"></a>要求

标头：msdbg.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

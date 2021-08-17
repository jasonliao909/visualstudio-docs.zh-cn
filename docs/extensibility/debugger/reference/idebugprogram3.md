---
description: 此接口表示在进程中运行的程序，并通过提供线程信息来扩展执行。
title: IDebugProgram3 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProgram3 interface
ms.assetid: 4301ba23-c00c-4ce5-8b1e-3f27da312034
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 8e1de2b61e7a942853cd0bae0d5526820030a4701921482a4aeb979cbfe96a2d
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121338821"
---
# <a name="idebugprogram3"></a>IDebugProgram3
此接口表示在进程中运行的程序，并通过提供线程信息来扩展 [执行](../../../extensibility/debugger/reference/idebugprogram2-execute.md) 。

## <a name="syntax"></a>语法

```
IDebugProgram3 : IDebugProgram3
```

## <a name="notes-for-implementers"></a>实施者注意事项
 调试引擎 (DE) ，自定义端口供应商实现此接口来表示进程中的程序。 会话调试管理器 (SDM) 还实现此接口以提供要 [附加](../../../extensibility/debugger/reference/idebugprogram2-attach.md)的信息。

## <a name="notes-for-callers"></a>调用方说明
 [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)事件将为新程序返回此接口。 此接口还可用作多个接口上许多方法的参数。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法 `IDebugProgram3` 。

|方法|说明|
|------------|-----------------|
|[ExecuteOnThread](../../../extensibility/debugger/reference/idebugprogram3-executeonthread.md)|执行程序。 返回线程，以向调试器显示用户在执行时查看的线程的信息。|

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="remarks"></a>备注
 程序是在特定运行时结构中运行的线程容器，而进程由一个或多个程序组成。

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [GetProgram](../../../extensibility/debugger/reference/idebugthread2-getprogram.md)
- [下一页](../../../extensibility/debugger/reference/ienumdebugprograms2-next.md)
- [事件](../../../extensibility/debugger/reference/idebugportevents2-event.md)
- [附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)
- [DestroyProgram](../../../extensibility/debugger/reference/idebugengine2-destroyprogram.md)
- [事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
- [Attach_V7](../../../extensibility/debugger/reference/idebugprogramnode2-attach-v7.md)

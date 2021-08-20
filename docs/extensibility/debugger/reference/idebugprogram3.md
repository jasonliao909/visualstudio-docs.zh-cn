---
description: 此接口表示在进程中运行的程序，通过提供线程信息来扩展 Execute。
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
ms.openlocfilehash: 14a7641542bb5392c4e8eba1196059b5b8136948
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122159732"
---
# <a name="idebugprogram3"></a>IDebugProgram3
此接口表示在进程中运行的程序，通过提供线程信息来扩展[Execute。](../../../extensibility/debugger/reference/idebugprogram2-execute.md)

## <a name="syntax"></a>语法

```
IDebugProgram3 : IDebugProgram3
```

## <a name="notes-for-implementers"></a>实现者说明
 调试引擎 (DE) ，自定义端口供应商实现此接口来表示进程中的程序。 SDM (会话) 也实现此接口以提供附加 [的信息](../../../extensibility/debugger/reference/idebugprogram2-attach.md)。

## <a name="notes-for-callers"></a>调用方说明
 [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)事件返回新程序的此接口。 此接口还用作多个接口上许多方法的参数。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法 `IDebugProgram3` 。

|方法|说明|
|------------|-----------------|
|[ExecuteOnThread](../../../extensibility/debugger/reference/idebugprogram3-executeonthread.md)|执行程序。 返回线程以向调试器提供用户在执行时正在查看的线程的信息。|

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="remarks"></a>备注
 程序是运行于特定运行时体系结构中的线程容器，而进程由一个或多个程序进行。

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

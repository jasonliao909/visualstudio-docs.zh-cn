---
description: 此接口由调试引擎 de (DE) 发送到会话调试管理器 (SDM) 程序附加到时。
title: IDebugProgramCreateEvent2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramCreateEvent2
helpviewer_keywords:
- IDebugProgramCreateEvent2 interface
ms.assetid: b19a7934-6179-4a68-9075-bd7dcd640b05
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 9f6d4db4ed0b2a732fc216938c616cd64963d94cb2d4878e731fae1e89c8bb84
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121338808"
---
# <a name="idebugprogramcreateevent2"></a>IDebugProgramCreateEvent2
此接口由调试引擎 de (DE) 发送到会话调试管理器 (SDM) 程序附加到时。

## <a name="syntax"></a>语法

```
IDebugProgramCreateEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 DE 或自定义端口供应商实现此接口来报告程序已创建，通常是在程序附加到时。 必须在与此接口相同的对象上实现 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) 接口。 SDM 使用 `QueryInterface` 方法访问 `IDebugEvent2` 接口。

## <a name="notes-for-callers"></a>调用方说明
 DE 或自定义端口供应商创建并发送此事件对象以报告程序的创建。 DE 通过使用 SDM 在附加到正在调试的程序时提供的 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) 回调函数发送此事件。 自定义端口供应商使用 [IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md) 接口发送此事件。

## <a name="remarks"></a>备注
 DE 或自定义端口供应商通过调用[PublishProgramNode](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogramnode.md)发布新的[IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)接口。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)

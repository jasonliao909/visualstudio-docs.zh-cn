---
description: 当程序附加到时，调试引擎会将此接口 (DE) 发送到会话调试管理器 (SDM) 。
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
ms.openlocfilehash: b778bf5a3267bf95895825b5dd6cc09aa428e3a8
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122126461"
---
# <a name="idebugprogramcreateevent2"></a>IDebugProgramCreateEvent2
当程序附加到时，调试引擎会将此接口 (DE) 发送到会话调试管理器 (SDM) 。

## <a name="syntax"></a>语法

```
IDebugProgramCreateEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 "DE" 或 "自定义" 端口供应商实现此接口，报告已创建程序，通常是在程序附加到时。 必须在与此接口相同的对象上实现 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) 接口。 SDM 使用 `QueryInterface` 方法来访问 `IDebugEvent2` 接口。

## <a name="notes-for-callers"></a>调用方说明
 DE 或自定义端口提供程序将创建并发送此事件对象，以报告程序的创建。 DE 在附加到正在调试的程序时，使用 SDM 提供的 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) 回调函数发送此事件。 自定义端口供应商使用 [IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md) 接口发送此事件。

## <a name="remarks"></a>备注
 DE 或自定义端口提供程序通过调用[PublishProgramNode](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogramnode.md)发布新的[IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)接口。

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)

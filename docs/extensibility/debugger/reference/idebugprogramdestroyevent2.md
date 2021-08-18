---
description: 当程序运行到完成 (时，) 调试引擎 (SDM) 将此接口发送到会话调试管理器。
title: IDebugProgramDestroyEvent2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramDestroyEvent2
helpviewer_keywords:
- IDebugProgramDestroyEvent2
ms.assetid: ddf127ca-c4a5-4071-90ca-68faf2f57dbd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: abe928021b966b64234370be515528fe920e5521
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122132712"
---
# <a name="idebugprogramdestroyevent2"></a>IDebugProgramDestroyEvent2
当程序运行到完成 (时，) 调试引擎 (SDM) 将此接口发送到会话调试管理器。

## <a name="syntax"></a>语法

```
IDebugProgramDestroyEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 DE 或自定义端口供应商实现此接口以报告程序已终止且不再可用于调试。 必须在与此接口相同的对象上实现 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) 接口。 SDM 使用 [QueryInterface](/cpp/atl/queryinterface) 访问 `IDebugEvent2` 接口。

## <a name="notes-for-callers"></a>调用方说明
 DE 或自定义端口供应商创建并发送此事件对象以报告程序的终止。 DE 通过使用 SDM 在附加到正在调试的程序时提供的 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) 回调函数发送此事件。 自定义端口供应商使用 [IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md) 接口发送此事件。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的 方法 `IDebugProgramDestroyEvent2` 。

|方法|说明|
|------------|-----------------|
|[GetExitCode](../../../extensibility/debugger/reference/idebugprogramdestroyevent2-getexitcode.md)|获取程序的退出代码。|

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)

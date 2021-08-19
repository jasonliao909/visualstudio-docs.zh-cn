---
description: 此接口表示 DE (调试) 。
title: IDebugEngine2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2
helpviewer_keywords:
- IDebugEngine2 interface
ms.assetid: 1f0e9ac0-6dfb-461a-976c-888d82144cdb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: bacc450f29e950f5fd2d339244ad3715dead711a
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122089181"
---
# <a name="idebugengine2"></a>IDebugEngine2
此接口表示 DE (调试) 。 它用于管理调试会话的各个方面，从创建断点到设置和清除异常。

## <a name="syntax"></a>语法

```
IDebugEngine2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 此接口由自定义 DE 实现，用于管理程序调试。 此接口必须由 DE 实现。

## <a name="notes-for-callers"></a>调用方说明
 此接口由会话调试管理器 (SDM) 调用，以管理调试会话，包括管理异常、创建断点和响应 DE 发送的同步事件。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法 `IDebugEngine2` 。

|方法|说明|
|------------|-----------------|
|[EnumPrograms](../../../extensibility/debugger/reference/idebugengine2-enumprograms.md)|为 DE 正在调试的所有程序创建枚举器。|
|[附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)|将 DE 附加到程序。|
|[CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)|在 DE 中创建挂起的断点。|
|[SetException](../../../extensibility/debugger/reference/idebugengine2-setexception.md)|指定 DE 应如何处理给定的异常。|
|[RemoveSetException](../../../extensibility/debugger/reference/idebugengine2-removesetexception.md)|删除指定的异常，以便调试引擎不再处理它。|
|[RemoveAllSetExceptions](../../../extensibility/debugger/reference/idebugengine2-removeallsetexceptions.md)|删除 IDE 为特定运行时体系结构或语言设置的异常列表。|
|[GetEngineID](../../../extensibility/debugger/reference/idebugengine2-getengineid.md)|获取 DE 的 GUID。|
|[DestroyProgram](../../../extensibility/debugger/reference/idebugengine2-destroyprogram.md)|通知 DE 指定的程序已以非典型方式终止，并且 DE 应清除对该程序的所有引用并发送程序销毁事件。|
|[ContinueFromSynchronousEvent](../../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md)|由 SDM 调用，以指示已接收并处理 DE 以前发送到 SDM 的同步调试事件。|
|[SetLocale](../../../extensibility/debugger/reference/idebugengine2-setlocale.md)|设置 DE 区域设置。|
|[SetRegistryRoot](../../../extensibility/debugger/reference/idebugengine2-setregistryroot.md)|设置 DE 当前使用的注册表根。|
|[SetMetric](../../../extensibility/debugger/reference/idebugengine2-setmetric.md)|设置指标。|
|[CauseBreak](../../../extensibility/debugger/reference/idebugengine2-causebreak.md)|请求此 DE 调试的所有程序在下次尝试运行时停止执行。|

## <a name="requirements"></a>要求
 标头：Msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
- [GetEngine](../../../extensibility/debugger/reference/idebugenginecreateevent2-getengine.md)

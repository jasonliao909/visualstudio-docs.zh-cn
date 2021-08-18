---
description: 此接口提供多线程调试支持。
title: IDebugEngineProgram2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngineProgram2
helpviewer_keywords:
- IDebugEngineProgram2 interface
ms.assetid: 151003a9-2e4d-4acf-9f4d-365dfa6b9596
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 8c2660c430ac18f337c61275297eb385216904cf
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122035145"
---
# <a name="idebugengineprogram2"></a>IDebugEngineProgram2
此接口提供多线程调试支持。

## <a name="syntax"></a>语法

```
IDebugEngineProgram2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 调试引擎实现此接口以支持同时调试多个线程。 此接口在实现 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) 接口的同一对象上实现。

## <a name="notes-for-callers"></a>调用方说明
 使用 [QueryInterface](/cpp/atl/queryinterface) 从接口获取此 `IDebugProgram2` 接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法 `IDebugEngineProgram2` 。

|方法|说明|
|------------|-----------------|
|[停止](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md)|停止此程序中运行的所有线程。|
|[WatchForThreadStep](../../../extensibility/debugger/reference/idebugengineprogram2-watchforthreadstep.md)|监视执行 (或停止监视) 线程上发生的执行事件。|
|[WatchForExpressionEvaluationOnThread](../../../extensibility/debugger/reference/idebugengineprogram2-watchforexpressionevaluationonthread.md)|允许 (或不允许) 给定线程上发生表达式计算，即使程序已停止。|

## <a name="remarks"></a>备注
 Visual Studio调用此接口以响应[IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)事件，并设置程序的"监视线程步骤"和"监视线程上的表达式计算"状态。 [每当](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md) 要停止程序时，都会调用 Stop;此方法使程序有机会终止所有线程。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)

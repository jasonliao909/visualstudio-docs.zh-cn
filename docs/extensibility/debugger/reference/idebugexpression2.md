---
description: 此接口表示已准备好进行绑定和评估的已分析表达式。
title: IDebugExpression2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpression2
helpviewer_keywords:
- IDebugExpression2 interface
ms.assetid: f5e4b124-1e30-47c8-a511-80084a02dba5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: e9f9772b808181a0049d335bc850faaecacdadf5
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122088986"
---
# <a name="idebugexpression2"></a>IDebugExpression2
此接口表示已准备好进行绑定和评估的已分析表达式。

## <a name="syntax"></a>语法

```
IDebugExpression2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 调试引擎 (DE) 实现此接口，以表示已准备好评估的已分析表达式。

## <a name="notes-for-callers"></a>调用方说明
 对 [ParseText 的调用](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) 将返回此接口。 [GetExpressionContext](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md) 返回 [IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md) 接口。 只有在正在调试的程序已暂停且堆栈帧可用时，才能访问这些接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法 `IDebugExpression2` 。

|方法|说明|
|------------|-----------------|
|[EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)|异步计算此表达式。|
|[中止](../../../extensibility/debugger/reference/idebugexpression2-abort.md)|结束异步表达式计算。|
|[EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)|同步计算此表达式。|

## <a name="remarks"></a>备注
 当程序停止时，会话调试管理器 (SDM) 调用 [EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)从 DE 获取堆栈帧。 然后，SDM 调用 [GetExpressionContext](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md) 获取 [IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md) 接口。 随后调用 [ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) 以创建 接口，该接口表示已准备好计算已分析 `IDebugExpression2` 的表达式。

 SDM 调用 [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) 或 [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) 以实际计算表达式并生成值。

 在 的实现中，DE 使用 COM 的 函数实例化表达式计算程序并获取 `IDebugExpressionContext2::ParseText` `CoCreateInstance` [IDebugExpressionEvaluator](../../../extensibility/debugger/reference/idebugexpressionevaluator.md) 接口 (请参阅接口中的 `IDebugExpressionEvaluator`) 。 然后，DE 调用 [Parse](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md) 以获取 [IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md) 接口。 此接口在 和 的实现 `IDebugExpression2::EvaluateSync` 中 `IDebugExpression2::EvaluateAsync` 用于执行计算。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetExpression](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getexpression.md)

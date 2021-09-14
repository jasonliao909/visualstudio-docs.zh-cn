---
description: 获取堆栈帧和线程的当前上下文中表达式计算的评估上下文。
title: IDebugStackFrame2：：GetExpressionContext |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame2::GetExpressionContext
helpviewer_keywords:
- IDebugStackFrame2::GetExpressionContext
ms.assetid: a2604e6a-502d-473b-868f-b11ac64c7a35
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d95af977f77bc48a112d584d613877d3259bdb90
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664435"
---
# <a name="idebugstackframe2getexpressioncontext"></a>IDebugStackFrame2::GetExpressionContext
获取堆栈帧和线程的当前上下文中表达式计算的评估上下文。

## <a name="syntax"></a>语法

```cpp
HRESULT GetExpressionContext ( 
   IDebugExpressionContext2** ppExprCxt
);
```

```csharp
int GetExpressionContext ( 
   out IDebugExpressionContext2 ppExprCxt
);
```

## <a name="parameters"></a>parameters
`ppExprCxt`\
[out]返回表示 [表达式计算上下文的 IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md) 对象。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 通常，可以将表达式计算上下文视为执行表达式计算的范围。 调用 [ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) 方法来分析表达式，然后调用生成的 [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) 或 [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) 方法来计算分析的表达式。

## <a name="see-also"></a>另请参阅
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md)
- [ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)
- [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)
- [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)

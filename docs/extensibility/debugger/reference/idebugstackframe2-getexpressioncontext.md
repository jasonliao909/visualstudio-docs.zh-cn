---
description: 获取堆栈帧和线程的当前上下文中的表达式计算的计算上下文。
title: IDebugStackFrame2：： GetExpressionContext |Microsoft Docs
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
ms.openlocfilehash: 97894a07c593a9793f898a7a44b59b5f9f87692c7b0e740b6ace6ce502e8cc57
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121338444"
---
# <a name="idebugstackframe2getexpressioncontext"></a>IDebugStackFrame2::GetExpressionContext
获取堆栈帧和线程的当前上下文中的表达式计算的计算上下文。

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

## <a name="parameters"></a>参数
`ppExprCxt`\
弄返回一个 [IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md) 对象，该对象表示表达式计算的上下文。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 通常，可以将表达式计算上下文视为用于执行表达式计算的作用域。 调用 [ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) 方法以分析表达式，然后调用生成的 [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) 或 [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) 方法来计算分析后的表达式。

## <a name="see-also"></a>请参阅
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md)
- [ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)
- [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)
- [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)

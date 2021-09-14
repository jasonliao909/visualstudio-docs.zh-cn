---
description: 此方法取消异步表达式计算，因为调用 EvaluateAsync) 方法。
title: IDebugExpression2：：Abort |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpression2::Abort
helpviewer_keywords:
- IDebugExpression2::Abort
ms.assetid: 4fcb712e-1bdb-4b75-a440-35cc79ee147e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: be5637b350e9448b5c02ede5087fed6c2df26bb4
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664824"
---
# <a name="idebugexpression2abort"></a>IDebugExpression2::Abort
此方法取消通过调用 [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) 方法启动的异步表达式计算。

## <a name="syntax"></a>语法

```cpp
HRESULT Abort(
   void
);
```

```csharp
int Abort();
```

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 取消异步表达式计算时，不要将 [IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md) 事件发送到传递给 [Attach](../../../extensibility/debugger/reference/idebugprogram2-attach.md) 或 [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) 方法的事件回调。

## <a name="see-also"></a>另请参阅
- [IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md)
- [IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)
- [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)

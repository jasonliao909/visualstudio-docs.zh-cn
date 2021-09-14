---
description: 此方法异步计算表达式。
title: IDebugExpression2：：EvaluateAsync |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpression2::EvaluateAsync
helpviewer_keywords:
- IDebugExpression2::EvaluateAsync
ms.assetid: 848fe6cb-0759-42f2-890b-d2b551c527d6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ad7d4c41aae0b1d48502fdb19865e737004696ae
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664818"
---
# <a name="idebugexpression2evaluateasync"></a>IDebugExpression2::EvaluateAsync
此方法异步计算表达式。

## <a name="syntax"></a>语法

```cpp
HRESULT EvaluateAsync (
    EVALFLAGS             dwFlags,
    IDebugEventCallback2* pExprCallback
);
```

```csharp
int EvaluateAsync(
    enum_EVALFLAGS       dwFlags,
    IDebugEventCallback2 pExprCallback
);
```

## <a name="parameters"></a>parameters
`dwFlags`\
[in]来自控制表达式评估的 [EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md) 枚举的标志的组合。

`pExprCallback`\
[in]此参数始终为 null 值。

## <a name="return-value"></a>返回值
如果成功，则返回 `S_OK` ;否则返回错误代码。 典型的错误代码是：

|错误|说明|
|-----------|-----------------|
|E_EVALUATE_BUSY_WITH_EVALUATION|当前正在计算另一个表达式，并且不支持同时进行表达式计算。|

## <a name="remarks"></a>备注
此方法应在开始表达式计算后立即返回。 成功计算表达式后，必须通过 Attach 或 Attach 向[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)事件回调发送[IDebugExpressionEvaluationCompleteEvent2。](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md) [](../../../extensibility/debugger/reference/idebugprogram2-attach.md) [](../../../extensibility/debugger/reference/idebugengine2-attach.md)

## <a name="example"></a>示例
下面的示例演示如何为实现 `CExpression` [IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md) 接口的简单对象实现此方法。

```cpp
HRESULT CExpression::EvaluateAsync(EVALFLAGS dwFlags,
                                   IDebugEventCallback2* pExprCallback)
{
    // Set the aborted state to FALSE
    // in case the user tries to redo the evaluation after aborting.
    m_bAborted = FALSE;
    // Post the WM_EVAL_EXPR message in the message queue of the current thread.
    // This starts the expression evaluation on a background thread.
    PostThreadMessage(GetCurrentThreadId(), WM_EVAL_EXPR, 0, (LPARAM) this);
    return S_OK;
}
```

## <a name="see-also"></a>另请参阅
- [IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md)
- [IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)
- [EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)

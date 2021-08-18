---
title: 中断模式下的表达式计算 |Microsoft Docs
description: 了解调试器处于中断模式下时所发生的过程，并且必须执行表达式计算。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- break mode, expression evaluation
- debugging [Debugging SDK], expression evaluation
- expression evaluation, break mode
ms.assetid: 34fe5b58-15d5-4387-a266-72120f90a4b6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 7dbf82e8586dbd12b99b2c360b1da3fb021133d6
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122089428"
---
# <a name="expression-evaluation-in-break-mode"></a>中断模式下的表达式计算
以下部分介绍调试器处于中断模式时，必须执行表达式计算的过程。

## <a name="expression-evaluation-process"></a>表达式计算过程
 下面是对表达式进行计算时所涉及的基本步骤：

1. 会话调试管理器 (SDM) 调用 [IDebugStackFrame2：： GetExpressionContext](../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md) 以获取表达式上下文接口 [IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md)。

2. 然后，SDM 用要分析的字符串调用 [IDebugExpressionContext2：:P arsetext](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) 。

3. 如果 ParseText 未返回 S_OK，则返回错误原因。

     本来

     如果 ParseText 返回 S_OK，则 SDM 可以调用 [IDebugExpression2：： EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) 或 [IDebugExpression2：： EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) 来从分析的表达式中获取最终值。

    - 使用时 `IDebugExpression2::EvaluateSync` ，给定的回调接口会传达正在进行的计算过程。 在 [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) 接口中返回最终值。

    - 使用时 `IDebugExpression2::EvaluateAsync` ，给定的回调接口会传达正在进行的计算过程。 完成评估后，EvaluateAsync 将通过回调发送 [IDebugExpressionEvaluationCompleteEvent2](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md) 接口。 对于此事件接口，最终值为 [GetResult](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getresult.md)。

## <a name="see-also"></a>请参阅
- [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md)

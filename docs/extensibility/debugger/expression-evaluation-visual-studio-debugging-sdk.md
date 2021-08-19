---
title: 表达式计算 (Visual Studio调试 SDK) |Microsoft Docs
description: 在中断模式下，IDE 计算涉及程序变量的表达式。 了解调试引擎如何分析和计算表达式。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation
ms.assetid: 5044ced5-c18c-4534-b0bf-cc3e50cd57ac
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 3c362b03dd6da91630b324fd659f0977c15a96c0
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122043578"
---
# <a name="expression-evaluation-visual-studio-debugging-sdk"></a>调试 SDK (Visual Studio表达式) 
在中断模式下，IDE 必须计算涉及多个程序变量的简单表达式。 若要完成其计算， (DE) 必须分析和计算输入到 IDE 窗口之一的表达式。

 表达式是使用 [IDebugExpressionContext2：:P arseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) 方法创建的，由生成的 [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) 接口表示。

 **IDebugExpression2** 接口由 DE 实现，并调用其 **EvalAsync** 方法将 [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)接口返回到 IDE，以便显示 IDE 中表达式计算的结果。 [IDebugProperty2：：GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) 返回一个 结构，该结构用于将表达式的值放入 **"监视** "窗口或" **局部区域"** 窗口中。

 调试包或会话调试管理器 (SDM) 调用 [IDebugExpression2：：EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) 或 [EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) 获取表示评估结果的 [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) 接口。 `IDebugProperty2` 具有返回表达式的名称、类型和值的方法。 此信息显示在各种调试器窗口中。

## <a name="using-expression-evaluation"></a>使用表达式计算
 若要使用表达式计算，必须实现 [IDebugExpressionContext2：:P arseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) 方法和 [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) 接口的所有方法，如下表所示。

|方法|说明|
|------------|-----------------|
|[EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)|异步计算表达式。|
|[中止](../../extensibility/debugger/reference/idebugexpression2-abort.md)|结束异步表达式计算。|
|[EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)|同步计算表达式。|

 同步和异步评估需要实现 [IDebugProperty2：：GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) 方法。 异步表达式计算需要 [实现 IDebugExpressionEvaluationCompleteEvent2](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)。

## <a name="see-also"></a>请参阅
- [执行控制和状态评估](../../extensibility/debugger/execution-control-and-state-evaluation.md)

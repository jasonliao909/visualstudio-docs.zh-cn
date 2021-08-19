---
title: 计算表达式|Microsoft Docs
description: 了解如何计算表达式，这些表达式是使用从"自动"、监视、"快速监视"或"即时"窗口向下传递的字符串创建的。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- expressions [Debugging SDK], evaluating
- debugging [Debugging SDK], expression evaluation
- expression evaluation
ms.assetid: 5ccfcc80-dea5-48a1-8bae-6a26f8d3bc56
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 142c5d195990e87a7741fbbbe0eeef4a7020c63a
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122080333"
---
# <a name="evaluate-expressions"></a>计算表达式
表达式基于从"自动"、"监视 **"、"快速** 监视"或"即时"窗口 **向下传递的字符串** 创建。 计算表达式时，它将生成一个可打印字符串，其中包含变量或参数的名称和类型及其值。 此字符串显示在相应的 IDE 窗口中。

## <a name="implementation"></a>实现
 当程序在断点处停止时，将计算表达式。 表达式本身由 [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) 接口表示，该接口表示已准备好在给定表达式计算上下文中进行绑定和评估的已分析表达式。 堆栈帧确定表达式计算上下文，调试引擎 (DE) [IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md) 接口提供。

 给定用户字符串和[IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md)接口后，调试引擎 (DE) 可以通过将用户字符串传递给[IDebugExpressionContext2：:P arseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)方法来获取[IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)接口。 返回的 IDebugExpression2 接口包含已分析的表达式，可供计算。

 借助 `IDebugExpression2` 接口，DE 可以使用 [IDebugExpression2：：EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) 或 [IDebugExpression2：：EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)通过同步或异步表达式计算获取表达式的值。 此值以及变量或参数的名称和类型将发送到 IDE 进行显示。 值、名称和类型由 [IDebugProperty2 接口](../../extensibility/debugger/reference/idebugproperty2.md) 表示。

 若要启用表达式计算，DE 必须实现 [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) 和 [IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md) 接口。 同步和异步评估都需要 [实现 IDebugProperty2：：GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) 方法。

## <a name="see-also"></a>请参阅
- [堆栈帧](../../extensibility/debugger/stack-frames.md)
- [表达式计算上下文](../../extensibility/debugger/expression-evaluation-context.md)
- [调试任务](../../extensibility/debugger/debugging-tasks.md)

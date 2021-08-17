---
title: 表达式计算器体系结构 |Microsoft Docs
description: 了解如何将专用语言集成到 Visual Studio 调试包，包括表达式计算器和符号提供程序/联编程序接口。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- architecture, expression evaluators
- expression evaluators, architecture
- debugging [Debugging SDK], expression evaluators
ms.assetid: aad7c4c6-1dc1-4d32-b975-f1fdf76bdeda
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 7a1d394cf9b985c1b239b0184f7fa3580c7775537c3e1b8b3beba4c48447e59f
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121417803"
---
# <a name="expression-evaluator-architecture"></a>表达式计算器体系结构
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式计算器的方法已弃用。 有关实现 CLR 表达式计算器的信息，请参阅 [CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 将专有语言集成到 Visual Studio 调试包意味着必须设置所需的表达式计算器 (企业版) 接口并调用公共语言运行时符号提供程序 (SP) 和联编程序接口。 SP 和联编程序对象与当前执行地址一起是在其中计算表达式的上下文。 这些接口生成和使用的信息表示企业版的体系结构中的关键概念。

## <a name="overview"></a>概述

### <a name="parse-the-expression"></a>分析表达式
 在调试程序时，将计算表达式的原因有很多，但在断点处停止正在调试的程序时， (由用户或异常) 导致的断点。 此时 Visual Studio 从调试引擎 (DE) 中获取[IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md)接口所表示的堆栈帧。 然后 Visual Studio 调用[GetExpressionContext](../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md)来获取[IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md)接口。 此接口表示可在其中计算表达式的上下文; [ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) 是评估过程的入口点。 直到此点为止，所有接口都是通过 DE 实现的。

 `IDebugExpressionContext2::ParseText`调用时，将对与 (发生断点的源文件的语言相关联的企业版进行实例化，此时还会在此点) 初始化 SH。 企业版由[IDebugExpressionEvaluator](../../extensibility/debugger/reference/idebugexpressionevaluator.md)接口表示。 然后，取消调用 [Parse](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md) ，以将文本格式) 的 (表达式转换为分析后的表达式，以便进行评估。 此分析的表达式由 [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md) 接口表示。 通常会分析表达式，此时不会计算该表达式。

 DE 会创建一个实现 [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) 接口的对象，将该 `IDebugParsedExpression` 对象放入对象中 `IDebugExpression2` ，并从返回 `IDebugExpression2` 对象 `IDebugExpressionContext2::ParseText` 。

### <a name="evaluate-the-expression"></a>计算表达式
 Visual Studio 调用[EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)或[EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)来计算分析后的表达式。 这两种方法都调用 [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) (`IDebugExpression2::EvaluateSync` 立即调用方法，同时 `IDebugExpression2::EvaluateAsync` 通过后台线程调用方法) 计算分析的表达式并返回表示已分析表达式的值和类型的 [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) 接口。 `IDebugParsedExpression::EvaluateSync` 使用提供的 SH、address 和联编程序将已分析的表达式转换为实际值，并由 `IDebugProperty2` 接口表示。

### <a name="for-example"></a>例如
 在正在运行的程序中命中断点后，用户可以选择在 " **快速监视** " 对话框中查看变量。 此对话框显示变量的名称、值和类型。 用户通常可以更改值。

 显示 " **快速监视** " 对话框时，要检查的变量的名称将作为文本发送到 [ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)。 这会返回一个 [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) 对象，该对象表示已分析的表达式（在本例中为变量）。 然后，调用[EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)以生成一个 `IDebugProperty2` 对象，该对象表示变量的值和类型以及其名称。 此时会显示此信息。

 如果用户更改变量的值，则将使用新值调用 [SetValueAsString](../../extensibility/debugger/reference/idebugproperty2-setvalueasstring.md) ，这会更改内存中变量的值，因此在程序恢复运行时将使用它。

 有关显示变量值的此过程的更多详细信息，请参阅 [显示局部变量](../../extensibility/debugger/displaying-locals.md) 。 有关如何更改变量的值的更多详细信息，请参阅 [更改本地的值](../../extensibility/debugger/changing-the-value-of-a-local.md) 。

## <a name="in-this-section"></a>本节内容
 [计算上下文](../../extensibility/debugger/evaluation-context.md)提供在 DE 调用企业版时传递的参数。

 [键表达式计算器接口](../../extensibility/debugger/key-expression-evaluator-interfaces.md)描述在写入企业版时所需的关键接口以及计算上下文。

## <a name="see-also"></a>请参阅
- [编写 CLR 表达式计算器](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
- [显示局部变量](../../extensibility/debugger/displaying-locals.md)
- [更改局部变量值](../../extensibility/debugger/changing-the-value-of-a-local.md)

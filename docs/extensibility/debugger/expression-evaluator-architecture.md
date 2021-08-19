---
title: 表达式评估器体系结构|Microsoft Docs
description: 了解如何将专有语言集成到Visual Studio包中，包括表达式计算程序以及符号提供程序/联编程序接口。
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
ms.openlocfilehash: ccfab88361d1fdc23f11839a59c2c56f959a5b75
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122153506"
---
# <a name="expression-evaluator-architecture"></a>表达式评估器体系结构
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式计算器的方法已弃用。 有关实现 CLR 表达式计算器的信息，请参阅 [CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 将专有语言集成到 Visual Studio 调试包中意味着必须设置所需的表达式计算程序 (企业版) 接口，并调用公共语言运行时符号提供程序 (SP) 和联编程序接口。 SP 和联编程序对象以及当前执行地址是计算表达式的上下文。 这些接口生成和使用的信息表示接口体系结构中的关键企业版。

## <a name="overview"></a>概述

### <a name="parse-the-expression"></a>分析表达式
 调试程序时，将出于许多原因计算表达式，但始终在断点处停止调试的程序时 (用户放置的断点或由异常) 。 此时，Visual Studio从调试引擎和 DE) 获取堆栈帧（由[IDebugStackFrame (2](../../extensibility/debugger/reference/idebugstackframe2.md)接口表示）。 Visual Studio调用[GetExpressionContext](../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md)获取[IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md)接口。 此接口表示可在其中计算表达式的上下文; [ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) 是计算过程的入口点。 到目前为止，所有接口都由 DE 实现。

 调用 时，DE 会实例化企业版发生断点的源文件的语言关联的 (DE 此时也会实例化 `IDebugExpressionContext2::ParseText` SH) 。 该企业版由[IDebugExpressionEvaluator](../../extensibility/debugger/reference/idebugexpressionevaluator.md)接口表示。 然后，DE 调用 [Parse，](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md) 将文本格式 (表达式转换为) 表达式，并准备好进行计算。 此分析表达式由 [IDebugParsedExpression 接口](../../extensibility/debugger/reference/idebugparsedexpression.md) 表示。 表达式通常会进行分析，此时不会计算。

 DE 创建一个实现 [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) 接口的对象，将该对象放入 对象，然后 `IDebugParsedExpression` `IDebugExpression2` 从 `IDebugExpression2` 返回该对象 `IDebugExpressionContext2::ParseText` 。

### <a name="evaluate-the-expression"></a>计算表达式
 Visual Studio [EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)或[EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)来计算分析的表达式。 这两种方法都调用 [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) (立即调用 方法，同时通过后台线程) 调用 方法以计算分析的表达式并返回表示已分析表达式的值和类型的 `IDebugExpression2::EvaluateSync` `IDebugExpression2::EvaluateAsync` [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) 接口。 `IDebugParsedExpression::EvaluateSync` 使用提供的 SH、地址和联编程序将分析的表达式转换为由 接口表示的实际 `IDebugProperty2` 值。

### <a name="for-example"></a>例如
 在正在运行的程序中命中断点后，用户选择在" **快速** 监视"对话框中查看变量。 此对话框显示变量的名称、其值及其类型。 用户通常可以更改值。

 显示 **"快速监视** "对话框时，正在检查的变量的名称作为文本发送到 [ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)。 这会返回 [一个 IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) 对象，该对象表示已分析的表达式（本例中为 变量）。 [然后调用 EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) 以生成一个 对象，该对象表示变量的值和类型 `IDebugProperty2` 及其名称。 显示的信息是此信息。

 如果用户更改变量的值，则使用新值调用 [SetValueAsString，](../../extensibility/debugger/reference/idebugproperty2-setvalueasstring.md) 这将更改内存中变量的值，以便程序恢复运行时将使用该值。

 有关 [显示变量值的](../../extensibility/debugger/displaying-locals.md) 此过程的更多详细信息，请参阅显示局部变量。 有关 [变量值更改](../../extensibility/debugger/changing-the-value-of-a-local.md) 方式的更多详细信息，请参阅更改局部变量的值。

## <a name="in-this-section"></a>本节内容
 [评估上下文](../../extensibility/debugger/evaluation-context.md)提供 DE 调用该参数时传递企业版。

 [密钥表达式计算程序接口](../../extensibility/debugger/key-expression-evaluator-interfaces.md)描述编写代码时所需的关键企业版以及计算上下文。

## <a name="see-also"></a>请参阅
- [编写 CLR 表达式计算程序](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
- [显示局部变量](../../extensibility/debugger/displaying-locals.md)
- [更改局部变量值](../../extensibility/debugger/changing-the-value-of-a-local.md)

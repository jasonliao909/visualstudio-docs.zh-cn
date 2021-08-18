---
title: 计算监视窗口表达式|Microsoft Docs
description: 了解如何Visual Studio调用调试引擎，以确定执行暂停时其监视列表中每个表达式的当前值。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Watch window expressions
- Watch window, expressions
- expression evaluation, Watch window expressions
ms.assetid: b07e72c7-60d3-4b30-8e3f-6db83454c348
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: fbd9ad916b034158f21f909d9895629db74e0718
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122096656"
---
# <a name="evaluate-a-watch-window-expression"></a>计算监视窗口表达式
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式计算器的方法已弃用。 有关实现 CLR 表达式计算器的信息，请参阅 [CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 执行暂停时，Visual Studio调用调试引擎 (DE) 以确定其监视列表中每个表达式的当前值。 DE 使用表达式计算器计算每个 (企业版) ，Visual Studio"监视"窗口中显示 **其** 值。

 下面概述了如何计算监视列表表达式：

1. Visual Studio DE 的[GetExpressionContext](../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md)获取可用于计算表达式的表达式上下文。

2. 对于监视列表中的每个表达式，Visual Studio [ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)将表达式文本转换为已分析的表达式。

3. `IDebugExpressionContext2::ParseText` 调用 [Parse](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md) 以执行文本分析的实际工作，并生成 [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md) 对象。

4. `IDebugExpressionContext2::ParseText` 创建 [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) 对象，并将 `IDebugParsedExpression` 该对象放入该对象中。 然后，此 I `DebugExpression2` 对象返回到Visual Studio。

5. Visual Studio [EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)计算已分析的表达式。

6. `IDebugExpression2::EvaluateSync`将调用传递给[EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)以执行实际计算，并生成一个[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)对象，该对象返回到 Visual Studio。

7. Visual Studio [GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)获取表达式的值，然后显示在监视列表中。

## <a name="parse-then-evaluate"></a>分析然后评估
 由于分析复杂表达式可能比计算复杂表达式要长得多，因此计算表达式的过程分为两个步骤：1) 分析表达式，2) 计算分析的表达式。 这样，计算可以多次发生，但只需分析表达式一次。 中间分析表达式从 IDebugParsedExpression 对象中的 企业版 返回，而[IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md)对象又作为[IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)对象封装并返回自 DE。 `IDebugExpression`对象将所有计算都延迟到 `IDebugParsedExpression` 对象。

> [!NOTE]
> 即使用户假设有此企业版，也不需要Visual Studio过程;调用[EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)时，企业版可以在同一步骤中分析和计算 (MyCEE 示例的工作方式，例如) 。 如果你的语言可以形成复杂的表达式，你可能希望将分析步骤与计算步骤分开。 当显示许多监视表达式时Visual Studio调试器的性能。

## <a name="in-this-section"></a>本节内容
 [表达式计算的示例实现](../../extensibility/debugger/sample-implementation-of-expression-evaluation.md) 使用 MyCEE 示例逐步完成表达式计算过程。

 [计算监视表达式](../../extensibility/debugger/evaluating-a-watch-expression.md) 说明成功分析表达式后会发生什么情况。

## <a name="related-sections"></a>相关章节
 [评估上下文](../../extensibility/debugger/evaluation-context.md)提供调试引擎在 DE 中调用表达式 (时) 传递的参数 (企业版) 。

## <a name="see-also"></a>请参阅
 [编写 CLR 表达式计算程序](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)

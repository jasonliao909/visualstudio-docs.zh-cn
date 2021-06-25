---
title: 键表达式计算器接口|Microsoft Docs
description: 了解编写表达式计算程序时应熟悉的接口以及计算上下文。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation, interfaces
ms.assetid: 1cac9aa3-0867-4e12-a16e-1e90abbc0fb6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: abfa4018e763bbbac5ff788f401d0ceb76eb97a1
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901261"
---
# <a name="key-expression-evaluator-interfaces"></a>密钥表达式计算程序接口
> [!IMPORTANT]
> 在 Visual Studio 2015 中，此表达式评估器实现方法已弃用。 有关实现 CLR 表达式评估器的信息，请参阅 [CLR 表达式评估器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式评估器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 在 EE (EE) 编写表达式评估程序以及计算上下文时，应熟悉以下接口。

## <a name="interface-descriptions"></a>接口说明

- [IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md)

     具有单个方法 [GetAddress](../../extensibility/debugger/reference/idebugaddress-getaddress.md)，该方法获取表示当前执行点的数据结构。 此数据结构是调试引擎在 DE (传递给 [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)) 计算表达式的三个参数之一。 此接口通常由符号提供程序实现。

- [IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)

     具有 [Bind](../../extensibility/debugger/reference/idebugbinder-bind.md) 方法，该方法获取包含符号当前值的内存区域。 给定包含方法（由 [IDebugObject](../../extensibility/debugger/reference/idebugobject.md) 对象表示）和符号本身（由 [IDebugField](../../extensibility/debugger/reference/idebugfield.md) 对象表示）返回符号 `IDebugBinder::Bind` 的值。 `IDebugBinder` 通常由 DE 实现。

- [IDebugField](../../extensibility/debugger/reference/idebugfield.md)

     表示简单数据类型。 对于更复杂的类型（如数组和方法），请分别使用派生 [的 IDebugArrayField](../../extensibility/debugger/reference/idebugarrayfield.md) 和 [IDebugMethodField](../../extensibility/debugger/reference/idebugmethodfield.md) 接口。 [IDebugContainerField](../../extensibility/debugger/reference/idebugcontainerfield.md) 是另一个重要的派生接口，它表示包含其他符号（如方法或类）的符号。 接口 `IDebugField` (及其派生) 通常由符号提供程序实现。

     对象可用于查找符号的名称和类型，并且与 `IDebugField` [IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md) 对象一起可用于查找其值。

- [IDebugObject](../../extensibility/debugger/reference/idebugobject.md)

     表示符号运行时值的实际位。 [Bind](../../extensibility/debugger/reference/idebugbinder-bind.md) 采用 [表示符号的 IDebugField](../../extensibility/debugger/reference/idebugfield.md) 对象，并返回 [IDebugObject](../../extensibility/debugger/reference/idebugobject.md) 对象。 [GetValue](../../extensibility/debugger/reference/idebugobject-getvalue.md)方法返回内存缓冲区中符号的值。 DE 通常实现此接口来表示内存中属性的值。

- [IDebugExpressionEvaluator](../../extensibility/debugger/reference/idebugexpressionevaluator.md)

     此接口表示表达式计算程序本身。 键方法是 [Parse](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)，它返回 [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md) 接口。

- [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md)

     此接口表示已准备好计算已分析的表达式。 键方法是 [EvaluateSync，](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) 它返回表示表达式的值和类型的 IDebugProperty2。

- [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)

     此接口表示值及其类型，是表达式计算的结果。

## <a name="see-also"></a>另请参阅
- [评估上下文](../../extensibility/debugger/evaluation-context.md)

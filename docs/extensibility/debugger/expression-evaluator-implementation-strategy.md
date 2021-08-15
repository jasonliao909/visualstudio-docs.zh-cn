---
title: 表达式计算器实现策略 |Microsoft Docs
description: 了解通过首先实现用于在 "局部变量" 窗口中显示局部变量的代码来创建表达式计算器的策略。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- expression evaluation, implementation strategy
- debug engines, implementation strategies
ms.assetid: 1bccaeb3-8109-4128-ae79-16fd8fbbaaa2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: b6576d4656dd4afeed452dce7ac9f15036d12be37886c5d105961a2c0862e188
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121342747"
---
# <a name="expression-evaluator-implementation-strategy"></a>表达式计算器实现策略
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式计算器的方法已弃用。 有关实现 CLR 表达式计算器的信息，请参阅 [CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

  (企业版) 快速创建表达式计算器的一种方法是先实现在 "**局部变量**" 窗口中显示局部变量所需的最少代码。 认识到 " **局部变量** " 窗口中的每一行都显示局部变量的名称、类型和值，并且所有三个均由一个 [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) 对象表示，这一点很有用。 局部变量的名称、类型和值是 `IDebugProperty2` 通过调用其 [GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) 方法从对象获取的。 有关如何在 " **局部变量** " 窗口中显示局部变量的详细信息，请参阅 [显示局部变量](../../extensibility/debugger/displaying-locals.md)。

## <a name="discussion"></a>讨论区
 可能的实现序列始于实现 [IDebugExpressionEvaluator](../../extensibility/debugger/reference/idebugexpressionevaluator.md)。 必须实现 [Parse](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md) 和 [GetMethodProperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md) 方法才能显示局部变量。 调用 `IDebugExpressionEvaluator::GetMethodProperty` 会返回一个 `IDebugProperty2` 对象，该对象表示一个方法：即 [IDebugMethodField](../../extensibility/debugger/reference/idebugmethodfield.md) 对象。 方法本身不会显示在 " **局部变量** " 窗口中。

 接下来应实现 [EnumChildren](../../extensibility/debugger/reference/idebugproperty2-enumchildren.md) 方法。 调试引擎 (DE) 调用此方法，通过传递的参数获取局部变量和参数的列表 `IDebugProperty2::EnumChildren` `guidFilter` `guidFilterLocalsPlusArgs` 。 `IDebugProperty2::EnumChildren` 调用 [EnumArguments](../../extensibility/debugger/reference/idebugmethodfield-enumarguments.md) 和 [EnumLocals](../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md)，并将结果合并到单个枚举中。 有关更多详细信息，请参阅 [显示局部变量](../../extensibility/debugger/displaying-locals.md) 。

## <a name="see-also"></a>另请参阅
- [实现表达式计算器](../../extensibility/debugger/implementing-an-expression-evaluator.md)
- [显示局部变量](../../extensibility/debugger/displaying-locals.md)

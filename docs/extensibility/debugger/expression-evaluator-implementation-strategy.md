---
title: 表达式评估器实现策略|Microsoft Docs
description: 了解通过首先实现代码在"局部变量"窗口中显示局部变量来创建表达式评估器的策略。
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
# <a name="expression-evaluator-implementation-strategy"></a>表达式计算程序实现策略
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式计算器的方法已弃用。 有关实现 CLR 表达式计算器的信息，请参阅 [CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 快速创建表达式计算 (企业版) 方法之一是首先实现在"局部变量"窗口中显示局部变量 **所需的** 最小代码。 请注意，"局部变量"窗口中的每一行都显示局部变量的名称、类型和值，并且所有三行都由[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)对象表示。 局部变量的名称、类型和值通过调用其 `IDebugProperty2` [GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) 方法从对象获取。 若要详细了解如何在"局部变量"窗口中显示局部 **变量，请参阅**[显示局部变量](../../extensibility/debugger/displaying-locals.md)。

## <a name="discussion"></a>讨论区
 可能的实现序列从实现 [IDebugExpressionEvaluator 开始](../../extensibility/debugger/reference/idebugexpressionevaluator.md)。 [必须实现 Parse](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)和[GetMethodProperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md)方法以显示局部点。 调用 `IDebugExpressionEvaluator::GetMethodProperty` 将 `IDebugProperty2` 返回表示方法的对象：即 [IDebugMethodField](../../extensibility/debugger/reference/idebugmethodfield.md) 对象。 方法本身不会显示在"局部 **设置"窗口中** 。

 接下来 [应实现 EnumChildren](../../extensibility/debugger/reference/idebugproperty2-enumchildren.md) 方法。 调试引擎 (DE) 调用此方法，通过传递 的参数获取局部变量 `IDebugProperty2::EnumChildren` 和 `guidFilter` 参数的列表 `guidFilterLocalsPlusArgs` 。 `IDebugProperty2::EnumChildren` 调用 [EnumArguments](../../extensibility/debugger/reference/idebugmethodfield-enumarguments.md) 和 [EnumLocals](../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md)，将结果合并到单个枚举中。 有关 [更多详细信息，请参阅](../../extensibility/debugger/displaying-locals.md) 显示局部区域设置。

## <a name="see-also"></a>请参阅
- [实现表达式计算程序](../../extensibility/debugger/implementing-an-expression-evaluator.md)
- [显示局部区域设置](../../extensibility/debugger/displaying-locals.md)

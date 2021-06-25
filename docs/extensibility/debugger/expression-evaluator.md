---
title: 表达式计算|Microsoft Docs
description: 了解表达式评估器，它检查语言的语法，以在运行时以中断模式分析和计算变量和表达式。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- expressions [Debugging SDK]
- debugging [Debugging SDK], expression evaluation
- expression evaluation
ms.assetid: f9381b2f-99aa-426c-aea0-d9c15f3c859b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 998f361d8008257cb8f4a888b4d4fbb985c9c977
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900975"
---
# <a name="expression-evaluator"></a>表达式计算器
EE (EE) 检查语言的语法，以便运行时分析和计算变量和表达式，从而允许用户在 IDE 处于中断模式时查看它们。

## <a name="use-expression-evaluators"></a>使用表达式评估器
 表达式是使用 [ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) 方法创建的，如下所示：

1. 调试引擎 (DE) [IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md) 接口。

2. 调试包从 `IDebugExpressionContext2` [IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md) 接口获取对象，然后对该对象调用 方法来 `IDebugStackFrame2::ParseText` 获取 [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) 对象。

3. 调试包调用 [EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) 方法或 [EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) 方法获取表达式的值。 `IDebugExpression2::EvaluateAsync` 从"命令/即时"窗口调用 。 所有其他 UI 组件都调用 `IDebugExpression2::EvaluateSync` 。

4. 表达式计算的结果是一个 [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) 对象，该对象包含表达式计算结果的名称、类型和值。

   在表达式计算期间，EE 需要来自符号提供程序组件的信息。 符号提供程序提供用于标识和理解已分析表达式的符号信息。

   异步表达式计算完成后，DE 通过会话调试管理器 (SDM) 发送异步事件，以通知 IDE 表达式计算已完成。 然后，从对 方法的调用返回计算 `IDebugExpression2::EvaluateSync` 结果。

## <a name="implementation-notes"></a>实现说明
 调试引擎预期使用公共语言运行时和 CLR 接口与 ([!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 计算) 器。 因此，与调试引擎一起工作的表达式计算程序必须支持 CLR (可以在 debugref.doc 中找到所有 CLR 调试接口的完整列表，该列表是) [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] [!INCLUDE[winsdklong](../../deployment/includes/winsdklong_md.md)] 的一) 。

## <a name="see-also"></a>另请参阅
- [调试器组件](../../extensibility/debugger/debugger-components.md)

---
title: 显示局部|Microsoft Docs
description: 了解局部变量和参数的列表，它们统称为 方法的局部变量，在执行暂停时显示。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation, displaying locals
ms.assetid: 62264cec-845b-4233-aed7-0b038fa79250
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 1b4ca685031f33198a0c9aedb7f9ea8c031f05b6af0e3531fb423aca986fab9c
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121343235"
---
# <a name="display-locals"></a>显示局部区域设置
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式计算器的方法已弃用。 有关实现 CLR 表达式计算器的信息，请参阅 [CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 执行始终在方法的上下文中发生，也称为包含方法或当前方法。 执行暂停时，Visual Studio调用调试引擎 (DE) 获取局部变量和参数的列表，统称为 方法的局部变量。 Visual Studio"局部变量"窗口中显示这些 **局部变量及其** 值。

 为了显示局部点，DE 调用属于 企业版 的[GetMethodProperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md)方法，并赋予其计算上下文，即符号提供程序 (SP) 、当前执行地址和联编程序对象。 有关详细信息，请参阅评估 [上下文](../../extensibility/debugger/evaluation-context.md)。 如果调用成功，该方法将 `IDebugExpressionEvaluator::GetMethodProperty` 返回 [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) 对象，该对象表示包含当前执行地址的方法。

 DE 调用[EnumChildren](../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)获取[IEnumDebugPropertyInfo2](../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)对象，该对象经过筛选，仅返回局部值并枚举以生成[DEBUG_PROPERTY_INFO列表。](../../extensibility/debugger/reference/debug-property-info.md) 每个结构都包含本地的名称、类型和值。 类型和值存储为适合显示的格式化字符串。 名称、类型和值通常一起显示在"局部区域"窗口 **的一** 行中。

> [!NOTE]
> "**快速监视****"和"监视**"窗口还显示名称、值和类型格式相同的变量。 但是，这些值通过调用 [GetPropertyInfo 而不是](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) 来获取 `IDebugProperty2::EnumChildren` 。

## <a name="in-this-section"></a>本节内容
 [局部区域设置的示例实现](../../extensibility/debugger/sample-implementation-of-locals.md) 使用示例逐步完成实现局部设置的过程。

## <a name="related-sections"></a>相关章节
 [评估上下文](../../extensibility/debugger/evaluation-context.md)说明当调试引擎 (DE) 调用表达式计算 (企业版) 时，它将传递三个参数。

## <a name="see-also"></a>请参阅
 [编写 CLR 表达式计算程序](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)

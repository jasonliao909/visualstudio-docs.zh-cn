---
title: 局部变量的实现示例|Microsoft Docs
description: 通过本文了解 Visual Studio 如何从表达式计算器中获取方法的局部变量值。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: sample
helpviewer_keywords:
- debugging [Debugging SDK], local variables
- expression evaluation, local variables
ms.assetid: 66a2e00a-f558-4e87-96b8-5ecf5509e04c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 71b358543463e8c780a122dfa466651639f5a906
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122063624"
---
# <a name="sample-implementation-of-locals"></a>局部变量的示例实现
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式计算器的方法已弃用。 有关实现 CLR 表达式计算器的信息，请参阅 [CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 以下是有关 Visual Studio 如何从表达式计算器 (EE) 中获取方法的局部变量的概述：

1. Visual Studio 调用调试引擎 (DE) 的 [GetDebugProperty](../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md) 以获取表示堆栈帧的所有属性的 [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) 对象，包括局部变量。

2. `IDebugStackFrame2::GetDebugProperty` 调用 [GetMethodProperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md) 以获取描述断点在其中发生的方法的对象。 DE 提供符号提供程序 ([IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md))、地址 ([IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md)) 和绑定 ([IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md))。

3. `IDebugExpressionEvaluator::GetMethodProperty` 调用 [GetContainerField](../../extensibility/debugger/reference/idebugsymbolprovider-getcontainerfield.md) 和提供的 `IDebugAddress` 对象以获取表示包含特定地址的方法的 [IDebugContainerField](../../extensibility/debugger/reference/idebugcontainerfield.md)。

4. 针对 [IDebugMethodField](../../extensibility/debugger/reference/idebugmethodfield.md) 接口查询 `IDebugContainerField` 接口。 通过此接口可以访问方法的局部变量。

5. `IDebugExpressionEvaluator::GetMethodProperty` 实例化运行 `IDebugProperty2` 接口的类（示例中称为 `CFieldProperty`），以表示方法的局部变量。 `IDebugMethodField` 对象与 `IDebugSymbolProvider`、`IDebugAddress` 和 `IDebugBinder` 对象一起放置在此 `CFieldProperty` 对象中。

6. 初始化 `CFieldProperty` 对象时，[GetInfo](../../extensibility/debugger/reference/idebugfield-getinfo.md) 针对 `IDebugMethodField` 对象调用，以获取包含有关方法本身的所有可显示信息的 [FIELD_INFO](../../extensibility/debugger/reference/field-info.md) 结构。

7. `IDebugExpressionEvaluator::GetMethodProperty` 返回 `CFieldProperty` 对象，作为 `IDebugProperty2` 对象。

8. Visual Studio 针对具有筛选器 `guidFilterLocalsPlusArgs` 的返回的 `IDebugProperty2` 对象调用 [EnumChildren](../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)，它返回包含方法的局部变量的 [IEnumDebugPropertyInfo2](../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md) 对象。 此枚举由对 [EnumLocals](../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md) 和 [EnumArguments](../../extensibility/debugger/reference/idebugmethodfield-enumarguments.md) 的调用填充。

9. Visual Studio 调用 [Next](../../extensibility/debugger/reference/ienumdebugpropertyinfo2-next.md) 以获取每个局部变量的 [DEBUG_PROPERTY_INFO](../../extensibility/debugger/reference/debug-property-info.md) 结构。 此结构包含针对局部变量的 `IDebugProperty2` 接口的指针。

10. Visual Studio 调用每个局部变量的 [GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)，以获取局部变量名称、值和类型。 此信息显示在“局部变量”窗口中。

## <a name="in-this-section"></a>在本节中
 [实现 GetMethodProperty](../../extensibility/debugger/implementing-getmethodproperty.md) 描述 [GetMethodProperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md) 的实现。

 [枚举局部变量](../../extensibility/debugger/enumerating-locals.md) 描述调试引擎 (DE) 如何进行调用以枚举局部变量或参数。

 [获取局部变量属性](../../extensibility/debugger/getting-local-properties.md) 描述 DE 如何进行调用以获取一个或多个局部变量的名称、类型和值。

 [获取局部变量值](../../extensibility/debugger/getting-local-values.md) 讨论如何获取局部变量的值，这需要计算上下文给出的绑定对象的服务。

 [计算局部变量](../../extensibility/debugger/evaluating-locals.md) 说明如何计算局部变量。

## <a name="related-sections"></a>相关章节
 [计算上下文](../../extensibility/debugger/evaluation-context.md) 提供在 DE 调用表达式计算器 (EE) 时传递的参数。

 [MyCEE 示例](/previous-versions/)演示一种实现方法，该方法用于创建 MyC 语言的表达式计算器。

## <a name="see-also"></a>另请参阅
- [显示局部变量](../../extensibility/debugger/displaying-locals.md)
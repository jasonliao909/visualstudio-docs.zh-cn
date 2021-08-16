---
title: 实现表达式计算|Microsoft Docs
description: 了解如何计算表达式，该表达式涉及调试引擎、符号提供程序、联编程序对象和表达式计算程序。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- expression evaluators
- debugging [Debugging SDK], expression evaluators
ms.assetid: e9ada7be-845e-4baa-bf8f-e4890e7ba490
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 4d4c5ab78d8a7d125bf78b32317bfeba673d7ef99852d69aab5e99bd6a59ee96
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121361114"
---
# <a name="implement-an-expression-evaluator"></a>实现表达式计算程序
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式计算器的方法已弃用。 有关实现 CLR 表达式计算器的信息，请参阅 [CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 计算表达式是调试引擎 (DE) 、符号提供程序 (SP) 、联编程序对象和表达式计算程序 (企业版) 。 这四个组件由接口连接，这些接口由一个组件实现，由另一个组件使用。

 该企业版以字符串的形式从 DE 接受表达式，并对其进行分析或计算。 该企业版运行 DE 使用的以下接口：

- [IDebugExpressionEvaluator](../../extensibility/debugger/reference/idebugexpressionevaluator.md)

- [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md)

  该企业版调用 DE 提供的联编程序对象，获取符号和对象的值。 该企业版使用以下接口，这些接口由 DE 实现：

- [IDebugObject](../../extensibility/debugger/reference/idebugobject.md)

- [IDebugArrayObject](../../extensibility/debugger/reference/idebugarrayobject.md)

- [IDebugFunctionObject](../../extensibility/debugger/reference/idebugfunctionobject.md)

- [IDebugPointerObject](../../extensibility/debugger/reference/idebugpointerobject.md)

- [IDebugManagedObject](../../extensibility/debugger/reference/idebugmanagedobject.md)

- [IEnumDebugObjects](../../extensibility/debugger/reference/ienumdebugobjects.md)

- [IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)

  该企业版[运行 IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)。 `IDebugProperty2`提供了一种机制，用于描述表达式计算的结果，例如本地变量、基元或要Visual Studio的对象，然后，该机制会在"局部变量"、"监视"或"即时"窗口中显示相应的 **信息。**

  当 DE 要求企业版时，SP 将给定给该用户。 SP 运行描述地址和字段的接口，例如以下接口及其派生项：

- [IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md)

- [IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md)

- [IDebugField](../../extensibility/debugger/reference/idebugfield.md)

  接口企业版所有这些接口。

## <a name="in-this-section"></a>本节内容
 [表达式计算程序实现策略](../../extensibility/debugger/expression-evaluator-implementation-strategy.md)为表达式计算程序定义一个三步过程 (企业版) 实现策略。

## <a name="see-also"></a>另请参阅
- [编写 CLR 表达式计算程序](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)

---
title: 计算上下文 |Microsoft Docs
description: 当调试引擎调用表达式计算器时，自变量将确定用于查找和计算符号的上下文： pSymbolProvider、pAddress 和 pBinder。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation, context
ms.assetid: 008a20c7-1b27-4013-bf96-d6a3f510da02
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: fa9b199f31dc200fe128e6435b2967ab689724bb
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122153545"
---
# <a name="evaluation-context"></a>评估上下文
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式计算器的方法已弃用。 有关实现 CLR 表达式计算器的信息，请参阅 [CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 当调试引擎 (DE) 调用表达式计算器 (企业版) 时，传递给[EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)的三个参数将确定用于查找和计算符号的上下文，如下表所示。

## <a name="arguments"></a>参数

|参数|说明|
|--------------|-----------------|
|`pSymbolProvider`|一个 [IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md) 接口，它指定用于标识符号的符号处理程序 (SH) 。|
|`pAddress`|指定当前执行点的 [IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md) 接口。 此接口查找包含要执行的代码的方法。|
|`pBinder`|一个 [IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md) 接口，它查找符号的值和类型（给定其名称）。|

 `IDebugParsedExpression::EvaluateSync` 返回表示结果值及其类型的 [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) 接口。

## <a name="see-also"></a>请参阅
- [键表达式计算器接口](../../extensibility/debugger/key-expression-evaluator-interfaces.md)
- [显示局部变量](../../extensibility/debugger/displaying-locals.md)
- [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)
- [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md)
- [IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)

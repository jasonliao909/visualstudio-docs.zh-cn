---
title: 表达式计算的实现示例 | Microsoft Docs
description: 了解 Visual Studio 如何为监视窗口表达式调用 ParseText 以生成 IDebugExpression2 对象。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: sample
helpviewer_keywords:
- expression evaluators
- debugging [Debugging SDK], expression evaluators
- expression evaluation, examples
ms.assetid: 2a5f04b8-6c65-4232-bddd-9093653a22c4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: de0e052fd42f1603889f7521a1e45e50b0f36eea
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902301"
---
# <a name="sample-implementation-of-expression-evaluation"></a>表达式计算的实现示例
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式计算器的方法已弃用。 有关实现 CLR 表达式计算器的信息，请参阅 [CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 对于监视窗口表达式，Visual Studio 调用 [ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) 来生成 [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) 对象。 `IDebugExpressionContext2::ParseText` 实例化表达式计算器 (EE) 并调用[分析](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md) 以获取 [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md) 对象。

 `IDebugExpressionEvaluator::Parse` 执行以下任务：

1. [仅限 C++] 分析表达式以查找错误。

2. 实例化运行 `IDebugParsedExpression` 接口的类（此例中称为 `CParsedExpression`），并在类中存储要分析的表达式。

3. 从 `IDebugParsedExpression` 对象返回 `CParsedExpression` 接口。

> [!NOTE]
> 在后面的示例以及 MyCEE 示例中，表达式计算器不会将分析与计算分开。

## <a name="managed-code"></a>托管代码
 下面的代码显示托管代码中 `IDebugExpressionEvaluator::Parse` 的实现。 此方法版本将分析延迟到 [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)，因为用于分析的代码也在同时进行计算（请参阅[计算 Watch 表达式](../../extensibility/debugger/evaluating-a-watch-expression.md)）。

```csharp
namespace EEMC
{
    public class CParsedExpression : IDebugParsedExpression
    {
        public HRESULT Parse(
                string                 expression,
                uint                   parseFlags,
                uint                   radix,
            out string                 errorMessage,
            out uint                   errorPosition,
            out IDebugParsedExpression parsedExpression)
        {
            errorMessage = "";
            errorPosition = 0;

            parsedExpression =
                new CParsedExpression(parseFlags, radix, expression);
            return COM.S_OK;
        }
    }
}
```

## <a name="unmanaged-code"></a>非托管代码
以下代码是非托管代码中的 `IDebugExpressionEvaluator::Parse` 实现。 此方法调用帮助程序函数 `Parse` 来分析表达式并检查错误，但此方法会忽略生成的值。 正式的计算会延迟到 [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)，其中表达式会在计算时进行分析（请参阅[计算 Watch 表达式](../../extensibility/debugger/evaluating-a-watch-expression.md)）。

```cpp
STDMETHODIMP CExpressionEvaluator::Parse(
        in    LPCOLESTR                 pszExpression,
        in    PARSEFLAGS                flags,
        in    UINT                      radix,
        out   BSTR                     *pbstrErrorMessages,
        inout UINT                     *perrorCount,
        out   IDebugParsedExpression  **ppparsedExpression
    )
{
    if (pbstrErrorMessages == NULL)
        return E_INVALIDARG;
    else
        *pbstrErrormessages = 0;

    if (pparsedExpression == NULL)
        return E_INVALIDARG;
    else
        *pparsedExpression = 0;

    if (perrorCount == NULL)
        return E_INVALIDARG;

    HRESULT hr;
    // Look for errors in the expression but ignore results
    hr = ::Parse( pszExpression, pbstrErrorMessages );
    if (hr != S_OK)
        return hr;

    CParsedExpression* pparsedExpr = new CParsedExpression( radix, flags, pszExpression );
    if (!pparsedExpr)
        return E_OUTOFMEMORY;

    hr = pparsedExpr->QueryInterface( IID_IDebugParsedExpression,
                                      reinterpret_cast<void**>(ppparsedExpression) );
    pparsedExpr->Release();

    return hr;
}
```

## <a name="see-also"></a>另请参阅
- [计算监视窗口表达式](../../extensibility/debugger/evaluating-a-watch-window-expression.md)
- [计算 Watch 表达式](../../extensibility/debugger/evaluating-a-watch-expression.md)

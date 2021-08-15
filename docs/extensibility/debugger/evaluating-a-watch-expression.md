---
title: 计算监视表达式|Microsoft Docs
description: 了解Visual Studio显示监视表达式的值时如何使用 EvaluateSync。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- expression evaluation, watch expressions
- watch expressions
ms.assetid: 8317cd52-6fea-4e8f-a739-774dc06bd44b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: c5f6978e6ba45c42777533d0fdd288f3ecc55f2dd8dfd26558f1a106489bf376
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121342968"
---
# <a name="evaluate-a-watch-expression"></a>计算监视表达式
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式计算器的方法已弃用。 有关实现 CLR 表达式计算器的信息，请参阅 [CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

当Visual Studio可以显示监视表达式的值时，它将调用[EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)，这反过来调用[EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)。 此过程生成包含表达式的值和类型的 [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) 对象。

在 的此实现 `IDebugParsedExpression::EvaluateSync` 中，将同时分析和计算表达式。 此实现执行以下任务：

1. 分析和计算表达式，以生成保存值及其类型的泛型对象。 在 C# 中，这表示为 C++ 中的 `object` while，这表示为 `VARIANT` 。

2. 实例化 (示例中调用的类) 实现 接口，并存储 `CValueProperty` `IDebugProperty2` 类中要返回的值。

3. 从 `IDebugProperty2` 对象返回 `CValueProperty` 接口。

## <a name="managed-code"></a>托管代码
这是托管代码中 `IDebugParsedExpression::EvaluateSync` 的实现。 帮助程序方法 `Tokenize` 将表达式解析为分析树。 帮助程序函数 `EvalToken` 将标记转换为值。 帮助程序函数以递归方式遍历分析树，为表示值的每个节点调用 ，并应用任何 (表达式) 或减法 `FindTerm` `EvalToken` 运算。

```csharp
namespace EEMC
{
    public class CParsedExpression : IDebugParsedExpression
    {
        public HRESULT EvaluateSync(
            uint evalFlags,
            uint timeout,
            IDebugSymbolProvider provider,
            IDebugAddress address,
            IDebugBinder binder,
            string resultType,
            out IDebugProperty2 result)
        {
            HRESULT retval = COM.S_OK;
            this.evalFlags = evalFlags;
            this.timeout = timeout;
            this.provider = provider;
            this.address = address;
            this.binder = binder;
            this.resultType = resultType;

            try
            {
                IDebugField field = null;
                // Tokenize, then parse.
                tokens = Tokenize(expression);
                result = new CValueProperty(
                        expression,
                        (int) FindTerm(EvalToken(tokens[0], out field),1),
                        field,
                        binder);
            }
            catch (ParseException)
            {
                result = new CValueProperty(expression, "Huh?");
                retval = COM.E_INVALIDARG;
            }
            return retval;
        }
    }
}
```

## <a name="unmanaged-code"></a>非托管代码
这是非托管 `IDebugParsedExpression::EvaluateSync` 代码中 的实现。 帮助程序函数 `Evaluate` 分析和计算表达式，并返回 `VARIANT` 一个持有结果值的 。 帮助程序函数 `VariantValueToProperty` 将 捆绑 `VARIANT` 到 `CValueProperty` 对象中。

```cpp
STDMETHODIMP CParsedExpression::EvaluateSync(
    in  DWORD                 evalFlags,
    in  DWORD                 dwTimeout,
    in  IDebugSymbolProvider* pprovider,
    in  IDebugAddress*        paddress,
    in  IDebugBinder*         pbinder,
    in  BSTR                  bstrResultType,
    out IDebugProperty2**     ppproperty )
{
    // dwTimeout parameter is ignored in this implementation.
    if (pprovider == NULL)
        return E_INVALIDARG;

    if (paddress == NULL)
        return E_INVALIDARG;

    if (pbinder == NULL)
        return E_INVALIDARG;

    if (ppproperty == NULL)
        return E_INVALIDARG;
    else
        *ppproperty = 0;

    HRESULT hr;
    VARIANT value;
    BSTR    bstrErrorMessage = NULL;
    hr = ::Evaluate( pprovider,
                     paddress,
                     pbinder,
                     m_expr,
                     &bstrErrorMessage,
                     &value );
    if (hr != S_OK)
    {
        if (bstrErrorMessage == NULL)
            return hr;

        //we can display better messages ourselves.
        HRESULT hrLocal = S_OK;
        VARIANT varType;
        VARIANT varErrorMessage;

        VariantInit( &varType );
        VariantInit( &varErrorMessage );
        varErrorMessage.vt      = VT_BSTR;
        varErrorMessage.bstrVal = bstrErrorMessage;

        CValueProperty* valueProperty = new CValueProperty();
        if (valueProperty != NULL)
        {
            hrLocal = valueProperty->Init(m_expr, varType, varErrorMessage);
            if (SUCCEEDED(hrLocal))
            {
                hrLocal = valueProperty->QueryInterface( IID_IDebugProperty2,
                        reinterpret_cast<void**>(ppproperty) );
            }
        }

        VariantClear(&varType);
        VariantClear(&varErrorMessage); //frees BSTR
        if (!valueProperty)
            return hr;
        valueProperty->Release();
        if (FAILED(hrLocal))
            return hr;
    }
    else
    {
        if (bstrErrorMessage != NULL)
            SysFreeString(bstrErrorMessage);

        hr = VariantValueToProperty( pprovider,
                                     paddress,
                                     pbinder,
                                     m_radix,
                                     m_expr,
                                     value,
                                     ppproperty );
        VariantClear(&value);
        if (FAILED(hr))
            return hr;
    }

    return S_OK;
}
```

## <a name="see-also"></a>另请参阅
- [计算监视窗口表达式](../../extensibility/debugger/evaluating-a-watch-window-expression.md)
- [表达式计算的实现示例](../../extensibility/debugger/sample-implementation-of-expression-evaluation.md)

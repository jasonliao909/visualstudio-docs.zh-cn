---
title: 实现 GetMethodProperty |Microsoft Docs
description: 了解如何Visual Studio调试引擎的 GetDebugProperty 获取有关堆栈帧上当前方法的信息。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- GetMethodProperty method
- IDebugExpressionEvaluator2 property
ms.assetid: 6305874f-a2c4-4432-834c-07530ea84bff
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 17f846e9dcb70300b27aa7248c4c4c2783b02887f6ba9d6071f636cbf48b78b0
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121361101"
---
# <a name="implement-getmethodproperty"></a>实现 GetMethodProperty
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式计算器的方法已弃用。 有关实现 CLR 表达式计算器的信息，请参阅 [CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

Visual Studio调试引擎的 (DE) [GetDebugProperty ，而 GetDebugProperty](../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md)又调用[GetMethodProperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md)以获取有关堆栈帧上当前方法的信息。

的此 `IDebugExpressionEvaluator::GetMethodProperty` 实现执行以下任务：

1. 调用 [GetContainerField](../../extensibility/debugger/reference/idebugsymbolprovider-getcontainerfield.md)，并传递 [IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md) 对象。 SP (符号) 返回表示包含指定地址的方法的[IDebugContainerField。](../../extensibility/debugger/reference/idebugcontainerfield.md)

2. 从 获取[IDebugMethodField。](../../extensibility/debugger/reference/idebugmethodfield.md) `IDebugContainerField`

3. 实例化 (中调用的类) 实现 `CFieldProperty` [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) 接口并包含 `IDebugMethodField` 从 SP 返回的对象。

4. 从 `IDebugProperty2` 对象返回 `CFieldProperty` 接口。

## <a name="managed-code"></a>托管代码
此示例演示托管代码中 `IDebugExpressionEvaluator::GetMethodProperty` 的实现。

```csharp
namespace EEMC
{
    [GuidAttribute("462D4A3D-B257-4AEE-97CD-5918C7531757")]
    public class EEMCClass : IDebugExpressionEvaluator
    {
        public HRESULT GetMethodProperty(
                IDebugSymbolProvider symbolProvider,
                IDebugAddress        address,
                IDebugBinder         binder,
                int                  includeHiddenLocals,
            out IDebugProperty2      property)
        {
            IDebugContainerField containerField = null;
            IDebugMethodField methodField       = null;
            property = null;

            // Get the containing method field.
            symbolProvider.GetContainerField(address, out containerField);
            methodField = (IDebugMethodField) containerField;

            // Return the property of method field.
            property = new CFieldProperty(symbolProvider, address, binder, methodField);
            return COM.S_OK;
        }
    }
}
```

## <a name="unmanaged-code"></a>非托管代码
此示例演示非托管代码中 `IDebugExpressionEvaluator::GetMethodProperty` 的实现。

```
[CPP]
STDMETHODIMP CExpressionEvaluator::GetMethodProperty(
        in IDebugSymbolProvider *pprovider,
        in IDebugAddress        *paddress,
        in IDebugBinder         *pbinder,
        in BOOL                  includeHiddenLocals,
        out IDebugProperty2    **ppproperty
    )
{
    if (pprovider == NULL)
        return E_INVALIDARG;

    if (ppproperty == NULL)
        return E_INVALIDARG;
    else
        *ppproperty = 0;

    HRESULT hr;
    IDebugContainerField* pcontainer = NULL;

    hr = pprovider->GetContainerField(paddress, &pcontainer);
    if (FAILED(hr))
        return hr;

    IDebugMethodField*    pmethod    = NULL;
    hr = pcontainer->QueryInterface( IID_IDebugMethodField,
            reinterpret_cast<void**>(&pmethod));
    pcontainer->Release();
    if (FAILED(hr))
        return hr;

    CFieldProperty* pfieldProperty = new CFieldProperty( pprovider,
                                                         paddress,
                                                         pbinder,
                                                         pmethod );
    pmethod->Release();
    if (!pfieldProperty)
        return E_OUTOFMEMORY;

    hr = pfieldProperty->Init();
    if (FAILED(hr))
    {
        pfieldProperty->Release();
        return hr;
    }

    hr = pfieldProperty->QueryInterface( IID_IDebugProperty2,
            reinterpret_cast<void**>(ppproperty));
    pfieldProperty->Release();

    return hr;
}
```

## <a name="see-also"></a>另请参阅
- [局部变量的示例实现](../../extensibility/debugger/sample-implementation-of-locals.md)

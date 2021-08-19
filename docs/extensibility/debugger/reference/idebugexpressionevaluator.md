---
description: 此接口表示表达式计算程序。
title: IDebugExpressionEvaluator |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpressionEvaluator
helpviewer_keywords:
- IDebugExpressionEvaluator interface
ms.assetid: 0636d8c3-625a-49fa-94b6-516f22b7e1bc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 41128445dca38d6d735d3dd4f83b84363bcb4989
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122138674"
---
# <a name="idebugexpressionevaluator"></a>IDebugExpressionEvaluator
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式计算器的方法已弃用。 有关实现 CLR 表达式评估器的信息，请参阅 [CLR 表达式评估器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式评估器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

此接口表示表达式计算程序。

## <a name="syntax"></a>语法

```
IDebugExpressionEvaluator : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
表达式计算程序必须实现此接口。

## <a name="notes-for-callers"></a>调用方说明
若要获取此接口，请通过使用类 ID 和 (`CoCreateInstance` CLSID) 方法实例化表达式计算器。 请参阅示例。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
下表显示了 的方法 `IDebugExpressionEvaluator` 。

|方法|说明|
|------------|-----------------|
|[Parse](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)|将表达式字符串转换为已分析的表达式。|
|[GetMethodProperty](../../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md)|获取方法的局部变量、参数和其他属性。|
|[GetMethodLocationProperty](../../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodlocationproperty.md)|将方法位置和偏移量转换为内存地址。|
|[SetLocale](../../../extensibility/debugger/reference/idebugexpressionevaluator-setlocale.md)|确定用于创建可打印结果的语言。|
|[SetRegistryRoot](../../../extensibility/debugger/reference/idebugexpressionevaluator-setregistryroot.md)|设置注册表根。 用于并行调试。|

## <a name="remarks"></a>备注
在典型情况下，调试引擎 (DE) 将表达式 (企业版) 作为[对 ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)的调用的结果实例化。 因为 DE 知道它想要使用的 企业版 语言和供应商，所以 DE 从注册表获取 企业版 的 CLSID (用于调试的[SDK](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)帮助程序函数 可帮助进行此检索 `GetEEMetric`) 。

实例企业版，DE 调用[Parse](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)来分析表达式，并存储在[IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md)对象中。 稍后，对 [EvaluateSync 的调用](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) 将计算表达式。

## <a name="requirements"></a>要求
标头：ee.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="example"></a>示例
此示例演示如何在源代码中给定符号提供程序和地址来实例化表达式计算程序。 此示例使用 SDK `GetEEMetric` [Helpers for Debugging](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md) 库 dbgmetric.lib 中的函数 dbgmetric.lib。

```cpp
IDebugExpressionEvaluator GetExpressionEvaluator(IDebugSymbolProvider pSymbolProvider,
                                                 IDebugAddress *pSourceAddress)
{
    // This is typically defined globally but is specified here just
    // for this example.
    static const WCHAR strRegistrationRoot[] = L"Software\\Microsoft\\VisualStudio\\8.0Exp";

    IDebugExpressionEvaluator *pEE = NULL;
    if (pSymbolProvider != NULL && pSourceAddress != NULL) {
        HRESULT hr         = S_OK;
        GUID  languageGuid = { 0 };
        GUID  vendorGuid   = { 0 };

        hr = pSymbolProvider->GetLanguage(pSourceAddress,
                                          &languageGuid,
                                          &vendorGuid);
        if (SUCCEEDED(hr)) {
            CLSID clsidEE = { 0 };
            CComPtr<IDebugExpressionEvaluator> spExpressionEvaluator;
            // Get the expression evaluator's CLSID from the registry.
            ::GetEEMetric(languageGuid,
                          vendorGuid,
                          metricCLSID,
                          &clsidEE,
                          strRegistrationRoot);
            if (!IsEqualGUID(clsidEE,GUID_NULL)) {
                // Instantiate the expression evaluator.
                spExpressionEvaluator.CoCreateInstance(clsidEE);
            }
            if (spExpressionEvaluator != NULL) {
                pEE = spExpressionEvaluator.Detach();
            }
        }
    }
    return pEE;
}
```

## <a name="see-also"></a>请参阅
- [表达式计算接口](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)
- [IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md)
- [EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)
- [用于调试的 SDK 帮助程序](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)

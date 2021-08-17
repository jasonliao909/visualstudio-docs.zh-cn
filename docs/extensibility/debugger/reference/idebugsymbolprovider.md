---
description: 此接口表示一个提供符号和类型的符号提供程序，以字段返回它们。
title: IDebugSymbolProvider |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugSymbolProvider
helpviewer_keywords:
- IDebugSymbolProvider interface
ms.assetid: df5f095f-1dee-46f9-84cf-92417c71d5fb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 3ba1475f62ff1732fd7b4a4e8554a428bf053be6
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122087413"
---
# <a name="idebugsymbolprovider"></a>IDebugSymbolProvider
此接口表示一个提供符号和类型的符号提供程序，以字段返回它们。

## <a name="syntax"></a>语法

```
IDebugSymbolProvider : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
符号提供程序必须实现此接口，以向表达式计算器提供符号和类型信息。

## <a name="notes-for-callers"></a>调用方说明
对于非托管符号提供程序) ，通过使用 COM 的函数 (或加载相应的托管代码程序集并基于该程序集中发现的信息实例化符号提供程序，可获取此 `CoCreateInstance` 接口。 调试引擎实例化符号提供程序，以与表达式计算程序协调工作。 有关实例化此接口的一种方法，请参阅示例。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
下表显示了 的方法 `IDebugSymbolProvider` 。

|方法|说明|
|------------|-----------------|
|`Initialize`|已否决。 请勿使用。|
|`Uninitialize`|已否决。 请勿使用。|
|[GetContainerField](../../../extensibility/debugger/reference/idebugsymbolprovider-getcontainerfield.md)|获取包含调试地址的字段。|
|`GetField`|已否决。 请勿使用。|
|[GetAddressesFromPosition](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromposition.md)|地图文档位置转换为调试地址数组。|
|[GetAddressesFromContext](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromcontext.md)|地图文档上下文转换为调试地址数组。|
|[GetContextFromAddress](../../../extensibility/debugger/reference/idebugsymbolprovider-getcontextfromaddress.md)|地图调试地址转换为文档上下文。|
|[GetLanguage](../../../extensibility/debugger/reference/idebugsymbolprovider-getlanguage.md)|获取用于在调试地址编译代码的语言。|
|`GetGlobalContainer`|已否决。 请勿使用。|
|[GetMethodFieldsByName](../../../extensibility/debugger/reference/idebugsymbolprovider-getmethodfieldsbyname.md)|获取表示完全限定的方法名称的字段。|
|[GetClassTypeByName](../../../extensibility/debugger/reference/idebugsymbolprovider-getclasstypebyname.md)|获取表示完全限定类名的类字段类型。|
|[GetNamespacesUsedAtAddress](../../../extensibility/debugger/reference/idebugsymbolprovider-getnamespacesusedataddress.md)|为与调试地址关联的命名空间创建枚举器。|
|[GetTypeByName](../../../extensibility/debugger/reference/idebugsymbolprovider-gettypebyname.md)|地图符号名称为符号类型。|
|[GetNextAddress](../../../extensibility/debugger/reference/idebugsymbolprovider-getnextaddress.md)|获取方法中给定调试地址后跟的调试地址。|

## <a name="remarks"></a>备注
此接口将文档位置映射到调试地址，反之亦然。

## <a name="requirements"></a>要求
标头：sh.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="example"></a>示例
此示例演示如何实例化符号提供程序，给定其 GUID (调试引擎必须知道此值) 。

```cpp
// A debug engine uses its own symbol provider and would know the GUID
// of that provider.
IDebugSymbolProvider *GetSymbolProvider(GUID *pSymbolProviderGuid)
{
    // This is typically defined globally. For this example, it is
    // defined here.
    static const WCHAR strRegistrationRoot[] = L"Software\\Microsoft\\VisualStudio\\8.0Exp";
    IDebugSymbolProvider *pProvider = NULL;
    if (pSymbolProviderGuid != NULL) {
        CLSID clsidProvider = { 0 };
        ::GetSPMetric(*pSymbolProviderGuid,
                      storetypeFile,
                      metricCLSID,
                      &clsidProvider,
                      strRegistrationRoot);
        if (IsEqualGUID(clsidProvider,GUID_NULL)) {
            // No file type provider, try metadata provider.
            ::GetSPMetric(*pSymbolProviderGuid,
                          ::storetypeMetadata,
                          metricCLSID,
                          &clsidProvider,
                          strRegistrationRoot);
        }
        if (!IsEqualGUID(clsidProvider,GUID_NULL)) {
            CComPtr<IDebugSymbolProvider> spSymbolProvider;
            spSymbolProvider.CoCreateInstance(clsidProvider);
            if (spSymbolProvider != NULL) {
                pProvider = spSymbolProvider.Detach();
            }
        }
    }
    return(pProvider);
}
```

## <a name="see-also"></a>请参阅
- [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)

---
description: 确定指定调试器地址中的代码是否隐藏。
title: IDebugComPlusSymbolProvider：：IsHiddenCode |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugComPlusSymbolProvider::IsHiddenCode
ms.assetid: 1352c6ab-7b92-4a16-b2d2-6520b628830e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e30e4b66768b249afb350be3336754b300b8089f2eb5eb429182b0601653e0bb
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121390328"
---
# <a name="idebugcomplussymbolproviderishiddencode"></a>IDebugComPlusSymbolProvider::IsHiddenCode
确定指定调试器地址中的代码是否隐藏。

## <a name="syntax"></a>语法

```cpp
HRESULT IsHiddenCode(
    IDebugAddress* pAddress
);
```

```csharp
int IsHiddenCode(
    IDebugAddress pAddress
);
```

## <a name="parameters"></a>参数
`pAddress`\
[in]由 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) 接口表示的调试地址。

## <a name="return-value"></a>返回值
如果隐藏代码，则 返回 `S_OK` ;否则返回 `S_FALSE` 。

## <a name="example"></a>示例
下面的示例演示如何为公开 [IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)接口的 **CDebugSymbolProvider** 对象实现此方法。

```cpp
HRESULT CDebugSymbolProvider::IsHiddenCode(
    IDebugAddress* pAddress
)
{
    HRESULT hr = S_OK;
    CDEBUG_ADDRESS address;
    CComPtr<CModule> pModule;

    ASSERT(IsValidObjectPtr(this, CDebugSymbolProvider));
    ASSERT(IsValidInterfacePtr(pAddress, IDebugAddress));

    METHOD_ENTRY( CDebugSymbolProvider::IsHiddenCode );

    IfFalseGo( pAddress, S_FALSE );
    IfFailGo( pAddress->GetAddress( &address ) );

    ASSERT(address.addr.dwKind == ADDRESS_KIND_METADATA_METHOD);
    IfFalseGo( address.addr.dwKind == ADDRESS_KIND_METADATA_METHOD, S_FALSE );

    IfFailGo( GetModule( address.GetModule(), &pModule) );

    if (!pModule->IsHiddenCode( address.addr.addr.addrMethod.tokMethod,
                                address.addr.addr.addrMethod.dwVersion,
                                address.addr.addr.addrMethod.dwOffset ))
    {

        // S_FALSE indicates this sequence point is not hidden

        hr = S_FALSE;
    }

Error:

    METHOD_EXIT( CDebugSymbolProvider::IsHiddenCode, hr );

    if (!SUCCEEDED(hr))
    {
        hr = S_FALSE;
    }

    return hr;
}
```

## <a name="see-also"></a>另请参阅
- [IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)

---
description: 给定 ICorDebugModule 对象，从数据流加载调试符号。
title: IDebugComPlusSymbolProvider2::LoadSymbolsFromStreamWithCorModule
titleSuffix: ''
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugComPlusSymbolProvider2::LoadSymbolsFromStreamWithCorModule
- LoadSymbolsFromStreamWithCorModule
ms.assetid: f79b894f-52c4-43c2-9a68-c71536451f6c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 47a412cdd825fe85872652a5e240165af3c42524f82908fe6f2de7fa6f326349
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121342331"
---
# <a name="idebugcomplussymbolprovider2loadsymbolsfromstreamwithcormodule"></a>IDebugComPlusSymbolProvider2::LoadSymbolsFromStreamWithCorModule
给定 **ICorDebugModule** 对象，从数据流加载调试符号。

## <a name="syntax"></a>语法

```cpp
HRESULT LoadSymbolsFromStreamWithCorModule(
    ULONG32   ulAppDomainID,
    GUID      guidModule,
    ULONGLONG baseAddress,
    IUnknown* pUnkMetadataImport,
    IUnknown* pUnkCorDebugModule,
    IStream*  pStream
);
```

```csharp
int LoadSymbolsFromStreamWithCorModule(
    uint    ulAppDomainID,
    Guid    guidModule,
    ulong   baseAddress,
    object  pUnkMetadataImport,
    object  pUnkCorDebugModule,
    IStream pStream
);
```

## <a name="parameters"></a>参数
`ulAppDomainID`\
[in]应用程序域的标识符。

`guidModule`\
[in]模块的唯一标识符。

`baseAddress`\
[in]基本内存地址。

`pUnkMetadataImport`\
[in]包含符号元数据的对象。

`pUnkCorDebugModule`\
[in]实现 [ICorDebugModule 接口 的对象](/dotnet/framework/unmanaged-api/debugging/icordebugmodule-interface)。

`pStream`\
[in]包含要加载的调试符号的数据流。

## <a name="return-value"></a>返回值
如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="example"></a>示例
以下示例演示如何为公开 [IDebugComPlusSymbolProvider2](../../../extensibility/debugger/reference/idebugcomplussymbolprovider2.md)接口的 **CDebugSymbolProvider** 对象实现此方法。

```cpp
HRESULT CDebugSymbolProvider::LoadSymbolsFromStreamWithCorModule(
    ULONG32 ulAppDomainID,
    GUID guidModule,
    ULONGLONG baseOffset,
    IUnknown* pUnkMetadataImport,
    IUnknown* pUnkCorDebugModule,
    IStream* pStream
)
{
    CAutoLock Lock(this);

    HRESULT hr = S_OK;
    CComPtr<IMetaDataImport> pMetadata;
    CComPtr<ICorDebugModule> pCorModule;

    CModule* pmodule = NULL;
    CModule* pmoduleNew = NULL;
    bool fAlreadyLoaded = false;
    Module_ID idModule(ulAppDomainID, guidModule);
    DWORD dwCurrentState = 0;

    ASSERT(IsValidObjectPtr(this, CDebugSymbolProvider));
    ASSERT(IsValidInterfacePtr(pUnkMetadataImport, IUnknown));

    METHOD_ENTRY( CDebugSymbolProvider::LoadSymbolsFromStream );

    IfFalseGo( pUnkMetadataImport, E_INVALIDARG );
    IfFalseGo( pUnkCorDebugModule, E_INVALIDARG );

    IfFailGo( pUnkMetadataImport->QueryInterface( IID_IMetaDataImport,
              (void**)&pMetadata) );

    IfFailGo( pUnkCorDebugModule->QueryInterface( IID_ICorDebugModule,
              (void**)&pCorModule) );

    ASSERT(guidModule != GUID_NULL);

    fAlreadyLoaded = GetModule( idModule, &pmodule ) == S_OK;

    IfNullGo( pmoduleNew = new CModule, E_OUTOFMEMORY );

    dwCurrentState = m_pSymProvGroup ? m_pSymProvGroup->GetCurrentState() : 0;

    IfFailGo( pmoduleNew->Create( idModule,
                                  dwCurrentState,
                                  pMetadata,
                                  pCorModule,
                                  pStream,
                                  baseOffset ) );

    if (fAlreadyLoaded)
    {
        IfFailGo(pmoduleNew->AddEquivalentModulesFrom(pmodule));
        RemoveModule(pmodule);
    }

    IfFailGo( AddModule( pmoduleNew ) );

Error:

    RELEASE (pmodule);
    RELEASE (pmoduleNew);

    METHOD_EXIT( CDebugSymbolProvider::LoadSymbolsFromStream, hr );

    return hr;
}
```

## <a name="see-also"></a>另请参阅
- [IDebugComPlusSymbolProvider2](../../../extensibility/debugger/reference/idebugcomplussymbolprovider2.md)

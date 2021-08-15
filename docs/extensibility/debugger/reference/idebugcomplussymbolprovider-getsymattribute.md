---
description: 检索具有指定模块的给定父属性的调试符号。
title: IDebugComPlusSymbolProvider：：GetSymAttribute |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugComPlusSymbolProvider::GetSymAttribute
- GetSymAttribute
ms.assetid: 6cbaac92-a60b-4165-a7f5-c34407770f3c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 59b0da0f176b4b55c507d1f44254a72aa955dacb5d352478e9f3fa17134f5cf4
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121417569"
---
# <a name="idebugcomplussymbolprovidergetsymattribute"></a>IDebugComPlusSymbolProvider::GetSymAttribute
检索具有指定模块的给定父属性的调试符号。

## <a name="syntax"></a>语法

```cpp
HRESULT GetSymAttribute (
    ULONG32  ulAppDomainID,
    GUID     guidModule,
    _mdToken tokParent,
    LPOLESTR pstrName,
    ULONG32  cBuffer,
    ULONG32* pcBuffer,
    BYTE*    buffer
);
```

```csharp
int GetSymAttribute (
    uint      ulAppDomainID,
    Guid      guidModule,
    int       tokParent,
    string    pstrName,
    uint      cBuffer,
    out uint  pcBuffer,
    out int[] buffer
);
```

## <a name="parameters"></a>参数
`ulAppDomainID`\
[in]应用程序域的标识符。

`guidModule`\
[in]模块的唯一标识符。

`tokParent`\
[in]父属性的标记。

`pstrName`\
[in]模块的名称。

`cBuffer`\
[in]输出 所需的字节数 `buffer` 。

`pcBuffer`\
[out]输出 的长度 `buffer` 。

`buffer`\
[out]包含符号的数组。

## <a name="return-value"></a>返回值
如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="example"></a>示例
下面的示例演示如何为公开 [IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)接口的 **CDebugSymbolProvider** 对象实现此方法。

```cpp
HRESULT CDebugSymbolProvider::GetSymAttribute(
    ULONG32 ulAppDomainID,
    GUID guidModule,
    _mdToken tokParent,
    __in_z LPOLESTR pstrName,
    ULONG32 cBuffer,
    ULONG32 *pcBuffer,
    BYTE buffer[])
{
    HRESULT hr = S_OK;
    CComPtr<CModule> pModule;
    Module_ID idModule(ulAppDomainID, guidModule);

    METHOD_ENTRY( CDebugSymbolProvider::GetSymAttribute );

    IfFailGo( GetModule( idModule, &pModule) );

    IfFailGo( pModule->GetSymAttribute( tokParent, pstrName, cBuffer, pcBuffer, buffer ) );

Error:

    METHOD_EXIT(CDebugSymbolProvider::GetSymAttribute, hr);

    return hr;
}
```

## <a name="see-also"></a>另请参阅
- [IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)

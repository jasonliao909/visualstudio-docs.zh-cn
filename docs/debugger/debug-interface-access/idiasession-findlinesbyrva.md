---
description: 检索包含指定相对虚拟地址 (RVA) 的指定编译单位中的行。
title: IDiaSession::findLinesByRVA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::findLinesByRVA method
ms.assetid: 06f53b0b-b5b4-42cf-9252-dcee0dbe2d71
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 89731647fa1de03d5ad3ae94b0357555d525de9c
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831891"
---
# <a name="idiasessionfindlinesbyrva"></a>IDiaSession::findLinesByRVA
检索包含指定相对虚拟地址 (RVA) 的指定编译单位中的行。

## <a name="syntax"></a>语法

```C++
HRESULT findLinesByRVA ( 
    DWORD                 rva,
    DWORD                 length,
    IDiaEnumLineNumbers** ppResult
);
```

#### <a name="parameters"></a>参数
`rva`

[in] 将地址指定为 RVA。

`length`

[in] 指定此查询要涵盖的地址范围的字节数。

`ppResult`

[out] 返回一个 [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md) 对象，该对象包含涵盖指定地址范围的所有行号的列表。

## <a name="return-value"></a>返回值
如果成功，则返回 `S_OK`；否则，返回错误代码。

## <a name="example"></a>示例
此示例演示一个函数，该函数使用函数的相对虚拟地址和长度获取指定函数中包含的所有行号。

```C++
IDiaEnumLineNumbers* GetLineNumbersByRVA(IDiaSymbol *pFunc, IDiaSession *pSession)
{
    IDiaEnumLineNumbers* pEnum = NULL;
    DWORD                rva;
    ULONGLONG            length;

    if (pFunc->get_relativeVirtualAddress ( &rva ) == S_OK)
    {
        pFunc->get_length ( &length );
        pSession->findLinesByRVA( rva, static_cast<DWORD>( length ), &pEnum );
    }
    return(pEnum);
}
```

## <a name="see-also"></a>另请参阅
- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)

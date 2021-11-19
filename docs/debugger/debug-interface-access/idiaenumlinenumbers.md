---
description: 枚举数据源中包含的各种行号。
title: IDiaEnumLineNumbers | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumLineNumbers interface
ms.assetid: cdf07b4f-19e4-4dcd-8af8-c2dbca586a7c
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 64fea0497f1cc8d8767a71eb4e06d77ae4b56e58
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832239"
---
# <a name="idiaenumlinenumbers"></a>IDiaEnumLineNumbers
枚举数据源中包含的各种行号。

## <a name="syntax"></a>语法

```
IDiaEnumLineNumbers : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
下表显示了 的方法 `IDiaEnumLineNumbers` 。

|方法|说明|
|------------|-----------------|
|[IDiaEnumLineNumbers::get__NewEnum](../../debugger/debug-interface-access/idiaenumlinenumbers-get-newenum.md)|检索此 [枚举数的 IEnumVARIANT](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-ienumvariant) 接口版本。|
|[IDiaEnumLineNumbers::get_Count](../../debugger/debug-interface-access/idiaenumlinenumbers-get-count.md)|检索行号数。|
|[IDiaEnumLineNumbers::Item](../../debugger/debug-interface-access/idiaenumlinenumbers-item.md)|通过索引检索行号。|
|[IDiaEnumLineNumbers::Next](../../debugger/debug-interface-access/idiaenumlinenumbers-next.md)|检索枚举序列中的指定行号数。|
|[IDiaEnumLineNumbers::Skip](../../debugger/debug-interface-access/idiaenumlinenumbers-skip.md)|跳过枚举序列中的指定行号数。|
|[IDiaEnumLineNumbers::Reset](../../debugger/debug-interface-access/idiaenumlinenumbers-reset.md)|将枚举序列重置为开头。|
|[IDiaEnumLineNumbers::Clone](../../debugger/debug-interface-access/idiaenumlinenumbers-clone.md)|创建一个枚举器，其中包含与当前枚举器相同的枚举状态。|

## <a name="remarks"></a>备注

## <a name="notes-for-callers"></a>调用方说明
此接口通过调用 [IDiaSession](../../debugger/debug-interface-access/idiasession.md) 接口中的以下方法之一获得：

- [IDiaSession::findLines](../../debugger/debug-interface-access/idiasession-findlines.md)

- [IDiaSession::findLinesByAddr](../../debugger/debug-interface-access/idiasession-findlinesbyaddr.md)

- [IDiaSession::findLinesByRVA](../../debugger/debug-interface-access/idiasession-findlinesbyrva.md)

- [IDiaSession::findLinesByVA](../../debugger/debug-interface-access/idiasession-findlinesbyva.md)

- [IDiaSession::findLinesByLinenum](../../debugger/debug-interface-access/idiasession-findlinesbylinenum.md)

## <a name="example"></a>示例
此示例演示如何从会话 `IDiaEnumLineNumbers` 获取 接口。 在这种情况下，该示例演示如何获取由 (表示的函数的行 `pSymbol`) 。 有关使用行号的更完整示例，请参阅 [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md) 接口。

```C++
void dumpFunctionLines( IDiaSymbol* pSymbol, IDiaSession* pSession )
{
    ULONGLONG length = 0;
    DWORD isect = 0;
    DWORD offset = 0;
    pSymbol->get_addressSection( &isect );
    pSymbol->get_addressOffset( &offset );
    pSymbol->get_length( &length );
    if ( isect != 0 && length > 0 )
    {
        CComPtr< IDiaEnumLineNumbers > pLines;
        if ( SUCCEEDED( pSession->findLinesByAddr(
                                      isect,
                                      offset,
                                      static_cast<DWORD>( length ),
                                      &pLines )
                      )
           )
        {
            // Do something with the enumeration
        }
    }
}
```

## <a name="requirements"></a>要求
标头：Dia2.h

库：diaguids.lib

DLL：msdia80.dll

## <a name="see-also"></a>另请参阅
- [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSession::findLinesByLinenum](../../debugger/debug-interface-access/idiasession-findlinesbylinenum.md)
- [IDiaSession::findLinesByRVA](../../debugger/debug-interface-access/idiasession-findlinesbyrva.md)
- [IDiaSession::findLinesByVA](../../debugger/debug-interface-access/idiasession-findlinesbyva.md)
- [IDiaSession::findLines](../../debugger/debug-interface-access/idiasession-findlines.md)
- [IDiaSession::findLinesByAddr](../../debugger/debug-interface-access/idiasession-findlinesbyaddr.md)

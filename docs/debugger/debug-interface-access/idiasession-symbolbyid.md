---
description: 按其唯一标识符检索符号。
title: IDiaSession::symbolById | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::symbolById method
ms.assetid: 062e4b5a-9c4d-4703-88da-ec13102c2b66
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 8f6f03339758ac3496f961313593c0b663fab30f
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831855"
---
# <a name="idiasessionsymbolbyid"></a>IDiaSession::symbolById
按其唯一标识符检索符号。

## <a name="syntax"></a>语法

```C++
HRESULT symbolById (
    DWORD        id,
    IDiaSymbol** ppSymbol
);
```

#### <a name="parameters"></a>参数
`id`

中唯一标识符。

`ppSymbol`

弄返回一个 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) 对象，该对象表示检索到的符号。

## <a name="return-value"></a>返回值
如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
指定的标识符是 DIA SDK 在内部用来使所有符号都唯一的唯一值。

例如，可以使用此方法来检索表示其他符号类型的符号 (参见示例) 。

## <a name="example"></a>示例
此示例检索表示另一个符号类型的 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) 。 此示例演示如何使用 `symbolById` 会话中的方法。 更简单的方法是调用 [IDiaSymbol：： get_type](../../debugger/debug-interface-access/idiasymbol-get-type.md) 方法直接检索类型符号。

```C++
IDiaSymbol *GetSymbolType(IDiaSymbol *pSymbol, IDiaSession *pSession)
{
    IDiaSymbol *pTypeSymbol = NULL;
    if (pSymbol != NULL && pSession != NULL)
    {
        DWORD symbolTypeId;
        pSymbol->get_typeId(&symbolTypeId);
        pSession->symbolById(symbolTypeId, &pTypeSymbol);
    }
    return(pTypeSymbol);
}
```

## <a name="see-also"></a>另请参阅
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [IDiaSymbol::get_type](../../debugger/debug-interface-access/idiasymbol-get-type.md)

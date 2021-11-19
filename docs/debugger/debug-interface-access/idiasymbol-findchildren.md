---
description: 检索符号的子项。
title: IDiaSymbol::findChildren | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::findChildren method
ms.assetid: 5fe7573a-e48b-428d-9c17-7421b7209246
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 72bd4479c50c6a518f4087c2244b2e194f5f05d5
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831812"
---
# <a name="idiasymbolfindchildren"></a>IDiaSymbol::findChildren
检索符号的子项。

## <a name="syntax"></a>语法

```C++
HRESULT findChildren ( 
   enum SymTagEnum   symtag,
   LPCOLESTR         name,
   DWORD             compareFlags,
   IDiaEnumSymbols** ppResult
);
```

#### <a name="parameters"></a>参数
 `symtag`

[in] 指定要检索的子项的符号标记，如 [SymTagEnum Enumeration](../../debugger/debug-interface-access/symtagenum.md) 中所定义。 对于要检索的所有子项，设置为 `SymTagNull`。

 `name`

[in] 指定要检索的子项的名称。 对于要检索的所有子项，设置为 `NULL`。

 `compareFlags`

[in] 指定应用于名称匹配的比较选项。 [NameSearchOptions Enumeration](../../debugger/debug-interface-access/namesearchoptions.md) 枚举中的值可以单独使用，也可以组合使用。

 `ppResult`

[out] 返回包含检索到的子符号列表的 [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md) 对象。

## <a name="return-value"></a>返回值
 如果找到至少一个符号子项，则返回 `S_OK`；如果未找到任何子项，则返回 `S_FALSE`；否则，返回错误代码。

## <a name="remarks"></a>备注
 此方法相当于将此符号用作第一个参数来调用 [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md) 方法。

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)
- [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)
- [NameSearchOptions 枚举](../../debugger/debug-interface-access/namesearchoptions.md)

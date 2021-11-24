---
description: 检索在指定虚拟地址处有效的符号的子项。
title: IDiaSymbol::findChildrenExByVA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::findChildrenExByVA
ms.assetid: 29080009-36e4-4697-acd7-50f2e3e1bf1b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 57157b7166f1720a8fb043751078c47f0b3da47a
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831752"
---
# <a name="idiasymbolfindchildrenexbyva"></a>IDiaSymbol::findChildrenExByVA
检索在指定虚拟地址处有效的符号的子项。

## <a name="syntax"></a>语法

```C++
HRESULT findChildrenExByVA ( 
   enum SymTagEnum   symtag,
   LPCOLESTR         name,
   DWORD             compareFlags,
   DWORD             address,
   IDiaEnumSymbols** ppResult
);
```

#### <a name="parameters"></a>参数
 `symtag`

[in] 指定要检索的子项的符号标记，如 [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)中所定义。 对于要检索的所有子项，设置为 `SymTagNull`。

 `name`

[in] 指定要检索的子项的名称。 对于要检索的所有子项，设置为 `NULL`。

 `compareFlags`

[in] 指定要应用于名称匹配的比较选项。 [NameSearchOptions Enumeration](../../debugger/debug-interface-access/namesearchoptions.md) 枚举中的值可以单独使用，也可以组合使用。

 `address`

[in] 指定虚拟地址。

 `ppResult`

[out] 返回包含检索到的子符号列表的 [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md) 对象。

## <a name="return-value"></a>返回值
 如果找到至少一个符号子项，则返回 `S_OK`；如果未找到任何子项，则返回 `S_FALSE`；否则，返回错误代码。

## <a name="remarks"></a>备注
 返回的本地符号包含实时范围信息。

## <a name="requirements"></a>要求
 标头：Dia2.h

 库：diaguids.lib

 DLL：msdia100.dll

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)
- [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)
- [NameSearchOptions 枚举](../../debugger/debug-interface-access/namesearchoptions.md)

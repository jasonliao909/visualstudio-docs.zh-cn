---
description: 检索在指定地址处有效的符号子级。
title: IDiaSymbol::findChildrenExByAddr | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::findChildrenExByAddr
ms.assetid: c1e7885d-2d15-4529-9ac2-32dd22efe31c
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 0be4ee10e4f343b36b16e5406c9f6d23d16d816d
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831758"
---
# <a name="idiasymbolfindchildrenexbyaddr"></a>IDiaSymbol::findChildrenExByAddr
检索在指定地址处有效的符号子级。

## <a name="syntax"></a>语法

```C++
HRESULT findChildrenExByAddr ( 
   enum SymTagEnum   symtag,
   LPCOLESTR         name,
   DWORD             compareFlags,
   DWORD             address,
   IDiaEnumSymbols** ppResult
);
```

#### <a name="parameters"></a>参数
 `symtag`

中指定要检索的子级的符号标记，如 [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)中所定义。 `SymTagNull`对于要检索的所有子级，将设置为。

 `name`

中指定要检索的子项的名称。 `NULL`对于要检索的所有子级，将设置为。

 `compareFlags`

中指定要应用于名称匹配的比较选项。 [NameSearchOptions 枚举](../../debugger/debug-interface-access/namesearchoptions.md)枚举中的值可以单独使用，也可以组合使用。

 `address`

中符号的地址。

 `ppResult`

弄返回一个 [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md) 对象，该对象包含所检索到的子符号的列表。

## <a name="return-value"></a>返回值
 `S_OK`如果找到至少一个符号子级，则返回 `S_FALSE` ; 如果未找到任何子级，则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 返回的本地符号包含实时范围信息。

## <a name="requirements"></a>要求
 标头： Dia2

 库： diaguids

 DLL： msdia100.dll

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)
- [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)
- [NameSearchOptions 枚举](../../debugger/debug-interface-access/namesearchoptions.md)

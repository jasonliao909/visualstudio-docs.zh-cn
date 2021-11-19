---
description: IDiaSymbol：： findInlineeLinesByRVA 检索一个枚举，该枚举允许客户端在此符号中直接或间接直接或间接地循环访问所有函数的行号信息 (RVA) 。
title: IDiaSymbol：： findInlineeLinesByRVA |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: ac108db1-9dbf-4dc4-bf48-159ca8d3725c
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: d0d1d7b83dd8e643dc5d25d71d43b50c039a8b25
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831747"
---
# <a name="idiasymbolfindinlineelinesbyrva"></a>IDiaSymbol::findInlineeLinesByRVA
检索一个枚举，该枚举允许客户端在此符号中直接或间接直接或间接地循环访问所有函数的行号信息 (RVA) 。

## <a name="syntax"></a>语法

```C++
HRESULT findInlineeLinesByRVA (    DWORD                 rva,   DWORD                 length,
   IDiaEnumLineNumbers** ppResult
);
```

#### <a name="parameters"></a>参数
 `rva`

中指定作为 RVA 的地址。

 `length`

中指定要用于此查询的地址范围（以字节数为单位）。

 `ppResult`

弄包含一个 `IDiaEnumLineNumbers` 对象，该对象包含所检索的行号的列表。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)
- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)
- [IDiaSession::findInlineeLines](../../debugger/debug-interface-access/idiasession-findinlineelines.md)

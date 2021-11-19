---
description: IDiaSession::findInlineeLinesByRVA 检索一个枚举，该枚举允许客户端遍历由指定的父符号直接或间接内联并包含在指定相对虚拟地址 (RVA) 中的所有函数的行号信息。
title: IDiaSession::findInlineeLinesByRVA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: 7a74d5ee-0dbf-47c0-92b4-47ec03b13ce9
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 1bb42c5d1ffed49c8bff3a6bc23f20f3cb9c86d5
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831907"
---
# <a name="idiasessionfindinlineelinesbyrva"></a>IDiaSession::findInlineeLinesByRVA
检索一个枚举，该枚举允许客户端遍历由指定的父符号直接或间接内联并包含在指定相对虚拟地址 (RVA) 中的所有函数的行号信息。

## <a name="syntax"></a>语法

```C++
HRESULT findInlineeLinesByRVA ( 
   IDiaSymbol*           parent,
   DWORD                 rva,
   DWORD                 length,
   IDiaEnumLineNumbers** ppResult
);
```

#### <a name="parameters"></a>参数
 `parent`

[in] 表示父级的 `IDiaSymbol` 对象。

 `rva`

[in] 将地址指定为 RVA。

 `length`

[in] 指定此查询要涵盖的地址范围（以字节数为单位）。

 `ppResult`

[out] 保留 `IDiaEnumLineNumbers` 对象，其中包含已检索的行号的列表。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)
- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)

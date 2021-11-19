---
description: IDiaSession：： findInlineeLinesByRVA 检索允许客户端通过指定的父符号直接或间接地循环访问所有函数的行号信息的枚举，这些函数包含在指定的相对虚拟地址 (RVA) 内。
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
检索一个枚举，该枚举允许客户端通过指定的父符号直接或间接地循环访问所有函数的行号信息，并将其包含在指定的相对虚拟地址 (RVA) 内。

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

中 `IDiaSymbol` 表示父对象的对象。

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

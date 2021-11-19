---
description: IDiaSession::findInlineeLinesByVA 检索一个枚举，该枚举允许客户端遍历由指定的父符号直接或间接内联并包含在指定虚拟地址 (VA) 中的所有函数的行号信息。
title: IDiaSession::findInlineeLinesByVA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: dffe6594-e0d1-4ed5-aeea-8773f88d82a6
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 7b14bbe058ef074d8173d5c11b37130abf576d9a
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831906"
---
# <a name="idiasessionfindinlineelinesbyva"></a>IDiaSession::findInlineeLinesByVA
检索一个枚举，该枚举允许客户端遍历由指定的父符号直接或间接内联并包含在指定虚拟地址 (VA) 中的所有函数的行号信息。

## <a name="syntax"></a>语法

```C++
HRESULT findInlineeLinesByVA ( 
   IDiaSymbol*           parent,   ULONGLONG             va,   DWORD                 length,
   IDiaEnumLineNumbers** ppResult
);
```

#### <a name="parameters"></a>参数
 `parent`

[in] 表示父级的 `IDiaSymbol` 对象。

 `va`

[in] 将地址指定为 VA。

 `length`

[in] 指定此查询要涵盖的地址范围（以字节数为单位）。

 `ppResult`

[out] 保留包含已检索的行号的列表的 `IDiaEnumLineNumbers` 对象。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)
- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)

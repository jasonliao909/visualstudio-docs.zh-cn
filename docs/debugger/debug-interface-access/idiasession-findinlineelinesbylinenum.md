---
description: 检索枚举，该枚举允许客户端在指定的源文件和行号中直接或间接地内向访问所有函数的行号信息。
title: IDiaSession::findInlineeLinesByLinenum | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: cf32ae7c-a0c8-4800-bc8f-d64fdd15fb06
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 4d1260c11aa8e737f9188b86de44cd8e6fdf33cb
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831917"
---
# <a name="idiasessionfindinlineelinesbylinenum"></a>IDiaSession::findInlineeLinesByLinenum
检索枚举，该枚举允许客户端在指定的源文件和行号中直接或间接地内向访问所有函数的行号信息。

## <a name="syntax"></a>语法

```C++
HRESULT findInlineeLinesByVA ( 
   IDiaSymbol*           compiland,
   IDiaSourceFile*       file,
   DWORD                 linenum,
   DWORD                 column,
   IDiaEnumLineNumbers** ppResult
);
```

#### <a name="parameters"></a>参数
 `compiland`

[in]一 [个 IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) 对象，表示要搜索行号的 compiland。 此参数不能为 `NULL`。

 `file`

[in]表示要搜索的源文件的 [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md) 对象。 此参数不能为 `NULL`。

 `linenum`

[in]指定从 1 到 1 的行号。

> [!NOTE]
> 不能使用零指定所有行 ([IDiaSession：：findLines](../../debugger/debug-interface-access/idiasession-findlines.md) 方法查找所有行) 。

 `column`

[in]指定列号。 使用零指定所有列。 列是行中的字节偏移量。

 `ppResult`

[out]返回一 [个 IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md) 对象，该对象包含检索到的行号列表。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)
- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)

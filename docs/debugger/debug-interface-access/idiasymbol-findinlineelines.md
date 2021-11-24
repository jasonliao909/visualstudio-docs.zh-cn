---
description: 检索一个枚举，该枚举允许客户端遍历此符号中直接或间接内联的所有函数的行号信息。
title: IDiaSymbol::findInlineeLines | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: 56ba4bc0-8f96-47c2-8b18-332b4e7c2d91
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: df3fcddf2f31282d27e6f9a5744f2cf8592d2a1e
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831750"
---
# <a name="idiasymbolfindinlineelines"></a>IDiaSymbol::findInlineeLines
检索一个枚举，该枚举允许客户端遍历此符号中直接或间接内联的所有函数的行号信息。

## <a name="syntax"></a>语法

```C++
HRESULT findInlineeLines ( 
   IDiaEnumLineNumbers** ppResult
);
```

#### <a name="parameters"></a>参数
 `ppResult`

[out] 保留包含已检索的行号的列表的 `IDiaEnumLineNumbers` 对象。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)
- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)
- [IDiaSession::findInlineeLines](../../debugger/debug-interface-access/idiasession-findinlineelines.md)

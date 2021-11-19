---
description: IDiaSymbol::findInlineeLinesByAddr 检索一个枚举，该枚举允许客户端遍历指定地址范围内直接或间接内联到此符号中的所有函数的行号信息。
title: IDiaSymbol::findInlineeLinesByAddr | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: f1ab47ca-c851-48ea-9c12-47fb80b31102
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 57eb156d96d20f1c1032980c31309c93519ab844
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831749"
---
# <a name="idiasymbolfindinlineelinesbyaddr"></a>IDiaSymbol::findInlineeLinesByAddr
检索一个枚举，该枚举允许客户端遍历指定地址范围内直接或间接内联到此符号中的所有函数的行号信息。

## <a name="syntax"></a>语法

```C++
HRESULT findInlineeLinesByAddr ( 
   DWORD                 isect,
   DWORD                 offset,
   DWORD                 length,
   IDiaEnumLineNumbers** ppResult
);
```

#### <a name="parameters"></a>参数
 `isect`

[in] 指定地址的节组件。

 `offset`

[in] 指定地址的偏移量组件。

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
- [IDiaSession::findInlineeLines](../../debugger/debug-interface-access/idiasession-findinlineelines.md)

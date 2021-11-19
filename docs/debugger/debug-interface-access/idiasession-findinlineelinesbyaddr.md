---
description: IDiaSession：：findInlineeLinesByAddr 检索枚举，该枚举允许客户端通过指定父符号直接或间接内联并包含在指定地址范围内的所有函数的行号信息进行重新访问。
title: IDiaSession::findInlineeLinesByAddr | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: bb70e408-eed1-4c9c-b5b1-44323125f48b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: f8a8c4b8ccf42012557d87581c212cea95cda552
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831908"
---
# <a name="idiasessionfindinlineelinesbyaddr"></a>IDiaSession::findInlineeLinesByAddr
检索一个 枚举，该枚举允许客户端通过指定父符号直接或间接地内向访问所有函数的行号信息，这些信息包含在指定的地址范围内。

## <a name="syntax"></a>语法

```C++
HRESULT findInlineeLinesByAddr ( 
   IDiaSymbol*           parent,   DWORD                 isect,   DWORD                 offset,   DWORD                 length,
   IDiaEnumLineNumbers** ppResult
);
```

#### <a name="parameters"></a>参数
 `parent`

[in]一 `IDiaSymbol` 个表示父级的对象。

 `isect`

[in]指定地址的节组件。

 `offset`

[in]指定地址的偏移部分。

 `length`

[in]指定要在此查询中覆盖的地址范围（以字节数为单位）。

 `ppResult`

[out]保存 `IDiaEnumLineNumbers` 一个 对象，该对象包含检索到的行号列表。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)
- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)

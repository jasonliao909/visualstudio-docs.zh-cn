---
description: IDiaSession：： findInlineeLinesByVA 检索允许客户端通过指定的父符号直接或间接地循环访问所有函数的行号信息的枚举，并将其包含在指定的虚拟地址 (VA) 中。
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
检索一个枚举，该枚举允许客户端通过指定的父符号直接或间接地循环访问所有函数的行号信息，并将其包含在指定的虚拟地址 (VA) 中。

## <a name="syntax"></a>语法

```C++
HRESULT findInlineeLinesByVA ( 
   IDiaSymbol*           parent,   ULONGLONG             va,   DWORD                 length,
   IDiaEnumLineNumbers** ppResult
);
```

#### <a name="parameters"></a>参数
 `parent`

中 `IDiaSymbol` 表示父对象的对象。

 `va`

中指定地址作为 VA。

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

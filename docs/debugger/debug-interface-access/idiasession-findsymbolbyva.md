---
description: 检索包含或最接近指定虚拟的指定符号类型。
title: IDiaSession::findSymbolByVA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::findSymbolByVA method
ms.assetid: 0350df23-9a5d-4e8d-8c26-7f571d8fb1af
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 1a76c3e03e38ff48501b9cc20fb580a41cdb9d55
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831877"
---
# <a name="idiasessionfindsymbolbyva"></a>IDiaSession::findSymbolByVA
检索包含或最接近指定虚拟的指定符号类型。

## <a name="syntax"></a>语法

```C++
HRESULT findSymbolByVA ( 
   ULONGLONG    va,
   SymTagEnum   symtag,
   IDiaSymbol** ppSymbol
);
```

#### <a name="parameters"></a>参数
 `va`

[in] 指定虚拟地址。

 `symtag`

[in] 要查找的符号类型。 值来自 [SymTagEnum Enumeration](../../debugger/debug-interface-access/symtagenum.md) 枚举。

 `ppSymbol`

[out] 返回表示检索到的符号的 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) 对象。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。

## <a name="example"></a>示例

```C++
IDiaSymbol* pFunc;
pSession->findSymbolByVA( va, SymTagFunction, &pFunc );
```

## <a name="see-also"></a>另请参阅
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)

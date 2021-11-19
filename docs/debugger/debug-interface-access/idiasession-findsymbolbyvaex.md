---
description: 检索包含或最接近指定虚拟地址 (VA) 和偏移量的指定符号类型。
title: IDiaSession::findSymbolByVAEx | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::findSymbolByVAEx method
ms.assetid: 11c685f6-cda2-4474-a432-214ecaae4ffa
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: a1ed6cb63f2d0a8fed11d995d7cbc748461edf70
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831875"
---
# <a name="idiasessionfindsymbolbyvaex"></a>IDiaSession::findSymbolByVAEx
检索包含或最接近指定虚拟地址 (VA) 和偏移量的指定符号类型。

## <a name="syntax"></a>语法

```C++
HRESULT findSymbolByVAEx ( 
   ULONGLONG    va,
   SymTagEnum   symtag,
   IDiaSymbol** ppSymbol,
   LONG*        displacement
);
```

#### <a name="parameters"></a>参数
 `va`

[in] 指定 VA。

 `symtag`

[in] 要查找的符号类型。 值来自 [SymTagEnum Enumeration](../../debugger/debug-interface-access/symtagenum.md) 枚举。

 `ppSymbol`

[out] 返回表示检索到的符号的 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) 对象。

 `displacement`

[out] 返回指定 `va` 给定的虚拟地址的偏移量的值。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。

## <a name="example"></a>示例

```C++
IDiaSymbol* pFunc;
LONG disp = 0;
pSession->findSymbolByVAEx( va, SymTagFunction, &pFunc, &disp );
```

## <a name="see-also"></a>另请参阅
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)
- [IDiaSession::findSymbolByVA](../../debugger/debug-interface-access/idiasession-findsymbolbyva.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)

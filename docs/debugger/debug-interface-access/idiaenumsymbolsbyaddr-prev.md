---
description: 按地址顺序检索以前的符号。
title: IDiaEnumSymbolsByAddr::Prev | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSymbolsByAddr::Prev method
ms.assetid: da3b3dca-68cb-4cb0-b25c-e28a1ffe49d3
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 97bba21a09d13706375f6b97897e307c46385294
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832162"
---
# <a name="idiaenumsymbolsbyaddrprev"></a>IDiaEnumSymbolsByAddr::Prev
按地址顺序检索以前的符号。

## <a name="syntax"></a>语法

```C++
HRESULT Prev ( 
   ULONG        celt,
   IDiaSymbol** rgelt,
   ULONG*       pceltFetched
);
```

#### <a name="parameters"></a>参数
 celt

[in] 要检索的枚举器中的符号数。

 rgelt

[out] 要用表示所需符号的 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) 对象填充的数组。

 pceltFetched

[out] 返回提取的枚举器中的符号数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果没有以前的符号，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="remarks"></a>备注
 此方法按提取的元素数更新枚举器位置。

## <a name="see-also"></a>另请参阅
- [IDiaEnumSymbolsByAddr](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)

---
description: 按地址顺序检索后面的符号。
title: IDiaEnumSymbolsByAddr::Next | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSymbolsByAddr::Next method
ms.assetid: a1320587-7ce7-401f-9548-2f8bcece5cc3
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: b509c84c9ee0fe81a7c9532bbc6f218af277df5d
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832166"
---
# <a name="idiaenumsymbolsbyaddrnext"></a>IDiaEnumSymbolsByAddr::Next
按地址顺序检索后面的符号。

## <a name="syntax"></a>语法

```C++
HRESULT Next ( 
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
 如果成功，则返回 `S_OK`。 如果没有更多符号，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="remarks"></a>备注
 此方法按提取的元素数更新枚举器位置。

## <a name="see-also"></a>另请参阅
- [IDiaEnumSymbolsByAddr](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)

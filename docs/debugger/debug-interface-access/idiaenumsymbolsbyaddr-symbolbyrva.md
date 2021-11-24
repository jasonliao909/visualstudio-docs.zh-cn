---
description: 通过按相对虚拟地址 (RVA) 执行查找来定位枚举器。
title: IDiaEnumSymbolsByAddr::symbolByRVA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSymbolsByAddr::symbolByRVA method
ms.assetid: f7828029-f2ee-4ccd-afac-785adc60a4c8
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: f223845e1d83a1f12c58973fa6ccb644b9902b8a
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832159"
---
# <a name="idiaenumsymbolsbyaddrsymbolbyrva"></a>IDiaEnumSymbolsByAddr::symbolByRVA
通过按相对虚拟地址 (RVA) 执行查找来定位枚举器。

## <a name="syntax"></a>语法

```C++
HRESULT symbolByRVA ( 
   DWORD**      relativeVirtualAddress,
   IDiaSymbol** ppsymbol
);
```

#### <a name="parameters"></a>参数
 relativeVirtualAddress

[in] 相对于图像开头的地址。

 ppsymbol

[out] 返回表示找到的符号的 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) 对象。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果找不到符号，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaEnumSymbolsByAddr](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr.md)
- [IDiaEnumSymbolsByAddr::symbolByVA](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr-symbolbyva.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)

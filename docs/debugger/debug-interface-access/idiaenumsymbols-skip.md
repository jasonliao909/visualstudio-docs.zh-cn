---
description: 跳过枚举序列中指定数量的符号。
title: IDiaEnumSymbols::Skip | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSymbols::Skip method
ms.assetid: e601fbc9-b10b-41c7-8180-959e57efabe8
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 34a278abc20ef939cd038813b4e2ed07b20b1bcf
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832168"
---
# <a name="idiaenumsymbolsskip"></a>IDiaEnumSymbols::Skip
跳过枚举序列中指定数量的符号。

## <a name="syntax"></a>语法

```C++
HRESULT Skip ( 
   ULONG celt
);
```

#### <a name="parameters"></a>参数
 celt

[in] 枚举序列中要跳过的符号数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；如果没有更多要跳过的符号，则返回 `S_FALSE`。

## <a name="see-also"></a>另请参阅
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)

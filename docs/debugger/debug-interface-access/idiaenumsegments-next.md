---
description: 检索枚举序列中指定数目的段。
title: IDiaEnumSegments::Next | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSegments::Next method
ms.assetid: 53f61874-d821-47ab-a1f5-27e982804a6a
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 5aaed8e83a49ab31844d7fddd5f8e036fdc0d6cd
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832213"
---
# <a name="idiaenumsegmentsnext"></a>IDiaEnumSegments::Next
检索枚举序列中指定数目的段。

## <a name="syntax"></a>语法

```C++
HRESULT Next ( 
   ULONG         celt,
   IDiaSegment** rgelt,
   ULONG*        pceltFetched
);
```

#### <a name="parameters"></a>参数
 celt

[in] 要检索的枚举器中的段数。

 rgelt

[out] 要用表示段的所需 [IDiaSegment](../../debugger/debug-interface-access/idiasegment.md) 对象填充的数组。

 pceltFetched

[out] 返回提取的枚举器中的段数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果没有更多段，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaEnumSegments](../../debugger/debug-interface-access/idiaenumsegments.md)
- [IDiaSegment](../../debugger/debug-interface-access/idiasegment.md)

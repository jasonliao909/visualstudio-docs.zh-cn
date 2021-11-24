---
description: 跳过枚举序列中指定数量的段。
title: IDiaEnumSegments::Skip | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSegments::Skip method
ms.assetid: ec67039f-da8c-4e70-8db7-957d7d5281e8
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 22479a35faf797969eb7936c6d630e91f7f6352b
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832207"
---
# <a name="idiaenumsegmentsskip"></a>IDiaEnumSegments::Skip
跳过枚举序列中指定数量的段。

## <a name="syntax"></a>语法

```C++
HRESULT Skip ( 
   ULONG celt
);
```

#### <a name="parameters"></a>参数
 celt

[in] 枚举序列中要跳过的段数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；如果没有更多要跳过的段，则返回 `S_FALSE`。

## <a name="see-also"></a>另请参阅
- [IDiaEnumSegments](../../debugger/debug-interface-access/idiaenumsegments.md)

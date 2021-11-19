---
description: 检索枚举序列中指定数量的帧数据元素。
title: IDiaEnumFrameData::Next | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumFrameData::Next method
ms.assetid: 546e2e23-efb2-425a-96a1-808c67c519fb
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 57324a0ec9b82ff0b32f16ebf32f8d3ee9e19fb5
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832276"
---
# <a name="idiaenumframedatanext"></a>IDiaEnumFrameData::Next
检索枚举序列中指定数量的帧数据元素。

## <a name="syntax"></a>语法

```C++
HRESULT Next ( 
   ULONG           celt,
   IDiaFrameData** rgelt,
   ULONG*          pceltFetched
);
```

#### <a name="parameters"></a>参数
 celt

[in] 要检索的枚举器中的帧数据元素数。

 rgelt

[out] 要用请求的帧数据元素填充的 [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md) 对象的数组。

 pceltFetched

[out] 返回提取的枚举器中的帧数据元素数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果没有更多记录，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md)
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)

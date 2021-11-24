---
description: 跳过枚举序列中指定数量的帧数据元素。
title: IDiaEnumFrameData::Skip | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumFrameData::Skip method
ms.assetid: 67140b4c-7125-4895-932d-42412326da29
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 50c7069e47533e65273ffd988eed676a59376a1e
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832274"
---
# <a name="idiaenumframedataskip"></a>IDiaEnumFrameData::Skip
跳过枚举序列中指定数量的帧数据元素。

## <a name="syntax"></a>语法

```C++
HRESULT Skip ( 
   ULONG celt
);
```

#### <a name="parameters"></a>参数
 celt

[in] 枚举序列中要跳过的帧数据元素的数量。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；如果没有更多要跳过的记录，则返回 `S_FALSE`。

## <a name="see-also"></a>另请参阅
- [IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md)

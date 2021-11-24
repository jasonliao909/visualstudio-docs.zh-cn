---
description: 跳过枚举序列中指定数量的调试流。
title: IDiaEnumDebugStreams::Skip | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumDebugStreams::Skip method
ms.assetid: 6ec7753c-d7af-4879-b107-1b3442e0b025
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 6c6c83d059455cc6046547af079de022bb7447d3
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832286"
---
# <a name="idiaenumdebugstreamsskip"></a>IDiaEnumDebugStreams::Skip
跳过枚举序列中指定数量的调试流。

## <a name="syntax"></a>语法

```C++
HRESULT Skip ( 
   ULONG celt
);
```

#### <a name="parameters"></a>参数
 `celt`

[in] 枚举序列中要跳过的调试流数量。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；如果没有更多要跳过的记录，则返回 `S_FALSE`。

## <a name="see-also"></a>另请参阅
- [IDiaEnumDebugStreams](../../debugger/debug-interface-access/idiaenumdebugstreams.md)

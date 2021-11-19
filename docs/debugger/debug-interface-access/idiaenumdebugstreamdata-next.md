---
description: 检索枚举序列中的指定记录数。
title: IDiaEnumDebugStreamData：：Next |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumDebugStreamData::Next method
ms.assetid: 114171dd-38fd-4bd7-a702-8ff887ffc99b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 8b67d12b983ef13ad92ee8a121d8733d435f7b7c
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832310"
---
# <a name="idiaenumdebugstreamdatanext"></a>IDiaEnumDebugStreamData::Next
检索枚举序列中的指定记录数。

## <a name="syntax"></a>语法

```C++
HRESULT Next ( 
   ULONG  celt,
   DWORD  cbData,
   DWORD* pcbData,
   BYTE   data[],
   ULONG* pceltFetched
);
```

#### <a name="parameters"></a>参数
 celt

[in]要检索的记录数。

 cbData

[in]数据缓冲区的大小（以字节为单位）。

 pcbData

[out]返回返回的字节数。 如果 `data` 为 NULL， `pcbData` 则包含所有请求的记录可用的数据总字节数。

 data[]

[out]使用调试流记录数据填充的缓冲区。

 pceltFetched

[in， out]返回 中的记录数 `data` 。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果没有 `S_FALSE` 更多记录，则返回 。 否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaEnumDebugStreamData](../../debugger/debug-interface-access/idiaenumdebugstreamdata.md)
- [IDiaEnumDebugStreams::Next](../../debugger/debug-interface-access/idiaenumdebugstreams-next.md)

---
description: 检索指定的记录。
title: IDiaEnumDebugStreamData：：Item |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumDebugStreamData::Item method
ms.assetid: 761e61a5-44a6-4d5d-a98e-c2e9b89d2343
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: fdffa847b40b7e2a2d3bf961d9daa15abc82fb0b
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832315"
---
# <a name="idiaenumdebugstreamdataitem"></a>IDiaEnumDebugStreamData::Item
检索指定的记录。

## <a name="syntax"></a>语法

```C++
HRESULT Item ( 
   DWORD  index,
   DWORD  cbData,
   DWORD* pcbData,
   BYTE   data[]
);
```

#### <a name="parameters"></a>参数
 索引

[in]要检索的记录的索引。 索引的范围为 0 到 `count` -1，其中 `count` 由[IDiaEnumDebugStreamData：：get_Count。](../../debugger/debug-interface-access/idiaenumdebugstreamdata-get-count.md)

 cbData

[in]数据缓冲区的大小（以字节为单位）。

 pcbData

[out]返回返回的字节数。 如果 `data` `NULL` 为 ， `pcbData` 则包含指定记录中可用数据的总字节数。

 data[]

[out]用调试流记录数据填充的缓冲区。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。 如果 `E_INVALIDARG` 参数在边界外，则返回无效 `index` 参数和 。

## <a name="see-also"></a>另请参阅
- [IDiaEnumDebugStreamData](../../debugger/debug-interface-access/idiaenumdebugstreamdata.md)
- [IDiaEnumDebugStreamData::Next](../../debugger/debug-interface-access/idiaenumdebugstreamdata-next.md)
- [IDiaEnumDebugStreams::Item](../../debugger/debug-interface-access/idiaenumdebugstreams-item.md)
- [IDiaEnumDebugStreamData::get_Count](../../debugger/debug-interface-access/idiaenumdebugstreamdata-get-count.md)
- [IDiaEnumDebugStreamData::Skip](../../debugger/debug-interface-access/idiaenumdebugstreamdata-skip.md)

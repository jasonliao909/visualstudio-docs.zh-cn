---
description: 检索源代码字节。
title: IDiaInjectedSource：：get_source |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaInjectedSource::get_source method
ms.assetid: 3c0b5386-321f-4f8f-85cc-e2ee7b4cc3d2
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: bd210d3d4130d94193abec38c41bda7bce67eaaa
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832083"
---
# <a name="idiainjectedsourceget_source"></a>IDiaInjectedSource::get_source
检索源代码字节。

## <a name="syntax"></a>语法

```C++
HRESULT get_source ( 
   DWORD  cbData,
   DWORD* pcbData,
   BYTE   data[]
);
```

#### <a name="parameters"></a>参数
 `cbData`

[in]表示数据缓冲区大小的字节数。

 `pcbData`

[out]返回表示返回的字节的字节数。 如果 `data` `NULL` 为 ， `pcbData` 则 是可用数据的总字节数。

 `data[]`

[out]使用源字节填充的缓冲区。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果 `S_FALSE` 不支持此属性，则返回 。 否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)

---
description: 检索根据源代码的字节计算出的循环冗余检验 (CRC)。
title: IDiaInjectedSource::get_crc | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaInjectedSource::get_crc method
ms.assetid: 2ecdda93-950e-40d6-b79b-4ae3c55b6cfc
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 396a0742b2ac2c3afd8d2868326a701f6f0da6d5
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832088"
---
# <a name="idiainjectedsourceget_crc"></a>IDiaInjectedSource::get_crc
检索根据源代码的字节计算出的循环冗余检验 (CRC)。

## <a name="syntax"></a>语法

```C++
HRESULT get_crc ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 返回根据源代码的字节计算出的 CRC。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果不支持此属性，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)

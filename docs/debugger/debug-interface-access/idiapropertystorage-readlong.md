---
description: 读取属性集中的 LONG 值。
title: IDiaPropertyStorage::ReadLONG | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaPropertyStorage::ReadLONG
ms.assetid: 32054cbc-db55-4513-a1b4-de80e77aac8a
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 5112970758a037754c61064ca073c79e950bafb4
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832017"
---
# <a name="idiapropertystoragereadlong"></a>IDiaPropertyStorage::ReadLONG
读取属性集中的 `LONG` 值。

## <a name="syntax"></a>语法

```C++
HRESULT ReadDLONG ( 
   PROPID id,
   LONG*  pValue
);
```

#### <a name="parameters"></a>参数
 `id`

[in] 要读取的属性的标识符（`PROPID` 在 WTypes.h 中定义为 `ULONG`）。

 `pValue`

[out] 返回属性值。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。 如果此属性的类型不是 `LONG`，则返回 `E_INVALIDARG`。

## <a name="remarks"></a>备注
 `LONG` 由 Windows 定义为 32 位带符号整数。

## <a name="see-also"></a>另请参阅
- [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)

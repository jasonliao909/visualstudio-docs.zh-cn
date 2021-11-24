---
description: 读取属性集中的 ULONGLONG 值。
title: IDiaPropertyStorage::ReadULONGLONG | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaPropertyStorage::ReadULONGLONG
ms.assetid: f80a2e24-5744-4fec-bab0-3ed51aef6e58
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 5434587770fb632cc353bc5254902a9fb3614c37
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832008"
---
# <a name="idiapropertystoragereadulonglong"></a>IDiaPropertyStorage::ReadULONGLONG
读取属性集中的 `ULONGLONG` 值。

## <a name="syntax"></a>语法

```C++
HRESULT ReadULONGLONG ( 
   PROPID     id,
   ULONGLONG* pValue
);
```

#### <a name="parameters"></a>参数
 `id`

[in] 要读取的属性的标识符（`PROPID` 在 WTypes.h 中定义为 `ULONG`）。

 `pValue`

[out] 返回属性值。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。 如果此属性的类型不是 `ULONGLONG`，则返回 `E_INVALIDARG`。

## <a name="remarks"></a>备注
 `ULONGLONG` 由 Windows 定义为 64 位无符号整数。

## <a name="see-also"></a>另请参阅
- [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)

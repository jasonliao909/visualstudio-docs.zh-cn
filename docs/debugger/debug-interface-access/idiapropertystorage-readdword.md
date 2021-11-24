---
description: 读取属性集中的 DWORD 值。
title: IDiaPropertyStorage::ReadDWORD | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaPropertyStorage::ReadDWORD
ms.assetid: 5f4c034e-a9d3-4560-94b5-ede524741439
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 58b51638b742fa8dfe874c4d46ff7bd0894f7766
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832018"
---
# <a name="idiapropertystoragereaddword"></a>IDiaPropertyStorage::ReadDWORD
读取属性集中的 `DWORD` 值。

## <a name="syntax"></a>语法

```C++
HRESULT ReadDWORD ( 
   PROPID id,
   DWORD* pValue
);
```

#### <a name="parameters"></a>参数
 `id`

[in] 要读取的属性的标识符（`PROPID` 在 WTypes.h 中定义为 `ULONG`）。

 `pValue`

[out] 返回属性值。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。 如果此属性的类型不是 `DWORD`，则返回 `E_INVALIDARG`。

## <a name="remarks"></a>备注
 `DWORD` 由 Windows 定义为 32 位无符号整数。

## <a name="see-also"></a>另请参阅
- [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)

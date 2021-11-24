---
description: 读取属性集中的 BOOL 值。
title: IDiaPropertyStorage::ReadBOOL | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaPropertyStorage::ReadBOOL
ms.assetid: ad1822db-4572-48f7-9919-f8137f6701f2
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: e9b2ba2f6e86522f5770aec30b1617742054cd9a
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832027"
---
# <a name="idiapropertystoragereadbool"></a>IDiaPropertyStorage::ReadBOOL
读取属性集中的 `BOOL` 值。

## <a name="syntax"></a>语法

```C++
HRESULT ReadBOOL ( 
   PROPID id,
   BOOL*  pValue
);
```

#### <a name="parameters"></a>参数
 `id`

[in] 要读取的属性的标识符（`PROPID` 在 WTypes.h 中定义为 `ULONG`）。

 `pValue`

[out] 返回属性值。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。 如果此属性的类型不是 `BOOL`，则返回 `E_INVALIDARG`。

## <a name="remarks"></a>备注
 为了得到一致的结果，请解释 `BOOL` 值，使非零值为 `TRUE`，零为 `FALSE`。

## <a name="see-also"></a>另请参阅
- [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)

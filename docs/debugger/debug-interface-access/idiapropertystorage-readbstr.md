---
description: 读取属性集中的 BSTR 值。
title: IDiaPropertyStorage::ReadBSTR | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaPropertyStorage::ReadBSTR
ms.assetid: 7214643b-3286-48ed-90aa-0fe95b4cae5b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 8294b245f2bb71d1cf46abcfd555db23b3ceebe9
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832019"
---
# <a name="idiapropertystoragereadbstr"></a>IDiaPropertyStorage::ReadBSTR
读取属性集中的 `BSTR` 值。

## <a name="syntax"></a>语法

```C++
HRESULT ReadBSTR ( 
   PROPID id,
   BSTR*  pValue
);
```

#### <a name="parameters"></a>参数
 `id`

[in] 要读取的属性的标识符（`PROPID` 在 WTypes.h 中定义为 `ULONG`）。

 `pValue`

[out] 返回属性值。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。 如果此属性的类型不是 `BSTR`，则返回 `E_INVALIDARG`。

## <a name="remarks"></a>备注
 `BSTR` 由 Windows 定义为以零结尾的宽字符字符串。

## <a name="see-also"></a>另请参阅
- [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)

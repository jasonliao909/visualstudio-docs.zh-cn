---
description: 检索给定属性标识符对应的字符串名称。
title: IDiaPropertyStorage::ReadPropertyNames | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaPropertyStorage::ReadPropertyNames
ms.assetid: f8bcab77-afca-4a8f-8710-697842f8a518
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 3c49a688fe1ecf9892ec5943934749694e8a839b
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832009"
---
# <a name="idiapropertystoragereadpropertynames"></a>IDiaPropertyStorage::ReadPropertyNames
检索给定属性标识符对应的字符串名称。

## <a name="syntax"></a>语法

```C++
HRESULT ReadPropertyNames (
   ULONG         cpropid,
   PROPID const* rgpropid,
   BSTR*         rglpwstrName
);
```

#### <a name="parameters"></a>参数
 `cpropid`

[in] `rgpropid` 中的属性 ID 数。

 `rgpropid`

[in] 要为其获取名称的属性 ID 的数组（`PROPID` 在 WTypes.h 中定义为 `ULONG`）。

 `rglpwstrName`

[in, out] 指定属性 ID 的属性名称的数组。 必须预先分配数组以保留请求数量的属性名称，并且必须能够至少保留 `cpropid``BSTR` 字符串。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。

## <a name="remarks"></a>备注
 不再需要时，必须释放返回的属性名称（通过调用 `SysFreeString` 函数）。

## <a name="see-also"></a>另请参阅
- [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)

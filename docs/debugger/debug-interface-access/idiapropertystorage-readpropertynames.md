---
description: 检索给定属性标识符的相应字符串名称。
title: IDiaPropertyStorage：：ReadPropertyNames |Microsoft Docs
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
检索给定属性标识符的相应字符串名称。

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

[in]中的属性 ID 数 `rgpropid` 。

 `rgpropid`

[in]要获取其名称的属性 ID 数组 (`PROPID` WTypes.h 中定义为 `ULONG`) 。

 `rglpwstrName`

[in， out]指定属性 ID 的属性名称数组。 必须预先分配数组以保存请求的属性名称数，并且必须能够保存至少字符串 `cpropid``BSTR` 。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 返回的属性名称必须释放 (不再需要时) `SysFreeString` 函数名称。

## <a name="see-also"></a>另请参阅
- [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)

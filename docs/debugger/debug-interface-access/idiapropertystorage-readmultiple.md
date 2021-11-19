---
description: 从当前属性集中读取指定的属性。
title: IDiaPropertyStorage：： ReadMultiple |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaPropertyStorage::ReadMultiple
ms.assetid: 6ccc9397-ce41-4f72-b261-72ac252cd4a5
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 1594d7137ec6c34c794f588f7a126bdb1392462b
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832016"
---
# <a name="idiapropertystoragereadmultiple"></a>IDiaPropertyStorage::ReadMultiple
从当前属性集中读取指定的属性。

## <a name="syntax"></a>语法

```C++
HRESULT ReadMultiple( 
   ULONG          cpspec,
   PROPSPEC const rgpspec,
   PROPVARIANT    rgvar
);
```

#### <a name="parameters"></a>参数
 `cpspec`

中数组中指定的属性计数 `rgpspec` 。 如果为零，则此方法不返回任何属性，但会 `S_OK` 以成功代码的形式返回。

 `rgpspec`

中要读取的属性的数组。 可以通过属性 ID 或可选的字符串名称指定属性。 不需要在数组中按任何特定顺序指定属性。 数组可以包含重复的属性，导致简单属性返回时出现重复的属性值。 非简单属性应返回拒绝访问，尝试再次打开它们。 数组可以包含属性 Id 和字符串 Id 的混合。 此数组必须具有至少 `cpspec` 个属性值。

 `rgvar`

[in，out] `PROPVARIANT` 要用每个属性的值填充 (在 VisualStudio 命名空间) 中的结构数组。 数组的大小必须至少为个 `cpspec` 元素。 调用方不需要初始化数组中的值。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 `S_FALSE`如果未找到一个或多个属性，则返回。 否则，返回错误代码。

## <a name="remarks"></a>备注
 如果找不到属性，则数组中的相应条目 `rgvar` 包含类型为 `VARIANT` 的 `VT_EMPTY` 。

## <a name="see-also"></a>另请参阅
- [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)

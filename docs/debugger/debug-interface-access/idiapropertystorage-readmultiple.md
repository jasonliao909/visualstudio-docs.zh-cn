---
description: 从当前属性集中读取指定的属性。
title: IDiaPropertyStorage::ReadMultiple | Microsoft Docs
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

[in] `rgpspec` 数组中指定属性的计数。 如果为零，则该方法不返回任何属性，但会返回 `S_OK` 作为成功代码。

 `rgpspec`

[in] 要读取的属性的数组。 可以通过属性 ID 或可选的字符串名称指定属性。 不需要在数组中按任何特定顺序指定属性。 数组可以包含重复的属性，导致简单属性返回时出现重复的属性值。 非简单属性在尝试再次打开它们时应返回拒绝访问。 数组可以包含属性 ID 和字符串 ID 的组合。 此数组必须具有至少 `cpspec` 个属性值。

 `rgvar`

[in, out] 要填充每个属性的值的 `PROPVARIANT` 结构数组（在 Microsoft.VisualStudio.OLE.Interop 命名空间中）。 该数组的大小必须至少为个 `cpspec` 元素。 调用方不需要初始化数组中的值。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果未找到一个或多个属性，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="remarks"></a>备注
 如果未找到属性，则 `rgvar` 数组中的相应条目包含类型为 `VT_EMPTY` 的 `VARIANT`。

## <a name="see-also"></a>另请参阅
- [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)

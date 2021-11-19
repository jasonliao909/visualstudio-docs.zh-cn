---
description: 描述地址映射中的条目。
title: DiaAddressMapEntry | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- DiaAddressMapEntry enumeration
ms.assetid: 5d0ae226-981d-4541-a801-fc4993fe663b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 4c5ac207ec1fc66554264d14f2aa9f0dccbb3773
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832379"
---
# <a name="diaaddressmapentry"></a>DiaAddressMapEntry
描述地址映射中的条目。

## <a name="syntax"></a>语法

```C++
struct DiaAddressMapEntry {
    DWORD rva,
    DWORD rvaTo
};
```

## <a name="elements"></a>元素
`rva` 映像 A 中 (RVA) 的相对虚拟地址。

`rvaTo` 相对虚拟地址 `rva` 将映射到映像 B 中的。

## <a name="remarks"></a>备注
地址映射提供从一个图像布局到另一个 (B)  () 的转换。 `DiaAddressMapEntry`按定义地址映射的结构的数组 `rva` 。

若要将地址（ `addrA` 如中的图像 A）转换为地址， `addrB` 请在图像 B 中执行以下步骤：

1. 在地图中搜索 `e` `rva` 小于或等于的条目 `addrA` 。

2. 设置 `delta = addrA - e.rva`。

3. 设置 `addrB = e.rvaTo + delta`。

    结构的数组 `DiaAddressMapEntry` 将传递给 [IDiaAddressMap：： set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md) 方法。

## <a name="requirements"></a>要求
标头： dia2

## <a name="see-also"></a>另请参阅
- [枚举和结构](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaAddressMap::set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md)

---
description: 提供用于支持图像布局转换的地址映射。
title: IDiaAddressMap::set_addressMap | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap::set_addressMap method
ms.assetid: 81e82073-089b-43d5-af39-49d7a4907c7a
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: dd73b8bad816556ac598bc4c2c115e29f660e0fa
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832342"
---
# <a name="idiaaddressmapset_addressmap"></a>IDiaAddressMap::set_addressMap
提供用于支持图像布局转换的地址映射。

## <a name="syntax"></a>语法

```C++
HRESULT set_addressMap ( 
   DWORD                     cbData,
   struct DiaAddressMapEntry data[],
   BOOL                      imagetoSymbols
);
```

#### <a name="parameters"></a>参数
 `cbData`

[in] `data` 参数中的元素数。

 `data[]`

[in] [DiaAddressMapEntry Structure](../../debugger/debug-interface-access/diaaddressmapentry.md) 结构的数组，这些结构定义转换映射。

 `imagetoSymbols`

[in] 如果 `data` 参数定义从新图像布局到原始布局的映射（如调试符号所述），则为 `TRUE`。 如果 `data` 是从原始布局到新图像布局的映射，则为 `FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。

## <a name="remarks"></a>备注
 通常，DIA 从程序数据库 (.pdb) 文件中检索地址转换映射。 如果缺少这些值，则会调用 [IDiaAddressMap::set_imageHeaders](../../debugger/debug-interface-access/idiaaddressmap-set-imageheaders.md) 方法两次，一次将 `imagetoSymbols` 参数设置为 `TRUE`，另一次将 `imagetoSymbols` 参数设置为 `FALSE`。 除非同时提供两个转换映射，否则无法使用 [IDiaAddressMap::put_addressMapEnabled](../../debugger/debug-interface-access/idiaaddressmap-put-addressmapenabled.md) 方法启用地址映射转换。

## <a name="see-also"></a>另请参阅
- [DiaAddressMapEntry 结构](../../debugger/debug-interface-access/diaaddressmapentry.md)
- [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)
- [IDiaAddressMap::put_addressMapEnabled](../../debugger/debug-interface-access/idiaaddressmap-put-addressmapenabled.md)
- [IDiaAddressMap::set_imageHeaders](../../debugger/debug-interface-access/idiaaddressmap-set-imageheaders.md)

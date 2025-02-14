---
description: 设置映像标头以启用相对虚拟地址转换。
title: IDiaAddressMap::set_imageHeaders | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap::set_imageHeaders method
ms.assetid: a46b9d0e-43e6-433f-b2c7-aa203981e4e4
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 3acedb7cf87d9dac560f552a305fc736f7b570fe
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832341"
---
# <a name="idiaaddressmapset_imageheaders"></a>IDiaAddressMap::set_imageHeaders
设置映像标头以启用相对虚拟地址转换。

## <a name="syntax"></a>语法

```C++
HRESULT set_imageHeaders ( 
   DWORD cbData,
   BYTE  data[],
   BOOL  originalHeaders
);
```

#### <a name="parameters"></a>参数
 cbData

[in] 标头数据的字节数。 必须是 `n*sizeof(IMAGE_SECTION_HEADER)`，其中 `n` 是可执行文件中节标头的数量。

 data[]

[in] 要用作映像标头的 `IMAGE_SECTION_HEADER` 结构数组。

 originalHeaders

[in] 如果映像标头来自新映像，则设置为 `FALSE`；如果它们反映升级前的原始映像，则设置为 `TRUE`。 通常，这只会在与对 [IDiaAddressMap::set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md) 方法的调用结合使用时设置为 `TRUE`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。

## <a name="remarks"></a>备注
 `IMAGE_SECTION_HEADER` 结构在 Winnt.h 中声明，表示可执行文件的映像节标头格式。

 相对虚拟地址计算取决于 `IMAGE_SECTION_HEADER` 值。 通常，DIA 从程序数据库 (.pdb) 文件中检索这些值。 如果缺少这些值，DIA 将无法计算相对虚拟地址，[IDiaAddressMap::get_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-get-relativevirtualaddressenabled.md) 方法将返回 `FALSE`。 然后，客户端必须调用 [IDiaAddressMap::put_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-put-relativevirtualaddressenabled.md) 方法，以在提供映像本身丢失的映像标头后启用相对虚拟地址计算。

## <a name="see-also"></a>另请参阅
- [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)
- [IDiaAddressMap::set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md)
- [IDiaAddressMap::get_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-get-relativevirtualaddressenabled.md)
- [IDiaAddressMap::put_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-put-relativevirtualaddressenabled.md)

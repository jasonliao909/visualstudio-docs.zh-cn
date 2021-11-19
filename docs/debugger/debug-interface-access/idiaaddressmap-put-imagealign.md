---
description: 设置图像对齐方式。
title: IDiaAddressMap::put_imageAlign | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap::put_imageAlign method
ms.assetid: f9ce875d-c263-43e5-a534-f34c37f9866f
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: c0817d0b1569557bad7ebc966c1dd23339a134ce
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832347"
---
# <a name="idiaaddressmapput_imagealign"></a>IDiaAddressMap::put_imageAlign
设置图像对齐方式。

## <a name="syntax"></a>语法

```C++
HRESULT put_imageAlign ( 
   DWORD NewVal
);
```

#### <a name="parameters"></a>参数
 NewVal

[in] 可执行文件的新图像对齐值。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。

## <a name="remarks"></a>备注
 图像（加载的可执行文件）与指定的内存边界对齐。 此对齐方式可能会受当前系统体系结构以及编译和链接时间选项的影响。 图像对齐始终位于字节边界上。 以下图像对齐值有效：1、2、4、8、16、32 和 64 字节边界。

 可以通过调用 [IDiaAddressMap::get_imageAlign](../../debugger/debug-interface-access/idiaaddressmap-get-imagealign.md) 方法来检索当前的图像对齐方式。

> [!NOTE]
> 等到可以调用此方法时，图像已经加载。 当图像已移动或已更改并且需要新的对齐方式时，通常使用 `put_imageAlign` 方法。

## <a name="see-also"></a>另请参阅
- [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)
- [IDiaAddressMap::get_imageAlign](../../debugger/debug-interface-access/idiaaddressmap-get-imagealign.md)

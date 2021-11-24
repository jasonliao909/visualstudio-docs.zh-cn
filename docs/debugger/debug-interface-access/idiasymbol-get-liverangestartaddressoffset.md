---
description: 返回本地符号有效的范围的起始地址的偏移部分。
title: IDiaSymbol::get_liveRangeStartAddressOffset | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_liveRangeStartAddressOffset
ms.assetid: f5b28914-0a14-4b22-8259-59d7f97ee610
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 7bf2779897b339ca4ff77cb23656fdf0e2340f10
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832548"
---
# <a name="idiasymbolget_liverangestartaddressoffset"></a>IDiaSymbol::get_liveRangeStartAddressOffset
返回本地符号有效的范围的起始地址的偏移部分。

## <a name="syntax"></a>语法

```C++
HRESULT get_liveRangeStartAddressOffset ( 
   DWORD* offset
);
```

#### <a name="parameters"></a>参数
 `offset`

[out] 返回起始地址范围的偏移部分。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。

> [!NOTE]
> 返回的错误代码表示符号没有实时范围信息。

## <a name="remarks"></a>备注
 由节和偏移组成的地址是符号有效的范围的开始位置。

 若要获取地址的节部分，请使用 [IDiaSymbol::get_liveRangeStartAddressSection](../../debugger/debug-interface-access/idiasymbol-get-liverangestartaddresssection.md)。

## <a name="requirements"></a>要求
 标头：Dia2.h

 库：diaguids.lib

 DLL：msdia100.dll

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)

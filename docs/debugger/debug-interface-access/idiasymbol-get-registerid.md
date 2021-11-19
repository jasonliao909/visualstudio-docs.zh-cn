---
description: 当 LocationType 枚举值设置为"LocIsEnregistered"时) 位置的寄存器指示符。
title: IDiaSymbol::get_registerId | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_registerId method
ms.assetid: f881e793-eb9e-48dc-a847-dd61d77174fc
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 715fc20baafeaf6ed7adb8790b84daedfc9d3b19
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832726"
---
# <a name="idiasymbolget_registerid"></a>IDiaSymbol::get_registerId
当 [LocationType](../../debugger/debug-interface-access/locationtype.md) 枚举设置为 时，检索位置的寄存器指示符 `LocIsEnregistered` 。

## <a name="syntax"></a>语法

```C++
HRESULT get_registerId ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回位置的寄存器表示符。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 表示 属性不可用于 符号。

## <a name="remarks"></a>备注
 如果符号相对于寄存器，即，如果符号 [的 LocationType](../../debugger/debug-interface-access/locationtype.md) 枚举设置为 ，则使用 方法，然后调用 `LocIsRegRel` `get_registerId` [IDiaSymbol：：get_offset](../../debugger/debug-interface-access/idiasymbol-get-offset.md) 方法，从符号所在的寄存器获取偏移量。

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)

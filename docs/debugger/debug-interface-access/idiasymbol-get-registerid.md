---
description: 当 LocationType Enumeration) 设置为 LocIsEnregistered` 时，检索位置的寄存器指示符。
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
当 [LocationType Enumeration](../../debugger/debug-interface-access/locationtype.md) 设置为 `LocIsEnregistered` 时，检索位置的寄存器指示符。

## <a name="syntax"></a>语法

```C++
HRESULT get_registerId ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 返回位置的寄存器指示符。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。

## <a name="remarks"></a>备注
 如果符号是相对于寄存器的，即如果符号的 [LocationType Enumeration](../../debugger/debug-interface-access/locationtype.md) 设置为 `LocIsRegRel`，则使用 `get_registerId` 方法，然后调用 [IDiaSymbol::get_offset](../../debugger/debug-interface-access/idiasymbol-get-offset.md) 方法从符号所在的寄存器中获得偏移。

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)

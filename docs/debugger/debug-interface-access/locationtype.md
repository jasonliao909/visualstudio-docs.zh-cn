---
description: 指示符号中包含的位置信息类型。
title: LocationType | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- LocationType enumeration
ms.assetid: d3e1eedc-bfd3-4c91-881b-d69565138d0f
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: d68e541060c07a523af001558f2804eed35d498d
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832812"
---
# <a name="locationtype"></a>LocationType
指示符号中包含的位置信息类型。

## <a name="syntax"></a>语法

```C++
enum LocationType {
    LocIsNull,
    LocIsStatic,
    LocIsTLS,
    LocIsRegRel,
    LocIsThisRel,
    LocIsEnregistered,
    LocIsBitField,
    LocIsSlot,
    LocIsIlRel,
    LocInMetaData,
    LocIsConstant,
    LocTypeMax
};
```

## <a name="elements"></a>元素
`LocIsNull` 位置信息不可用。

`LocIsStatic` 位置是静态的。

`LocIsTLS` 位置位于线程本地存储中。

`LocIsRegRel` 位置与寄存器相关。

`LocIsThisRel` 位置与 `this` 相关。

`LocIsEnregistered` 位置位于寄存器中。

`LocIsBitField` 位置位于位域中。

`LocIsSlot` 位置为 Microsoft 中间语言 (MSIL) 插槽。

`LocIsIlRel` 位置与 MSIL 相关。

`LocInMetaData` 位置位于元数据中。

`LocIsConstant` 位置位于常数值中。

`LocTypeMax` 此枚举中的位置类型的数量。

## <a name="remarks"></a>备注
[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) 接口可用的属性取决于符号在图像文件中的位置。 有关详细信息，请参阅[符号位置](../../debugger/debug-interface-access/symbol-locations.md)。

此枚举中的值是通过调用 [IDiaSymbol::get_locationType](../../debugger/debug-interface-access/idiasymbol-get-locationtype.md) 方法返回的。

## <a name="requirements"></a>要求
标头：cvconst.h

## <a name="see-also"></a>另请参阅
- [枚举和结构](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [IDiaSymbol::get_locationType](../../debugger/debug-interface-access/idiasymbol-get-locationtype.md)
- [符号位置](../../debugger/debug-interface-access/symbol-locations.md)

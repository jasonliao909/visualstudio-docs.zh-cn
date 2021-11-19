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

`LocIsRegRel` 位置是寄存器相对位置。

`LocIsThisRel` 位置为 `this` -relative。

`LocIsEnregistered` 位置在寄存器中。

`LocIsBitField` 位置位于位字段中。

`LocIsSlot` Location 是 Microsoft 中间语言 (MSIL) 槽。

`LocIsIlRel` 位置是 MSIL 相对位置。

`LocInMetaData` 位置位于元数据中。

`LocIsConstant` 位置位于常量值中。

`LocTypeMax` 此枚举中的位置类型数。

## <a name="remarks"></a>备注
[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)接口可用的属性取决于符号在图像文件中的位置。 有关详细信息，请参阅 [符号位置](../../debugger/debug-interface-access/symbol-locations.md)。

此枚举中的值通过调用 [IDiaSymbol：：get_locationType](../../debugger/debug-interface-access/idiasymbol-get-locationtype.md) 方法返回。

## <a name="requirements"></a>要求
标头：cvconst.h

## <a name="see-also"></a>另请参阅
- [枚举和结构](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [IDiaSymbol::get_locationType](../../debugger/debug-interface-access/idiasymbol-get-locationtype.md)
- [符号位置](../../debugger/debug-interface-access/symbol-locations.md)

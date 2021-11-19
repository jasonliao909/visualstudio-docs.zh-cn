---
title: BasicType | Microsoft Docs
description: 查找有关 BasicType 枚举的参考信息，该枚举在调试接口访问 SDK Visual Studio符号的基本类型。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- BasicType enumeration
ms.assetid: 19ae53ba-cd6e-47b6-9f94-27ae663ce955
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 9c59e66b73767b5ee5c6787fe0155ad1a2345161
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832418"
---
# <a name="basictype"></a>BasicType
指定符号的基本类型。

## <a name="syntax"></a>语法

```C++
enum BasicType {
    btNoType   = 0,
    btVoid     = 1,
    btChar     = 2,
    btWChar    = 3,
    btInt      = 6,
    btUInt     = 7,
    btFloat    = 8,
    btBCD      = 9,
    btBool     = 10,
    btLong     = 13,
    btULong    = 14,
    btCurrency = 25,
    btDate     = 26,
    btVariant  = 27,
    btComplex  = 28,
    btBit      = 29,
    btBSTR     = 30,
    btHresult  = 31,
    btChar16   = 32,  // char16_t
    btChar32   = 33,  // char32_t
};
```

## <a name="elements"></a>元素
btNoType 未指定基本类型。

btVoid 基本类型为 `void` 。

btChar Basic 类型 (`char` C/C++ 类型) 。

btWChar Basic 类型是一种宽 (Unicode) 字符 `WCHAR` () 。

btInt Basic 类型 `signed int` (C/C++ 类型) 。

btUInt Basic 类型 `unsigned int` (C/C++ 类型) 。

btFloat Basic 类型是浮点数 `FLOAT` () 。

btBCD 基本类型是二进制编码的十进制 `BCD` () 。

btBool Basic 类型是布尔值 `BOOL` () 。

btLong Basic 类型 (`long int` C/C++ 类型) 。

btULong Basic 类型是 (`unsigned long int` C/C++ 类型的) 。

btCurrency 基本类型为 currency。

btDate 基本类型是日期/时间 `DATE` () 。

btVariant 基本类型是一种变量类型结构 `VARIANT` () 。

btComplex 基本类型是一个复数。

btBit Basic 类型为位。

btBSTR 基本类型是基本字符串或二进制字符串 `BSTR` () 。

btHresult 基本类型是 `HRESULT` 。

## <a name="remarks"></a>备注
此枚举中的值由 [IDiaSymbol：：get_baseType](../../debugger/debug-interface-access/idiasymbol-get-basetype.md) 方法返回。

## <a name="requirements"></a>要求
标头：cvconst.h

## <a name="see-also"></a>另请参阅
- [枚举和结构](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaSymbol::get_baseType](../../debugger/debug-interface-access/idiasymbol-get-basetype.md)
- [IDiaSymbol::get_length](../../debugger/debug-interface-access/idiasymbol-get-length.md)

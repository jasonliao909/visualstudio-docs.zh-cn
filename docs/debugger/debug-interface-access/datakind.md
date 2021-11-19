---
description: 指示数据值的特定范围。
title: DataKind | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- DataKind enumeration
ms.assetid: b64be708-22d6-4360-99e7-8f4e6b196de7
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: fbf8d7f40f1cd3c14bd6b830a65526921f1c6ece
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832385"
---
# <a name="datakind"></a>DataKind
指示数据值的特定范围。

## <a name="syntax"></a>语法

```C++
enum DataKind {
    DataIsUnknown,
    DataIsLocal,
    DataIsStaticLocal,
    DataIsParam,
    DataIsObjectPtr,
    DataIsFileStatic,
    DataIsGlobal,
    DataIsMember,
    DataIsStaticMember,
    DataIsConstant
};
```

## <a name="elements"></a>元素
无法确定 DataIsUnknown 数据符号。

DataIsLocal 数据项是局部变量。

DataIsStaticLocal 数据项是静态局部变量。

DataIsParam 数据项是一个形参。

DataIsObjectPtr 数据项是一个对象指针 `this` () 。

DataIsFileStatic 数据项是文件范围的变量。

DataIsGlobal 数据项是全局变量。

DataIsMember 数据项是对象成员变量。

DataIsStaticMember 数据项是类静态变量。

DataIsConstant 数据项是一个常量值。

## <a name="remarks"></a>备注
此枚举中的值由 [IDiaSymbol：：get_dataKind](../../debugger/debug-interface-access/idiasymbol-get-datakind.md) 方法返回。

## <a name="requirements"></a>要求
标头：cvconst.h

## <a name="see-also"></a>另请参阅
- [枚举和结构](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaSymbol::get_dataKind](../../debugger/debug-interface-access/idiasymbol-get-datakind.md)

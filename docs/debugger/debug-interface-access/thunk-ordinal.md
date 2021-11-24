---
description: 指定 thunk 类型。
title: THUNK_ORDINAL | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- Thunk_Ordinal enumeration
ms.assetid: 026f98a9-36b8-41ef-8a72-12d7cbc2d362
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 30a8f8d43056011bc28113bde1ce837da0205bc2
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832470"
---
# <a name="thunk_ordinal"></a>THUNK_ORDINAL
指定 thunk 类型。

## <a name="syntax"></a>语法

```C++
typedef enum THUNK_ORDINAL {
    THUNK_ORDINAL_NOTYPE,
    THUNK_ORDINAL_ADJUSTOR,
    THUNK_ORDINAL_VCALL,
    THUNK_ORDINAL_PCODE,
    THUNK_ORDINAL_LOAD

    // trampoline thunk ordinals - only for use in Trampoline thunk symbols
    THUNK_ORDINAL_TRAMP_INCREMENTAL,
    THUNK_ORDINAL_TRAMP_BRANCHISLAND,
} THUNK_ORDINAL;
```

## <a name="elements"></a>元素
THUNK_ORDINAL_NOTYPE 标准 thunk。

THUNK_ORDINAL_ADJUSTOR `this` 调整器 thunk。

THUNK_ORDINAL_VCALL 虚拟调用 thunk。

THUNK_ORDINAL_PCODE P 代码 thunk。

THUNK_ORDINAL_LOAD 延迟加载 thunk。

THUNK_ORDINAL_TRAMP_INCREMENTAL 增量 trampoline thunk（trampoline thunk 用于将调用从一个内存空间弹跳到另一个内存空间）。

THUNK_ORDINAL_TRAMP_BRANCHISLAND 分支点 trampoline thunk。

## <a name="remarks"></a>备注
此枚举中的值是通过调用 [IDiaSymbol::get_thunkOrdinal](../../debugger/debug-interface-access/idiasymbol-get-thunkordinal.md) 方法返回的。

## <a name="requirements"></a>要求
标头：cvconst.h

## <a name="see-also"></a>另请参阅
- [枚举和结构](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaSymbol::get_thunkOrdinal](../../debugger/debug-interface-access/idiasymbol-get-thunkordinal.md)

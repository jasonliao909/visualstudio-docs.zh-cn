---
description: 检索一个标志，该标志指定数据符号是否已拆分为聚合或其他符号的集合;编译器将符号视为单独的实体，即使它们确实是较大符号的一部分。
title: IDiaSymbol：：get_isSplitted |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_isSplitted method
ms.assetid: ff160cf6-003b-4ef5-a406-20a7b287b2bf
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: c025460f04cbd2d9eb5546f434ff990584fa7e26
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832558"
---
# <a name="idiasymbolget_issplitted"></a>IDiaSymbol::get_isSplitted
检索一个标志，该标志指定数据符号是否已拆分为聚合或其他符号的集合;编译器将符号视为单独的实体，即使它们确实是较大符号的一部分。

## <a name="syntax"></a>语法

```C++
HRESULT get_isSplitted(
   BOOL *pFlag
);
```

#### <a name="parameters"></a>参数
 `pFlag`

[out]如果 `TRUE` 符号已拆分为符号的聚合，则返回 ;否则返回 `FALSE` 。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则 `S_FALSE` 返回 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 表示属性不可用于符号。

## <a name="remarks"></a>备注
 [IDiaSymbol：：get_isAggregated](../../debugger/debug-interface-access/idiasymbol-get-isaggregated.md)方法返回属于拆分符号一 `TRUE` 部分的所有符号。

## <a name="requirements"></a>要求

|要求|说明|
|-----------------|-----------------|
|标头：|dia2.h|
|版本：|DIA SDK v8.0|

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [IDiaSymbol::get_isAggregated](../../debugger/debug-interface-access/idiasymbol-get-isaggregated.md)

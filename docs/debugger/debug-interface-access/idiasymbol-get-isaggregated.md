---
description: 检索一个标志，该标志指定该数据符号是否为聚合或符号集合的一部分;编译器会将聚合符号视为单独的实体，但它们实际上是一个大符号的组成部分。
title: IDiaSymbol：： get_isAggregated |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_isAggregated method
ms.assetid: 24d280ef-6ea3-4958-9418-4ad3ca7c67c1
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 8ebf6035fcec95fff5849d7aa472ed97f9d9cc0b
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832733"
---
# <a name="idiasymbolget_isaggregated"></a>IDiaSymbol::get_isAggregated
检索一个标志，该标志指定该数据符号是否为聚合或符号集合的一部分;编译器会将聚合符号视为单独的实体，但它们实际上是一个大符号的组成部分。

## <a name="syntax"></a>语法

```C++
HRESULT get_isAggregated(
   BOOL *pFlag
);
```

#### <a name="parameters"></a>参数
 `pFlag`

弄 `TRUE` 如果数据是从父符号拆分的符号聚合的一部分，则返回; 否则返回 `FALSE` 。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回 `S_FALSE` 错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。

## <a name="remarks"></a>备注
 [IDiaSymbol：： get_isSplitted](../../debugger/debug-interface-access/idiasymbol-get-issplitted.md)方法用于作为 `TRUE` 聚合符号的父符号的符号。

## <a name="requirements"></a>要求

|要求|说明|
|-----------------|-----------------|
|标头：|dia2|
|版本：|DIA SDK v8.0|

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [IDiaSymbol::get_isSplitted](../../debugger/debug-interface-access/idiasymbol-get-issplitted.md)

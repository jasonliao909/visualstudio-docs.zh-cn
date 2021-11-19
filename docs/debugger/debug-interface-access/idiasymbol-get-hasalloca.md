---
description: 检索一个标志，该标志指定该函数是否包含对 alloca (的调用，该调用用于在堆栈) 上分配内存。
title: IDiaSymbol::get_hasAlloca | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_hasAlloca method
ms.assetid: 3b9fb747-670b-4da7-bb70-612f7b911786
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 91a87bc8bbe7375fbafdd1c42371a267c435835c
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832669"
---
# <a name="idiasymbolget_hasalloca"></a>IDiaSymbol::get_hasAlloca
检索一个标志，该标志指定该函数是否包含对 `alloca` (的调用，该调用用于在堆栈) 上分配内存。

## <a name="syntax"></a>语法

```cpp
HRESULT get_hasAlloca(   BOOL *pFlag);
```

#### <a name="parameters"></a>参数
 `pFlag`

弄 `TRUE` 如果函数包含对的调用，则返回 `alloca` ; 否则返回 `FALSE` 。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回 `S_FALSE` 错误代码。

> [!NOTE]
> 返回值意味着该 `S_FALSE` 属性对符号不可用。

## <a name="requirements"></a>要求

|要求|说明|
|-----------------|-----------------|
|标头：|dia2|
|版本：|DIA SDK v8.0|

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)

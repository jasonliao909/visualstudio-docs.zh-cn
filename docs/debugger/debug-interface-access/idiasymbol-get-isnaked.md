---
description: 检索一个标记，该标记指定函数是否具有 naked 属性（即该函数没有由编译器添加的 prolog 或 epilog 代码）。
title: IDiaSymbol::get_isNaked | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_isNaked method
ms.assetid: b16629dc-8e17-476b-9c7b-58e7277c61ed
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 68b4cf880b2b296751ec0a364d88207c35754c4a
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832483"
---
# <a name="idiasymbolget_isnaked"></a>IDiaSymbol::get_isNaked
检索一个标记，该标记指定函数是否具有 [naked](/cpp/cpp/naked-cpp) 属性（即该函数没有由编译器添加的 prolog 或 epilog 代码）。

## <a name="syntax"></a>语法

```C++
HRESULT get_isNaked(
   BOOL *pFlag
);
```

#### <a name="parameters"></a>参数
 `pFlag`

[out] 如果函数具有 `naked` 属性，则返回 `TRUE`；否则，返回 `FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。

## <a name="requirements"></a>要求

|要求|说明|
|-----------------|-----------------|
|标头：|dia2.h|
|版本：|DIA SDK v8.0|

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [Naked 函数调用](/cpp/cpp/naked-function-calls)

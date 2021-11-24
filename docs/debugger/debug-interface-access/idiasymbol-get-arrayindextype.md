---
description: 检索符号的数组索引类型的符号接口。
title: IDiaSymbol::get_arrayIndexType | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_arrayIndexType method
ms.assetid: cd63b9ec-9694-406c-b37f-bde6bd5fcbf2
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 917117d10744f674d9c80fac3970d6b030695a9f
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832532"
---
# <a name="idiasymbolget_arrayindextype"></a>IDiaSymbol::get_arrayIndexType
检索符号的数组索引类型的符号接口。

## <a name="syntax"></a>语法

```C++
HRESULT get_arrayIndexType ( 
   IDiaSymbol** pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 返回表示符号的数组索引类型的 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) 对象。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。

## <a name="remarks"></a>备注
 某些语言可以指定用作数组索引的类型。 从此方法返回的符号指定了该类型。

## <a name="requirements"></a>要求

|要求|说明|
|-----------------|-----------------|
|标头：|dia2.h|
|版本：|DIA SDK v7.0|

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)

---
description: 检索指定用户定义的数据类型是否已定义任何强制转换运算符的标志。
title: IDiaSymbol::get_hasCastOperator | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_hasCastOperator method
ms.assetid: a21114a6-56a3-4e8a-a65f-58ec2a0a8908
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 89ca0e736cddf33f72fcc08ea23bcafcbdd6fd0f
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832622"
---
# <a name="idiasymbolget_hascastoperator"></a>IDiaSymbol::get_hasCastOperator
检索指定用户定义的数据类型是否已定义任何强制转换运算符的标志。

## <a name="syntax"></a>语法

```C++
HRESULT get_hasCastOperator ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 如果用户定义的数据类型已定义任何强制转换运算符，则返回 `TRUE`；否则，返回 `FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。

## <a name="requirements"></a>要求

|要求|说明|
|-----------------|-----------------|
|标头：|dia2.h|
|版本：|DIA SDK v7.0|

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)

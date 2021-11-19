---
description: 检索 FORTRAN 多维数组的级别（维数）。
title: IDiaSymbol::get_rank | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_rank method
ms.assetid: 14cc9c4b-a5ec-414a-b01f-4a142c17b7cc
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 03c61eea4e46f1e9223ee296f8728e8f4284bf31
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832729"
---
# <a name="idiasymbolget_rank"></a>IDiaSymbol::get_rank
检索 FORTRAN 多维数组的级别（维数）。

## <a name="syntax"></a>语法

```C++
HRESULT get_rank ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 返回 FORTRAN 多维数组中的维数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。

## <a name="remarks"></a>备注
 “级别”是指数组中的维数，其中数组声明为 `myarray[1,2,3]`。 此示例的级别为 3，维数为 3。 级别不适用于 C++，因为 C++ 使用每个维度的数组的概念（即 `myarray[1][2][3]`）。

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)

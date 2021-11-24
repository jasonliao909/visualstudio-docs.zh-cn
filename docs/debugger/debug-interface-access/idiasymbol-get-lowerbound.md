---
description: 检索 FORTRAN 数组维度的下限。
title: IDiaSymbol::get_lowerBound | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_lowerBound method
ms.assetid: e9a6440b-d068-4de4-a240-6723d20812b9
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 070475ac67cf38ecc862ce6f96e77d5d47c16422
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831791"
---
# <a name="idiasymbolget_lowerbound"></a>IDiaSymbol::get_lowerBound
检索 FORTRAN 数组维度的下限。

## <a name="syntax"></a>语法

```C++
HRESULT get_lowerBound ( 
   IDiaSymbol** pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 返回一个 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) 对象，该对象表示 FORTRAN 数组维度的下限。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)

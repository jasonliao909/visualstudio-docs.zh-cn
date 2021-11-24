---
description: 检索指定用户定义的数据类型是否具有重载运算符的标志。
title: IDiaSymbol::get_overloadedOperator | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_overloadedOperator method
ms.assetid: 257a9894-e980-47ae-bdc0-c5e2293ea734
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: a2d35bb29e91cbd1a87081c5fe7e6fc7c3606407
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832510"
---
# <a name="idiasymbolget_overloadedoperator"></a>IDiaSymbol::get_overloadedOperator
检索指定用户定义数据类型是否具有重载运算符的标志。

## <a name="syntax"></a>语法

```C++
HRESULT get_overloadedOperator ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 如果用户定义数据类型具有重载运算符，则返回 `TRUE`；否则返回 `FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)

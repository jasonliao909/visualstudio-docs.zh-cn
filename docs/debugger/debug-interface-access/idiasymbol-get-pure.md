---
description: 检索一个标志，该标志指定该函数是否为纯虚拟函数。
title: IDiaSymbol::get_pure | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_pure method
ms.assetid: b61107e9-9144-4981-b7ef-58a339b80c58
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: e72d37c25ce1df188978eeb8a755e8cdc83cad9a
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832439"
---
# <a name="idiasymbolget_pure"></a>IDiaSymbol::get_pure
检索一个标志，该标志指定该函数是否为纯虚拟函数。

## <a name="syntax"></a>语法

```C++
HRESULT get_pure ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 如果该函数为纯虚拟函数，则返回 `TRUE`；否则，返回 `FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)

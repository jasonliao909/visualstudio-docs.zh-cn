---
description: 检索一个标记，该标记指定是否永远不会覆盖函数或标签。
title: IDiaSymbol::get_notReached | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_notReached method
ms.assetid: e44ba922-6cda-40c2-9b62-44e5a8628e63
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 26f695b7ab4d74bd78a3830810ac93265db83e02
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832791"
---
# <a name="idiasymbolget_notreached"></a>IDiaSymbol::get_notReached
检索一个标记，该标记指定是否永远不会覆盖函数或标签。

## <a name="syntax"></a>语法

```C++
HRESULT get_notReached(
   BOOL *pFlag
);
```

#### <a name="parameters"></a>参数
 pFlag

[out] 如果从未覆盖函数或标签，则返回 `TRUE`；否则，返回 `FALSE`。

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

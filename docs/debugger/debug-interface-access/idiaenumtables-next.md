---
description: 检索枚举序列中指定数目的表。
title: IDiaEnumTables::Next | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumTables::Next method
ms.assetid: 8d7bd359-d33e-4317-9674-d89283efd7de
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 77a8f8a6e933d8655085d5c9e4537391ecf6c7e9
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832145"
---
# <a name="idiaenumtablesnext"></a>IDiaEnumTables::Next
检索枚举序列中指定数目的表。

## <a name="syntax"></a>语法

```C++
HRESULT Next ( 
   ULONG       celt,
   IDiaTable** rgelt,
   ULONG*      pceltFetched
);
```

#### <a name="parameters"></a>参数
 `celt`

[in] 要检索的枚举器中的表数。

 `rgelt`

[out] 要用表示所需表的 [IDiaTable](../../debugger/debug-interface-access/idiatable.md) 对象填充的数组。

 `pceltFetched`

[out] 返回提取的枚举器中的表数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果没有更多表，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md)
- [IDiaTable](../../debugger/debug-interface-access/idiatable.md)

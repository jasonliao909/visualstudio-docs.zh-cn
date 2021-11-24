---
description: 跳过枚举序列中指定数量的表。
title: IDiaEnumTables::Skip | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumTables::Skip method
ms.assetid: 5c9db956-0654-4f1a-8775-530aa980d8ec
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: c2a40bf5a68836f4c1baf4c19b9b417e71795e9a
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832141"
---
# <a name="idiaenumtablesskip"></a>IDiaEnumTables::Skip
跳过枚举序列中指定数量的表。

## <a name="syntax"></a>语法

```C++
HRESULT Skip ( 
   ULONG celt
);
```

#### <a name="parameters"></a>参数
 `celt`

[in] 枚举序列中要跳过的表数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；如果没有更多要跳过的表，则返回 `S_FALSE`。

## <a name="see-also"></a>另请参阅
- [IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md)

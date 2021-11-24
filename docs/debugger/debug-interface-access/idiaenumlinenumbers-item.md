---
description: 通过索引检索行号。
title: IDiaEnumLineNumbers::Item | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumLineNumbers::Item method
ms.assetid: 08efbeaf-22f7-49e9-96a8-bb906dfe4fd8
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: e49593578efb94feb9fc5f9da2152b9008a4d8ba
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832246"
---
# <a name="idiaenumlinenumbersitem"></a>IDiaEnumLineNumbers::Item
通过索引检索行号。

## <a name="syntax"></a>语法

```C++
HRESULT Item ( 
   DWORD            index,
   IDiaLineNumber** lineNumber
);
```

#### <a name="parameters"></a>参数
 索引

[in] 要检索的 [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md) 对象的索引。 索引在 0 到 `count`-1 范围内，其中 `count` 由 [IDiaEnumLineNumbers::get_Count](../../debugger/debug-interface-access/idiaenumlinenumbers-get-count.md) 方法返回。

 lineNumber

[out] 返回表示所需行号的 [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md) 对象。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)
- [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)

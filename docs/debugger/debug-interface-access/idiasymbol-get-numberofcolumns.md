---
description: 检索矩阵中的列数。
title: IDiaSymbol::get_numberOfColumns | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: 64834351-e2c9-4f1c-9dc0-2abb5478bc63
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 1f73a66e836af382b3e00292baff03a28cc9ccf1
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832783"
---
# <a name="idiasymbolget_numberofcolumns"></a>IDiaSymbol::get_numberOfColumns
检索矩阵中的列数。

## <a name="syntax"></a>语法

```C++
HRESULT get_numberOfColumns(
   DWORD* pRetVal);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 一个指向 `DWORD` 的指针，保留矩阵中的列数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回 `S_FALSE` 或错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)

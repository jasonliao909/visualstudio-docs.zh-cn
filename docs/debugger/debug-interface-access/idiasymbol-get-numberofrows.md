---
description: 检索矩阵中的行数。
title: IDiaSymbol::get_numberOfRows | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: cf3eb110-d07f-4995-b68b-08290aa67d6f
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: fa69a07bbb6cac59c367db495a530a9b4055eb79
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832778"
---
# <a name="idiasymbolget_numberofrows"></a>IDiaSymbol::get_numberOfRows
检索矩阵中的行数。

## <a name="syntax"></a>语法

```C++
HRESULT get_numberOfRows(
   DWORD* pRetVal);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 一个指向 `DWORD` 的指针，保留矩阵中的行数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回 `S_FALSE` 或错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)

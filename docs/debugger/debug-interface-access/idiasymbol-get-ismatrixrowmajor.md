---
description: 指定矩阵是否是行优先。
title: IDiaSymbol::get_isMatrixRowMajor | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: 36b1e881-ea76-48b0-b67f-e9eb0d19bec7
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 7cd7953e62e52ba1e5deb033f9d18cdda96d2386
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832654"
---
# <a name="idiasymbolget_ismatrixrowmajor"></a>IDiaSymbol::get_isMatrixRowMajor
指定矩阵是否是行优先。

## <a name="syntax"></a>语法

```C++
HRESULT get_isMatrixRowMajor(
   BOOL* pRetVal);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 指向指定矩阵是否是行优先的 `BOOL` 的指针。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则返回 `S_FALSE` 或错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)

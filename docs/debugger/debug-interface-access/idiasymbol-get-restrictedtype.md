---
description: 指定是否将 this 指针标记为受限制。
title: IDiaSymbol::get_restrictedType | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: c48b00a6-26b0-47b0-b824-fe44dedbc756
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 7070a619556871344558950cc48f43cb7b06c738
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832718"
---
# <a name="idiasymbolget_restrictedtype"></a>IDiaSymbol::get_restrictedType
指定是否将 `this` 指针标记为受限制。

## <a name="syntax"></a>语法

```C++
HRESULT get_restrictedType(
   BOOL* pRetVal);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 指向指定 `this` 指针是否标记为受限制的 `BOOL` 的指针。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则返回 `S_FALSE` 或错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)

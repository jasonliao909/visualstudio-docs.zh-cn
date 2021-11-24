---
description: 检索应用于原始类型的修饰符数。
title: IDiaSymbol::get_numberOfModifiers | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: 61ff7431-1994-4f7e-a182-1817f16f60a9
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: a7906879f00fcb53c91d297aa3a3e97e3f74efed
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832781"
---
# <a name="idiasymbolget_numberofmodifiers"></a>IDiaSymbol::get_numberOfModifiers
检索应用于原始类型的修饰符数。

## <a name="syntax"></a>语法

```C++
HRESULT get_numberOfModifiers(
   DWORD* pRetVal);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 指向指定应用于原始类型的修饰符数的 `DWORD` 的指针。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则返回 `S_FALSE` 或错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)

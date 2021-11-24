---
description: 返回调用约定的方法的指示器。
title: IDiaSymbol::get_callingConvention | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_callingConvention method
ms.assetid: 355d3877-b6b6-45fd-a1d8-baed428d8f96
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 2084a2cc135de453fd364b39512ca85455b6f128
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832633"
---
# <a name="idiasymbolget_callingconvention"></a>IDiaSymbol::get_callingConvention
返回调用约定的方法的指示器。

## <a name="syntax"></a>语法

```C++
HRESULT get_callingConvention ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 从指定方法的调用约定的 [CV_call_e 枚举](../../debugger/debug-interface-access/cv-call-e.md)返回一个值。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。

## <a name="requirements"></a>要求

|要求|说明|
|-----------------|-----------------|
|标头：|dia2.h|
|版本：|DIA SDK v7.0|

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [CV_call_e 枚举](../../debugger/debug-interface-access/cv-call-e.md)

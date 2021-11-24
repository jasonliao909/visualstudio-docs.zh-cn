---
description: 检索 FORTRAN 数组维度上限的符号标识符。
title: IDiaSymbol::get_upperBoundId | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_upperBoundId method
ms.assetid: ddfa1617-bd0f-4187-ba77-a225bab93a95
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: c0d5bb2206293a560adb049afff5430a083c9ab2
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832584"
---
# <a name="idiasymbolget_upperboundid"></a>IDiaSymbol::get_upperBoundId
检索 FORTRAN 数组维度上限的符号标识符。

## <a name="syntax"></a>语法

```C++
HRESULT get_upperBoundId ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`
- [out,] 返回表示 FORTRAN 数组维度上限的符号的 ID。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。

## <a name="remarks"></a>备注
 标识符是由 DIA SDK 创建的唯一值，用于将所有符号标记为唯一。

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)

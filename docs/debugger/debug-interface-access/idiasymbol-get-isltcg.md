---
description: 检索一个标志，该标志指定 Compiland) 是否已与链接器开关 /LTCG (Link-time Code Generation)  (/cpp/build/reference/ltcg-link-time-code-generation) 链接，这有助于整个程序优化。
title: IDiaSymbol::get_isLTCG | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_isLTCG method
ms.assetid: 5f7f05b8-6b71-4958-9e1e-e4924ef9c59b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 0c7b73b33739ade2b83b5e9e2ae760845de1d7e6
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832656"
---
# <a name="idiasymbolget_isltcg"></a>IDiaSymbol::get_isLTCG
检索一个标志，该标志指定 [Compiland](../../debugger/debug-interface-access/compiland.md) 是否已与链接器开关 [/LTCG ](/cpp/build/reference/ltcg-link-time-code-generation) (链接时代码生成) 链接，这有助于优化整个程序。 此开关仅适用于托管代码。

## <a name="syntax"></a>语法

```C++
HRESULT get_iSLTCG(
   BOOL *pFlag
);
```

#### <a name="parameters"></a>参数
 pFlag

[out]如果 与 /LTCG 链接器开关链接 `TRUE` `compiland` ，则返回 ;否则返回 `FALSE` 。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 表示 属性不可用于 符号。

## <a name="requirements"></a>要求

|要求|说明|
|-----------------|-----------------|
|标头：|dia2.h|
|版本：|DIA SDK v8.0|

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)

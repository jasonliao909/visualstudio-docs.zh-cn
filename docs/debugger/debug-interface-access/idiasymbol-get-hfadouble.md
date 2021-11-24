---
description: 检索一个标志，该标志指定用户定义类型 (UDT) 是否包含双精度类型的同构浮点聚合 (HFA) 数据。
title: IDiaSymbol::get_hfaDouble | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_hfaDouble method
ms.assetid: efc247b9-c16e-4fa3-89b0-901caf7b74c3
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 1f38d004deab394abff83fd24d8a871c8e40b9f5
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832459"
---
# <a name="idiasymbolget_hfadouble"></a>IDiaSymbol::get_hfaDouble
检索一个标志，该标志指定用户定义类型 (UDT) 是否包含双精度类型的同构浮点聚合 (HFA) 数据。

## <a name="syntax"></a>语法

```C++
HRESULT get_hfaDouble( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 如果 UDT 包含双精度类型的 HFA 数据，则返回 `TRUE`；否则，返回 `FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。

## <a name="remarks"></a>备注

## <a name="requirements"></a>要求
 标头：Dia2.h

 库：diaguids.lib

 DLL：msdia100.dll

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [IDiaSymbol::get_udtKind](../../debugger/debug-interface-access/idiasymbol-get-udtkind.md)

---
description: 检索指定用户定义类型 (UDT) 是否包含双精度类型的同构浮点聚合 (HFA) 数据的标志。
title: IDiaSymbol::get_hfaFloat | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_hfaFloat method
ms.assetid: 73ddcffe-cdac-4b03-be42-82ef985d17ee
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: f2947d49f351b21a2702049fcf97f363a9e3d301
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832496"
---
# <a name="idiasymbolget_hfafloat"></a>IDiaSymbol::get_hfaFloat
检索指定用户定义类型 (UDT) 是否包含浮点类型的同构浮点聚合 (HFA) 数据的标志。

## <a name="syntax"></a>语法

```C++
HRESULT get_hfaFloat( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 如果 UDT 包含浮点类型的 HFA 数据，则返回 `TRUE`；否则返回 `FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则返回 `S_FALSE` 或错误代码。

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

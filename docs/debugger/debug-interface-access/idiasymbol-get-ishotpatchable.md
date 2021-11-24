---
description: 检索指示是否已使用 /hotpatch（创建可热修补的映像）编译器开关编译模块的标志。
title: IDiaSymbol::get_isHotpatchable | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_isHotpatchable method
ms.assetid: b7b6f490-1cf2-4a68-9237-b152dac84d3c
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: cb51ab86da2ecca068eb2c2ff557ef7f1755ec0a
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832664"
---
# <a name="idiasymbolget_ishotpatchable"></a>IDiaSymbol::get_isHotpatchable
检索指示是否已使用 [/hotpatch（创建可热修补的映像）](/cpp/build/reference/hotpatch-create-hotpatchable-image)编译器开关编译模块的标志。

## <a name="syntax"></a>语法

```C++
HRESULT get_isHotpatchable(
   BOOL *pFlag
);
```

#### <a name="parameters"></a>参数
 `pFlag`

[out] 如果模块可进行热修补，则返回 `TRUE`；否则返回 `FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。

## <a name="remarks"></a>备注
 此属性在 `SymTagCompilandDetails` 符号类型中可用（请参阅 [CompilandDetails](../../debugger/debug-interface-access/compilanddetails.md)）。

## <a name="requirements"></a>要求

|要求|说明|
|-----------------|-----------------|
|标头：|dia2.h|
|版本：|DIA SDK v8.0|

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [CompilandDetails](../../debugger/debug-interface-access/compilanddetails.md)

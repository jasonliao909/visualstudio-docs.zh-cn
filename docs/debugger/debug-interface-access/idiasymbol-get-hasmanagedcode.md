---
description: 检索一个标记，该标记指示模块是否包含托管代码。
title: IDiaSymbol::get_hasManagedCode | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_hasManagedCode method
ms.assetid: e40f82f5-88fe-4a9b-b594-3605f42773ec
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- dotnet
ms.openlocfilehash: 0bd8c7dd0154eb25289d3a9e44fe24097d817b24
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831799"
---
# <a name="idiasymbolget_hasmanagedcode"></a>IDiaSymbol::get_hasManagedCode
检索一个标记，该标记指示模块是否包含托管代码。

## <a name="syntax"></a>语法

```C++
HRESULT get_hasManagedCode(
   BOOL *pFlag
);
```

#### <a name="parameters"></a>参数
 `pFlag`

[out] 如果模块包含托管代码，则返回 `TRUE`；否则，返回 `FALSE`，该代码为非托管代码。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回 `S_FALSE` 或错误代码。

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

---
description: 返回用于生成编译单位的编译器的名称。
title: IDiaSymbol::get_compilerName | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_compilerName method
ms.assetid: 66eaaf72-68d4-40ee-b132-97bea9fe395c
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: c388e51ca6ded38d9db6fc64f244568d1660425b
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832589"
---
# <a name="idiasymbolget_compilername"></a>IDiaSymbol::get_compilerName
返回用于生成[编译单位](../../debugger/debug-interface-access/compiland.md)的编译器的名称。

## <a name="syntax"></a>语法

```C++
HRESULT get_compilerName (
   BSTR *pName
);
```

#### <a name="parameters"></a>参数
 指向将包含编译器的 Unicode 名称的 BSTR 的 `pName` 指针。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。

## <a name="remarks"></a>备注

## <a name="requirements"></a>要求

|要求|说明|
|-----------------|-----------------|
|标头：|dia2.h|
|版本：|DIA SDK v8.0|

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)

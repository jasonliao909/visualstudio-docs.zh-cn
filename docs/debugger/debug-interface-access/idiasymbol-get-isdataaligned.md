---
description: 检索一个标记，该标记指定用户定义的类型 (UDT) 是否已与某些特定的内存边界对齐。
title: IDiaSymbol::get_isDataAligned | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_isDataAligned method
ms.assetid: ddd11a41-6c00-4829-acf4-aa1ace8c21a7
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 219c8755348859331fa39fac09d263020775b812
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832666"
---
# <a name="idiasymbolget_isdataaligned"></a>IDiaSymbol::get_isDataAligned
检索一个标记，该标记指定用户定义的类型 (UDT) 是否已与某些特定的内存边界对齐。

## <a name="syntax"></a>语法

```C++
HRESULT get_isDataAligned(
   BOOL *pFlag
);
```

#### <a name="parameters"></a>参数
 `pFlag`

[out] 如果 UDT 已与某些内存边界对齐，则返回 `TRUE`；否则，返回 `FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。

## <a name="remarks"></a>备注
 当可执行文件使用非默认数据对齐编译时，通常会设置此属性。 例如，Microsoft c + + 编译器可以更改使用命令行选项时，数据对齐 /Zp <em>#</em>，其中 *#* 是一个字节值。

## <a name="requirements"></a>要求

|要求|说明|
|-----------------|-----------------|
|标头：|dia2.h|
|版本：|DIA SDK v8.0|

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)

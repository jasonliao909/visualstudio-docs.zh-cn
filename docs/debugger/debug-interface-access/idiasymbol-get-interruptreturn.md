---
description: 检索指定函数是否包含中断指令返回（例如，X86 程序集代码 iret`）的标志。
title: IDiaSymbol::get_interruptReturn | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_interruptReturn method
ms.assetid: 9665da6c-4cc0-41d7-b2e2-0d9e50174cf8
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 5167627f840d7d9121940179088e33e4d0697a36
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832488"
---
# <a name="idiasymbolget_interruptreturn"></a>IDiaSymbol::get_interruptReturn
检索指定函数是否包含中断指令返回（例如，X86 程序集代码 `iret`）的标志。

## <a name="syntax"></a>语法

```C++
HRESULT get_interruptReturn(
   BOOL *pFlag
);
```

#### <a name="parameters"></a>参数
 `pFlag`

[out] 如果函数具有中断指令返回，则返回 `TRUE`；否则返回 `FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。

## <a name="requirements"></a>要求

|要求|说明|
|-----------------|-----------------|
|标头：|dia2.h|
|版本：|DIA SDK v8.0|

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)

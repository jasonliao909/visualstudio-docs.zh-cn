---
description: 检索一个标志，该标志指定函数是否包含 setjmp) 命令 (与 longjmp (/cpp/c-runtime-library/reference/longjmp) 命令配对的 setjmp) 命令，这构成了异常处理的 C 样式方法) 。
title: IDiaSymbol::get_hasSetJump | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_hasSetJump method
ms.assetid: 22656206-dccf-40ed-b179-fc016d1b262a
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 6face230a71d30514f589a77964f14ef4236b90d
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832521"
---
# <a name="idiasymbolget_hassetjump"></a>IDiaSymbol::get_hasSetJump
检索一个标志，该标志指定函数是否包含 [setjmp](/cpp/c-runtime-library/reference/setjmp) 命令 ([与 longjmp](/cpp/c-runtime-library/reference/longjmp) 命令配对，这些标志构成了异常处理方法的 C 样式) 。

## <a name="syntax"></a>语法

```C++
HRESULT get_hasSetJump(
   BOOL *pFlag
);
```

#### <a name="parameters"></a>参数
 `pFlag`

[out]如果 `TRUE` 函数包含命令， `setjmp` 则返回 ;否则返回 `FALSE` 。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则 `S_FALSE` 返回 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 表示属性不可用于符号。

## <a name="requirements"></a>要求

|要求|说明|
|-----------------|-----------------|
|标头：|dia2.h|
|版本：|DIA SDK v8.0|

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [IDiaSymbol::get_hasLongJump](../../debugger/debug-interface-access/idiasymbol-get-haslongjump.md)
- [longjmp](/cpp/c-runtime-library/reference/longjmp)
- [setjmp](/cpp/c-runtime-library/reference/setjmp)

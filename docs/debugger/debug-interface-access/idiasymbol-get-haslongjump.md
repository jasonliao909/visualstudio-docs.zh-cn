---
description: 检索一个标记，该标记指定函数是否包含 longjmp) 命令的使用（与 setjmp(/cpp/c-runtime-library/reference/setjmp) 命令搭配，这些形成了异常处理的 C 样式方法）。
title: IDiaSymbol::get_hasLongJump | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_hasLongJump method
ms.assetid: 14484cb1-43b0-47a1-a9a8-081b55566886
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 8de8dcc40d65425540f701b6b833da234b800bf5
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831800"
---
# <a name="idiasymbolget_haslongjump"></a>IDiaSymbol::get_hasLongJump
检索一个标记，该标记指定函数是否包含 [longjmp](/cpp/c-runtime-library/reference/longjmp) 命令的使用（与 [setjmp](/cpp/c-runtime-library/reference/setjmp) 命令搭配，这些形成了异常处理的 C 样式方法）。

## <a name="syntax"></a>语法

```C++
HRESULT get_hasLongJump
   BOOL *pFlag
);
```

#### <a name="parameters"></a>参数
 `pFlag`

[out] 如果该函数包含 `longjmp` 命令，则返回 `TRUE`；否则，返回 `FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。

## <a name="requirements"></a>要求

|要求|说明|
|-----------------|-----------------|
|标头：|dia2.h|
|版本：|DIA SDK v8.0|

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [IDiaSymbol::get_hasSetJump](../../debugger/debug-interface-access/idiasymbol-get-hassetjump.md)
- [longjmp](/cpp/c-runtime-library/reference/longjmp)
- [setjmp](/cpp/c-runtime-library/reference/setjmp)

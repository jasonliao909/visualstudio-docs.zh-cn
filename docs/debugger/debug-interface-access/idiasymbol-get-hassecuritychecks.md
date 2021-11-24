---
description: 检索一个标记，该标记指定是否已使用缓冲区溢出安全检查（例如，/GS (缓冲区安全检查)编译器开关）对编译单位或函数进行编译。
title: IDiaSymbol::get_hasSecurityChecks | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_hasSecurityChecks method
ms.assetid: 4bb51f62-8645-41a4-bc44-1451010623fd
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 95ab646b7ba88bc82d2ebcd35d5be925e51f1af3
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832526"
---
# <a name="idiasymbolget_hassecuritychecks"></a>IDiaSymbol::get_hasSecurityChecks
检索一个标记，该标记指定是否已使用缓冲区溢出安全检查（例如，[/GS (缓冲区安全检查)](/cpp/build/reference/gs-buffer-security-check)编译器开关）对编译单位或函数进行编译。

## <a name="syntax"></a>语法

```C++
HRESULT get_hasSecurityChecks(
   BOOL *pFlag
);
```

#### <a name="parameters"></a>参数
 `pFlag`

[out] 如果函数具有任何安全检查，则返回 `TRUE`；否则，返回 `FALSE`。

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
- [/GS（缓冲区安全检查）](/cpp/build/reference/gs-buffer-security-check)

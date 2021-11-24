---
description: 指定此符号是否是指向成员函数的指针。
title: IDiaSymbol::get_isPointerToMemberFunction | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: aa9b5599-9602-41be-ab50-d84b90bee72f
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: dd666577e7e37807105f32ca89d9e224a5cdf3b8
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832752"
---
# <a name="idiasymbolget_ispointertomemberfunction"></a>IDiaSymbol::get_isPointerToMemberFunction
指定此符号是否是指向成员函数的指针。

## <a name="syntax"></a>语法

```C++
HRESULT get_isPointerToMemberFunction(
   BOOL* pRetVal);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 指向指定此符号是否是指向成员函数的指针的 `BOOL` 的指针。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则返回 `S_FALSE` 或错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)

---
description: 检索一个标记，该标记指定类或方法是否已密封。
title: IDiaSymbol::get_sealed | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_sealed method
ms.assetid: cd1fef1f-47de-47c7-885f-f6f0a9a07d8c
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: d86b78041bd4f78a382c82e95f4b330e7ddd5d2a
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832714"
---
# <a name="idiasymbolget_sealed"></a>IDiaSymbol::get_sealed
检索一个标记，该标记指定类或方法是否已密封。

## <a name="syntax"></a>语法

```C++
HRESULT get_sealed( 
   BOOL* pRetVal)
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 如果类或方法已密封，则返回 `TRUE`；否则，返回 `FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。

## <a name="remarks"></a>备注
 密封类不能用作基类。 密封方法不能被重写。

## <a name="requirements"></a>要求
 标头：Dia2.h

 库：diaguids.lib

 DLL：msdia100.dll

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)

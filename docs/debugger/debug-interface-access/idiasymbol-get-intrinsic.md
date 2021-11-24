---
description: 检索一个标记，该标记指定类是否为内部类型。
title: IDiaSymbol::get_intrinsic | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_intrinsic method
ms.assetid: f969f595-d9f9-48b9-adaa-63a6e4e09575
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 4e5ac1796a1a876a454dc976688799ba1033570e
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832487"
---
# <a name="idiasymbolget_intrinsic"></a>IDiaSymbol::get_intrinsic
检索一个标记，该标记指定类是否为内部类型。

## <a name="syntax"></a>语法

```C++
HRESULT get_intrinsic( 
   BOOL* pRetVal)
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 如果类是内部类型，则返回 `TRUE`；否则，返回 `FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。

## <a name="remarks"></a>备注

## <a name="requirements"></a>要求
 标头：Dia2.h

 库：diaguids.lib

 DLL：msdia100.dll

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)

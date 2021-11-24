---
description: 检索此符号的编译器特定类型标识符值数组。
title: IDiaSymbol::get_typeIds | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_typeIds method
ms.assetid: 5166e647-fde5-4efe-92bf-77f8ae3fbc9b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 0324891d5819ea850d1a4cd21464778a93ea78ba
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832650"
---
# <a name="idiasymbolget_typeids"></a>IDiaSymbol::get_typeIds
检索此符号的编译器特定类型标识符值数组。

## <a name="syntax"></a>语法

```C++
HRESULT get_typeIds ( 
   DWORD  cTypeIds,
   DWORD* pcTypeIds,
   DWORD  typeIds[]
);
```

#### <a name="parameters"></a>参数
 `cTypeIds`

[in] 用于保留数据的缓冲区的大小。

 `pcTypeIds`

[out] 返回写入的 `typeIds` 数，如果 `typeIds` 为 `NULL`，则返回可用的类型标识符总数。

 `typeIds[]`

[out] 要用类型标识符填充的数组。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)

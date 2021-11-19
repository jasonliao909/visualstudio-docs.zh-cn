---
description: 检索此符号的编译器特定类型的数组。
title: IDiaSymbol：： get_types |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_types method
ms.assetid: 5f056e0c-e15b-4e00-8f78-aadc8574f7ea
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 9258e80ea3a3a050daebc1ea1189a573733c928b
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832481"
---
# <a name="idiasymbolget_types"></a>IDiaSymbol::get_types
检索此符号的编译器特定类型的数组。

## <a name="syntax"></a>语法

```C++
HRESULT get_types ( 
   DWORD       cTypes,
   DWORD*      pcTypes,
   IDiaSymbol* types[]
);
```

#### <a name="parameters"></a>参数
 `cTypes`

中用于保存数据的缓冲区大小。

 `pcTypes`

弄返回写入的类型的数目，或者如果 `types` 参数为 `NULL` ，则返回可用的类型总数。

 `types[]`

弄要使用表示此符号的所有类型的 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) 对象填充的数组。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回 `S_FALSE` 错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)

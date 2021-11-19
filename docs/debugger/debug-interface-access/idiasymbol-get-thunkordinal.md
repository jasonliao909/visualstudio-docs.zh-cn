---
description: 检索函数的 thunk 类型。
title: IDiaSymbol::get_thunkOrdinal | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_thunkOrdinal method
ms.assetid: 4b28d78a-1974-4d8a-8bb7-781bf630f2f4
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 06ad9b4e11e81a337095b49a15411688e2974e1f
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831706"
---
# <a name="idiasymbolget_thunkordinal"></a>IDiaSymbol::get_thunkOrdinal
检索函数的 thunk 类型。

## <a name="syntax"></a>语法

```C++
HRESULT get_thunkOrdinal ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄从 [THUNK_ORDINAL 枚举](../../debugger/debug-interface-access/thunk-ordinal.md) 枚举返回一个值，该值指定函数的 THUNK 类型。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回 `S_FALSE` 错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。

## <a name="remarks"></a>备注
 仅当符号为的 [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md) 值时，此属性才有效 `SymTagThunk` 。

 "Thunk" 是一段代码，用于在32位内存地址 (空间（也称为平面地址空间) ）和16位地址空间（)  (称为分段地址空间）之间进行转换。

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [THUNK_ORDINAL 枚举](../../debugger/debug-interface-access/thunk-ordinal.md)
- [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)

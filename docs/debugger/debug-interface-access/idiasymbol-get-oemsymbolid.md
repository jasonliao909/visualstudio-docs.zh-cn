---
description: 检索 Original Equipment Manufacturer (OEM) 符号的 ID 值。
title: IDiaSymbol::get_oemSymbolId | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_oemSymbolId method
ms.assetid: 187801f0-bd82-4c5b-9fae-8eeb1a4ac0ce
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: a241d75b9a073b3ba4072e6d287ea64a5c2ad202
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831794"
---
# <a name="idiasymbolget_oemsymbolid"></a>IDiaSymbol::get_oemSymbolId
检索 Original Equipment Manufacturer (OEM) 符号的 ID 值。

## <a name="syntax"></a>语法

```C++
HRESULT get_oemSymbolId ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 返回 OEM 的内部分配的符号 ID。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。

## <a name="remarks"></a>备注
 标识符是由 DIA SDK 创建的唯一值，用于将所有符号标记为唯一。

 此属性仅适用于具有 `SymTagCustomType` 的 [SymTagEnum Enumeration](../../debugger/debug-interface-access/symtagenum.md) 类型的符号。

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)

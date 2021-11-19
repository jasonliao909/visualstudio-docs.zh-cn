---
title: CustomType |Microsoft Docs
description: 在 Visual Studio 调试接口访问 SDK 中查找有关 CustomType 符号类型 (SymTagCustomType) 的参考信息。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- CustomType symbol
ms.assetid: 1b66bc0a-7979-416f-bf7f-e5df91584c91
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 4caaa6094c15cc3f51cb3a0c6f3341781d4036f5
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832403"
---
# <a name="customtype"></a>CustomType
供应商定义的类型 (编译器特定类型) 由 `SymTagCustomType` 符号标识。

## <a name="properties"></a>属性
 下表显示了此符号类型的其他有效属性。

|属性|数据类型|说明|
|--------------|---------------|-----------------|
|[IDiaSymbol::get_oemId](../../debugger/debug-interface-access/idiasymbol-get-oemid.md)|`DWORD`|OEM 的标识符。|
|[IDiaSymbol::get_oemSymbolId](../../debugger/debug-interface-access/idiasymbol-get-oemsymbolid.md)|`DWORD`|OEM 的内部 ID。|
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|符号的索引 ID。|
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|返回 `SymTagCustomType` () 的 [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md) 值之一。|
|[IDiaSymbol::get_type](../../debugger/debug-interface-access/idiasymbol-get-type.md)|`IDiaSymbol*`|自定义类型符号引用的第一个类型。|
|[IDiaSymbol::get_typeId](../../debugger/debug-interface-access/idiasymbol-get-typeid.md)|`DWORD`|类型符号的 ID。|
|[IDiaSymbol::get_types](../../debugger/debug-interface-access/idiasymbol-get-types.md)|`IDiaSymbol**`|自定义类型符号引用的所有类型的数组。|

## <a name="see-also"></a>另请参阅
- [符号类型的类层次结构](../../debugger/debug-interface-access/class-hierarchy-of-symbol-types.md)
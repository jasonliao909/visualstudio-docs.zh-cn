---
title: 批注 | Microsoft Docs
description: 在 Visual Studio 调试接口访问 SDK 中查找有关 Annotation 符号类型 (SymTagAnnotation) 的参考信息。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- SymTabAnnotation symbol
- Annotation symbol
ms.assetid: eb9f759b-98a5-45fc-b085-91f1f2666e72
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 0e1db9552311196400ef2aa9b70610c7aa9e3726
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832423"
---
# <a name="annotation"></a>Annotation
位置程序代码可以使用 `SymTagAnnotation` 符号进行注释。

## <a name="properties"></a>属性
 下表显示了对此符号类型有效的属性。

|属性|数据类型|说明|
|--------------|---------------|-----------------|
|[IDiaSymbol::get_addressOffset](../../debugger/debug-interface-access/idiasymbol-get-addressoffset.md)|`DWORD`|位置的偏移部分；有关详细信息，请参阅 [LocationType Enumeration](../../debugger/debug-interface-access/locationtype.md)。|
|[IDiaSymbol::get_addressSection](../../debugger/debug-interface-access/idiasymbol-get-addresssection.md)|`DWORD`|位置的节部分；有关详细信息，请参阅 [LocationType Enumeration](../../debugger/debug-interface-access/locationtype.md)。|
|[IDiaSymbol::get_dataKind](../../debugger/debug-interface-access/idiasymbol-get-datakind.md)|`DWORD`|[DataKind Enumeration](../../debugger/debug-interface-access/datakind.md) 值之一。|
|[IDiaSymbol::get_relativeVirtualAddress](../../debugger/debug-interface-access/idiasymbol-get-relativevirtualaddress.md)|`DWORD`|此注释在其模块中的相对位置。|
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|符号的索引 ID。|
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|返回 `SymTagAnnotation`（[SymTagEnum Enumeration](../../debugger/debug-interface-access/symtagenum.md) 值之一）。|
|[IDiaSymbol::get_value](../../debugger/debug-interface-access/idiasymbol-get-value.md)|`VARIANT`|常数数据的值。|
|[IDiaSymbol::get_virtualAddress](../../debugger/debug-interface-access/idiasymbol-get-virtualaddress.md)|`ULONGLONG`|此注释在可执行映像中的位置。|

## <a name="see-also"></a>另请参阅
- [符号类型的词法层次结构](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)
- [LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)
- [符号位置](../../debugger/debug-interface-access/symbol-locations.md)
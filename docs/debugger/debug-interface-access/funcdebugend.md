---
description: 如果函数具有定义的调试结束点，则调试起点由带有 SymTagFuncDebugEnd 标记的符号标识。
title: FuncDebugEnd | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- FuncDebugEnd symbol
- debugging [DIA SDK], end point
ms.assetid: 68f84fff-7cd3-4636-b929-7063a45009f8
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 40094e48b58ee7ed5e9646afe80c6ecd5cc9a6f9
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832365"
---
# <a name="funcdebugend"></a>FuncDebugEnd
如果函数具有定义的调试结束点，则调试起点由带有 `SymTagFuncDebugEnd` 标记的符号标识。

## <a name="properties"></a>属性
 下表显示了对此符号类型有效的属性。

|属性|数据类型|说明|
|--------------|---------------|-----------------|
|[IDiaSymbol::get_addressOffset](../../debugger/debug-interface-access/idiasymbol-get-addressoffset.md)|`DWORD`|位置的偏移部分；有关详细信息，请参阅 [LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)。|
|[IDiaSymbol::get_addressSection](../../debugger/debug-interface-access/idiasymbol-get-addresssection.md)|`DWORD`|位置的节部分；有关详细信息，请参阅 [LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)。|
|[IDiaSymbol::get_customCallingConvention](../../debugger/debug-interface-access/idiasymbol-get-customcallingconvention.md)|`BOOL`|如果函数使用自定义调用约定（仅在 DIA SDK V8.0 或更高版本中），则为 `TRUE`。|
|[IDiaSymbol::get_farReturn](../../debugger/debug-interface-access/idiasymbol-get-farreturn.md)|`BOOL`|如果函数执行远返回（仅在 DIA SDK V8.0 或更高版本中），则为 `TRUE`。|
|[IDiaSymbol::get_interruptReturn](../../debugger/debug-interface-access/idiasymbol-get-interruptreturn.md)|`BOOL`|如果函数包含从中断返回（仅在 DIA SDK V8.0 或更高版本中），则为 `TRUE`。|
|[IDiaSymbol::get_isStatic](../../debugger/debug-interface-access/idiasymbol-get-isstatic.md)|`BOOL`|如果函数是静态的（仅在 DIA SDK V8.0 或更高版本中），则为 `TRUE`。|
|[IDiaSymbol::get_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md)|`IDiaSymbol*`|封闭函数的符号。|
|[IDiaSymbol::get_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md)|`DWORD`|词法父级符号的 ID。|
|[IDiaSymbol::get_locationType](../../debugger/debug-interface-access/idiasymbol-get-locationtype.md)|`DWORD`|终结点具有静态位置；有关详细信息，请参阅[符号位置](../../debugger/debug-interface-access/symbol-locations.md)。|
|[IDiaSymbol::get_noInline](../../debugger/debug-interface-access/idiasymbol-get-noinline.md)|`BOOL`|如果函数是用 [noinline](/cpp/cpp/noinline) 特性指定的（仅在 DIA SDK V8.0 或更高版本中），则为 `TRUE`。|
|[IDiaSymbol::get_noReturn](../../debugger/debug-interface-access/idiasymbol-get-noreturn.md)|`BOOL`|如果函数是用 [noreturn](/cpp/cpp/noreturn) 特性指定的（仅在 DIA SDK V8.0 或更高版本中），则为 `TRUE`。|
|[IDiaSymbol::get_notReached](../../debugger/debug-interface-access/idiasymbol-get-notreached.md)|`BOOL`|如果从未调用函数（仅在 DIA SDK V8.0 或更高版本中），则为 `TRUE`。|
|[IDiaSymbol::get_offset](../../debugger/debug-interface-access/idiasymbol-get-offset.md)|`LONG`|内存中符号的偏移；有关详细信息，请参阅 [LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)、`LocIsRegRel`。|
|[IDiaSymbol::get_optimizedCodeDebugInfo](../../debugger/debug-interface-access/idiasymbol-get-optimizedcodedebuginfo.md)|`BOOL`|如果该函数具有优化代码的调试信息（仅在 DIA SDK V8.0 或更高版本中），则为 `TRUE`。|
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|符号的索引 ID。|
|[IDiaSymbol::get_relativeVirtualAddress](../../debugger/debug-interface-access/idiasymbol-get-relativevirtualaddress.md)|`DWORD`|此函数在其模块中结束的相对位置。|
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|返回 `SymTagFuncDebugEnd`（[SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)值之一）。|
|[IDiaSymbol::get_virtualAddress](../../debugger/debug-interface-access/idiasymbol-get-virtualaddress.md)|`ULONGLONG`|此函数在可执行映像中的位置。|

## <a name="see-also"></a>另请参阅
- [符号类型的词法层次结构](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)
- [LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)
- [符号位置](../../debugger/debug-interface-access/symbol-locations.md)

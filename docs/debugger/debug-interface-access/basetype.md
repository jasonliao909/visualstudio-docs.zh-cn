---
title: BaseType | Microsoft Docs
description: 在调试接口访问 SDK 中查找有关 SymTagBaseType (的) 类型Visual Studio参考信息。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- BaseType symbol [DIA SDK]
ms.assetid: 2f9e22e6-8360-496a-ac6b-17a5a56b0c46
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 6afb4b2bfd99a8f944ab0d5d3d2a27e2c521371f
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832420"
---
# <a name="basetype"></a>BaseType
基类型由符号 `SymTagBaseType` 标识。

## <a name="properties"></a>属性
 下表显示了此符号类型的其他有效属性。

|属性|数据类型|说明|
|--------------|---------------|-----------------|
|[IDiaSymbol::get_baseType](../../debugger/debug-interface-access/idiasymbol-get-basetype.md)|`DWORD`|BasicType 枚举 [的值之一](../../debugger/debug-interface-access/basictype.md)。|
|[IDiaSymbol::get_constType](../../debugger/debug-interface-access/idiasymbol-get-consttype.md)|`BOOL`|`TRUE` 如果基类型标记为 const，则为 。|
|[IDiaSymbol::get_length](../../debugger/debug-interface-access/idiasymbol-get-length.md)|`LONGLONG`|基类型的大小（以字节为单位）。|
|[IDiaSymbol::get_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md)|`IDiaSymbol*`|封闭的 [Compiland 的符号](../../debugger/debug-interface-access/compiland.md)。|
|[IDiaSymbol::get_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md)|`DWORD`|词法父符号的 ID。|
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|符号的索引 ID。|
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|返回 `SymTagBaseType` ([SymTagEnum 枚举值之一) 。](../../debugger/debug-interface-access/symtagenum.md)|
|[IDiaSymbol::get_unalignedType](../../debugger/debug-interface-access/idiasymbol-get-unalignedtype.md)|`BOOL`|`TRUE` 如果基类型未对齐，则为 。|
|[IDiaSymbol::get_volatileType](../../debugger/debug-interface-access/idiasymbol-get-volatiletype.md)|`BOOL`|`TRUE` 如果基类型标记为易失性，则为 。|

## <a name="see-also"></a>另请参阅
- [BasicType 枚举](../../debugger/debug-interface-access/basictype.md)
- [符号类型的类层次结构](../../debugger/debug-interface-access/class-hierarchy-of-symbol-types.md)
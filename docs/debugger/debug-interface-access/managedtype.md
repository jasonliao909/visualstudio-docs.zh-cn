---
description: 托管类型 (元数据定义的任何符号，或者由 SymTagManagedType 符号标识的语言（如 C#) ）的内存和资源管理功能的本机类型。
title: ManagedType | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- SymTagManagedType symbol
- managed type symbol
- ManagedType symbol
ms.assetid: 5db99e2a-4f2e-4796-89b7-b401b151826f
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- dotnet
ms.openlocfilehash: 5dc58ad37599c9c2ac7a8964bf968c7b070e6b59
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832809"
---
# <a name="managedtype"></a>ManagedType
托管类型 (元数据定义的任何符号，或本机语言（如 C#) ）的内存和资源管理功能由符号 `SymTagManagedType` 标识。

## <a name="properties"></a>属性
 下表显示了此符号类型的其他有效属性。

|属性|数据类型|说明|
|--------------|---------------|-----------------|
|[IDiaSymbol::get_name](../../debugger/debug-interface-access/idiasymbol-get-name.md)|`BSTR`|托管符号的名称。|
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|符号的索引 ID。|
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|返回 `SymTagManagedType` ([SymTagEnum 枚举值之一) 。](../../debugger/debug-interface-access/symtagenum.md)|

## <a name="see-also"></a>另请参阅
- [符号类型的类层次结构](../../debugger/debug-interface-access/class-hierarchy-of-symbol-types.md)

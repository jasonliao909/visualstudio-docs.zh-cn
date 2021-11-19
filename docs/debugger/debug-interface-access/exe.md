---
description: Exe 是没有词法或类父级的唯一符号，因为它表示 .exe 或 .dll 文件的全局范围。
title: Exe | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- .dll files
- Exe symbol
- .exe files
- executable files, Exe symbol
ms.assetid: a781d2cf-55fe-4373-9cf1-b732864244e0
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 32f559e2365e0c422497573dc19ce2ce094caa9a
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832368"
---
# <a name="exe"></a>Exe
Exe 是没有词法或类父级的唯一符号，因为它表示 .exe 或 .dll 文件的全局范围。 每个文件只有一个带有 `SymTagExe` 标记的符号。 [IDiaSession::get_globalScope](../../debugger/debug-interface-access/idiasession-get-globalscope.md) 方法返回符号。

## <a name="properties"></a>属性
 下表显示了对此符号类型有效的属性。

|属性|数据类型|说明|
|--------------|---------------|-----------------|
|[IDiaSymbol::get_age](../../debugger/debug-interface-access/idiasymbol-get-age.md)|`DWORD`|此可执行文件的期限。|
|[IDiaSymbol::get_guid](../../debugger/debug-interface-access/idiasymbol-get-guid.md)|`GUID`|此可执行文件的 `GUID`。|
|[IDiaSymbol::get_isCTypes](../../debugger/debug-interface-access/idiasymbol-get-isctypes.md)|`BOOL`|如果与此可执行文件关联的符号文件包含 C 类型，则为 `TRUE`（仅在 DIA SDK v8.0 或更高版本中）。|
|[IDiaSymbol::get_isStripped](../../debugger/debug-interface-access/idiasymbol-get-isstripped.md)|`BOOL`|如果已从与此可执行文件关联的符号文件中去除私有符号，则为 `TRUE`（仅在 DIA SDK v8.0 或更高版本中）。|
|[IDiaSymbol::get_machineType](../../debugger/debug-interface-access/idiasymbol-get-machinetype.md)|`DWORD`|指示目标 CPU 的值（[CV_CPU_TYPE_e Enumeration](../../debugger/debug-interface-access/cv-cpu-type-e.md) 值之一）。|
|[IDiaSymbol::get_name](../../debugger/debug-interface-access/idiasymbol-get-name.md)|`BSTR`|.exe 文件的名称。|
|[IDiaSymbol::get_signature](../../debugger/debug-interface-access/idiasymbol-get-signature.md)|`DWORD`|可执行文件的签名。|
|[IDiaSymbol::get_symbolsFileName](../../debugger/debug-interface-access/idiasymbol-get-symbolsfilename.md)|`BSTR`|.exe 文件的 .pdb 或 .dbg 文件的完整路径。|
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|符号的索引 ID。|
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|返回 `SymTagExe`（[SymTagEnum Enumeration](../../debugger/debug-interface-access/symtagenum.md) 值之一）。|

## <a name="see-also"></a>另请参阅
- [IDiaSession::get_globalScope](../../debugger/debug-interface-access/idiasession-get-globalscope.md)
- [符号类型的词法层次结构](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)

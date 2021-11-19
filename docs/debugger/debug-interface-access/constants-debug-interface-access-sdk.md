---
title: " (调试接口访问 SDK) 的常量 |Microsoft Docs"
description: 查看可用于通过调试接口访问 (DIA) SDK 来识别程序调试数据库的各个部分的字符串常量列表 (PDB) 文件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- constants, DIA SDK
- DIA SDK, constants
ms.assetid: aca4ec77-bc08-4cdd-a6ce-8d4a28ea5ea3
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 3db5105f310bdb3493262965f313620b66393651
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832404"
---
# <a name="constants-debug-interface-access-sdk"></a>常量（调试接口访问 SDK）
这些字符串常量可用于通过 DIA SDK 标识程序调试数据库 (PDB) 文件的各个部分。

## <a name="constants"></a>常量
以下声明为 C/c + + 宏。

|宏|值|
|-----------|-----------|
|`DiaTable_Symbols`|L "符号"|
|`DiaTable_Sections`|L "Sections"|
|`DiaTable_SrcFiles`|L "SourceFiles"|
|`DiaTable_LineNums`|L"LineNumbers"|
|`DiaTable_SegMap`|L"SegmentMap"|
|`DiaTable_Dbg`|L"Dbg"|
|`DiaTable_InjSrc`|L "InjectedSource"|
|`DiaTable_FrameData`|L"FrameData"|

## <a name="example"></a>示例
下面是一个使用以下符号的示例：

```C++
HRESULT GetSymbolTable(IDiaEnumTables *pEnumTables, IDiaTable **pTable)
{
    HRESULT hr;
    VARIANT var;
    var.vt      = VT_BSTR;
    var.bstrVal = SysAllocString( DiaTable_Symbols );
    hr = pEnumTables->Item( var, pTable );
    return(hr);
}
```

## <a name="requirements"></a>要求
标头： dia2

## <a name="see-also"></a>另请参阅
- [引用](../../debugger/debug-interface-access/debug-interface-access-sdk-reference.md)
- [枚举和结构](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaEnumTables::Item](../../debugger/debug-interface-access/idiaenumtables-item.md)

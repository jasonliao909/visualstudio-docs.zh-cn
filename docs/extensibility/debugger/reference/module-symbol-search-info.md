---
description: 包含有关已搜索的符号搜索路径的状态信息。
title: MODULE_SYMBOL_SEARCH_INFO |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MODULE_SYMBOL_SEARCH_INFO
helpviewer_keywords:
- MODULE_SYMBOL_SEARCH_INFO structure
ms.assetid: 432aff03-08a5-4c5a-b2d5-e212090fc70a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 78308844f64e87c95a41b662c2055f770809f262
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122125291"
---
# <a name="module_symbol_search_info"></a>MODULE_SYMBOL_SEARCH_INFO

包含有关已搜索的符号搜索路径的状态信息。

## <a name="syntax"></a>语法

```cpp
typedef struct _tagSYMBOL_SEARCH_INFO
{
    SYMBOL_SEARCH_INFO_FIELDS dwValidFields;
    BSTR                      bstrVerboseSearchInfo;
} MODULE_SYMBOL_SEARCH_INFO;
```

```csharp
public struct MODULE_SYMBOL_SEARCH_INFO {
    public uint   dwValidFields;
    public string bstrVerboseSearchInfo;
}
```

## <a name="members"></a>成员

`dwValidFields`\
[SYMBOL_SEARCH_INFO_FIELDS](../../../extensibility/debugger/reference/symbol-search-info-fields.md)枚举中的标志的组合，指定此结构中所述的搜索信息种类。

`bstrVerboseSearchInfo`\
搜索路径和结果连接成一个字符串。

## <a name="remarks"></a>备注

此结构是通过调用 [GetSymbolInfo](../../../extensibility/debugger/reference/idebugmodule3-getsymbolinfo.md) 方法返回的。

如果该 `bstrVerboseSearchInfo` 字段不为空，则它包含搜索的路径列表和该搜索的结果。 该列表的格式为路径，后跟省略号 ( "..." ) ，然后是结果。 如果有多个路径结果对，则每个对都由 "\r\n" (回车符/换行符) 对分隔。 模式如下所示：

\<path>...\<result>\r\n\<path> ... \<result>\r\n\<path> .。。\<result>

请注意，最后一个条目没有 \r\n 的序列。

下面是一个已 `bstrVerboseSearchInfo` 发送到标准输出的可能字符串。

`c:\symbols\user32.pdb... File not found.`

`c:\winnt\symbols\user32.pdb... Version does not match.`

`\\symbols\symbols\user32.dll\0a8sd0ad8ad\user32.pdb... Symbols loaded.`

## <a name="requirements"></a>要求

标头： msdbg

命名空间： VisualStudio

程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅

- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetSymbolInfo](../../../extensibility/debugger/reference/idebugmodule3-getsymbolinfo.md)

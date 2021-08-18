---
description: 检索搜索符号的路径列表以及每个路径的搜索结果。
title: IDebugModule3：：GetSymbolInfo |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugModule3::GetSymbolInfo
helpviewer_keywords:
- GetSymbolInfo method
- IDebugModule3::GetSymbolInfo method
ms.assetid: dda5e8e1-6878-4aa9-9ee4-e7d0dcc11210
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d187673c7f2a5f33ecdedd5fe88a3b62d518edc0
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122133115"
---
# <a name="idebugmodule3getsymbolinfo"></a>IDebugModule3::GetSymbolInfo
检索搜索符号的路径列表以及每个路径的搜索结果。

## <a name="syntax"></a>语法

```cpp
HRESULT GetSymbolInfo(
    SYMBOL_SEARCH_INFO_FIELDS  dwFields,
    MODULE_SYMBOL_SEARCH_INFO* pInfo
);
```

```csharp
int GetSymbolInfo(
    enum_SYMBOL_SEARCH_INFO_FIELDS dwFields,
    MODULE_SYMBOL_SEARCH_INFO[]    pinfo
);
```

## <a name="parameters"></a>参数
`dwFields`\
[in]来自 SYMBOL_SEARCH_INFO_FIELDS [标志的组合](../../../extensibility/debugger/reference/symbol-search-info-fields.md) ，指定要填充 `pInfo` 的哪些字段。

`pInfo`\
[out]一 [MODULE_SYMBOL_SEARCH_INFO](../../../extensibility/debugger/reference/module-symbol-search-info.md) 结构，其成员将用指定的信息填充。 如果这是一个 null 值，则此方法返回 `E_INVALIDARG` 。

## <a name="return-value"></a>返回值
如果方法成功，则返回 `S_OK` ;否则返回错误代码。

> [!NOTE]
> 即使返回 (，) `MODULE_SYMBOL_SEARCH_INFO` 返回的字符串可能 `S_OK` 为空。 在这种情况下，没有要返回的搜索信息。

## <a name="remarks"></a>备注
如果 结构的 字段不为空，则它包含搜索的路径列表以及 `bstrVerboseSearchInfo` `MODULE_SYMBOL_SEARCH_INFO` 该搜索的结果。 列表的格式为路径，后跟省略号 ("...") ，后跟结果。 如果路径结果对不止一个，则每对由"\r\n"分隔 (回车/换行) 对。 模式如下所示：

\<path>...\<result>\r\n... \<path> \<result>\r\n\<path> ...\<result>

请注意，最后一个条目没有\r\n序列。

## <a name="example"></a>示例
此示例中，此方法返回包含三个不同搜索结果的三个路径。 每行以回车/换行对终止。 示例输出仅将搜索结果打印为单个字符串。

> [!NOTE]
> 状态结果是紧接在"..."之后的所有内容直到行尾。

```cpp
void ShowSymbolSearchResults(IDebugModule3 *pIDebugModule3)
{
    MODULE_SYMBOL_SEARCH_INFO ssi = { 0 };
    HRESULT hr;
    hr = pIDebugModule3->GetSymbolInfo(SSIF_VERBOSE_SEARCH_INFO,&ssi);
    if (SUCCEEDED(hr)) {
        CComBSTR searchInfo = ssi.bstrVerboseSearchInfo;
        if (searchInfo.Length() != 0) {
            std::wcout << (wchar_t *)(BSTR)searchInfo;
            std::wcout << std::endl;
        }
    }
}
```

**c：\symbols\user32.pdb...找不到文件。** 
**c：\winnt\symbols\user32.pdb...版本不匹配。** 
**\\\symbols\symbols\user32.dll\0a8sd0ad8ad\user32.pdb...已加载符号。**

## <a name="see-also"></a>请参阅

- [SYMBOL_SEARCH_INFO_FIELDS](../../../extensibility/debugger/reference/symbol-search-info-fields.md)
- [MODULE_SYMBOL_SEARCH_INFO](../../../extensibility/debugger/reference/module-symbol-search-info.md)
- [IDebugModule3](../../../extensibility/debugger/reference/idebugmodule3.md)

---
description: 获取与此文档上下文关联的语言。
title: IDebugDocumentContext2：： GetLanguageInfo |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentContext2::GetLanguageInfo
helpviewer_keywords:
- IDebugDocumentContext2::GetLanguageInfo
ms.assetid: 6a212ee5-414c-4eb5-ab11-19db1786943d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f21a9dbc1d74815eb9adf4bcd3ac3ce6ec10dedd341352dd108c5aa88803e29f
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121323594"
---
# <a name="idebugdocumentcontext2getlanguageinfo"></a>IDebugDocumentContext2::GetLanguageInfo
获取与此文档上下文关联的语言。

## <a name="syntax"></a>语法

```cpp
HRESULT GetLanguageInfo(
    BSTR* pbstrLanguage,
    GUID* pguidLanguage
);
```

```csharp
int GetLanguageInfo(
    out string pbstrLanguage,
    out Guid   pguidLanguage
);
```

## <a name="parameters"></a>参数
`pbstrLanguage`\
弄返回在此文档上下文中实现代码的语言的名称。

`pguidLanguage`\
弄返回在此文档上下文中实现代码的语言的 GUID。 例如，`guidVBScriptLang` 或 `guidCPPLang`。 此 GUID 并不局限于提供的语言 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] 。

## <a name="return-value"></a>返回值
如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="example"></a>示例
下面的示例演示如何为 `CDebugContext` 公开 [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md) 接口的简单对象实现此方法。

```cpp
HRESULT CDebugContext::GetLanguageInfo(BSTR* pbstrLanguage, GUID* pguidLanguage)
{
    HRESULT hr;

    // Check for a valid language argument pointers.
    if (pbstrLanguage && pguidLanguage)
    {
        *pguidLanguage = GUID_NULL;
        *pbstrLanguage = SysAllocString(L"Batch File");
        if (*pbstrLanguage)
        {
            *pguidLanguage = guidBatLang;
            hr = S_OK;
        }
        else
        {
            hr = E_OUTOFMEMORY;
        }
    }
    else
    {
        hr = E_INVALIDARG;
    }

    return hr;
}
```

## <a name="see-also"></a>另请参阅
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)

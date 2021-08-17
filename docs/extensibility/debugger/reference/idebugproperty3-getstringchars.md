---
description: 检索与此属性关联的字符串，并存储在用户提供的缓冲区中。
title: IDebugProperty3：：GetStringChars |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty3::GetStringChars
helpviewer_keywords:
- IDebugProperty3::GetStringChars
ms.assetid: 832c37f3-85cb-4227-8ab2-f27a80eafe90
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8056b6ebcbb9d6758c05d482b02f0cac584d4a3e7a21974562b7e83658d32308
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121402398"
---
# <a name="idebugproperty3getstringchars"></a>IDebugProperty3::GetStringChars
检索与此属性关联的字符串，并存储在用户提供的缓冲区中。

## <a name="syntax"></a>语法

```cpp
HRESULT GetStringChars(
    ULONG  buflen,
    WCHAR* rgString,
    ULONG* pceltFetched
);
```

```csharp
int GetStringChars(
    uint       buflen,
    out string rgString,
    out uint   pceltFetched
);
```

## <a name="parameters"></a>参数
`buflen`\
[in]用户提供的缓冲区可以保留的最大字符数。

`rgString`\
[out]返回字符串。

 [仅 C++]， `rgString` 是指向接收字符串 Unicode 字符的缓冲区的指针。 此缓冲区必须至少是字符 `buflen` ， (字节) 大小。

`pceltFetched`\
[out]返回实际存储在缓冲区中的字符数。  (`NULL` C++.) 

## <a name="return-value"></a>返回值
如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
在 C++ 中，必须注意确保缓冲区的长度至少为 `buflen` Unicode 字符。 请注意，Unicode 字符长 2 个字节。

> [!NOTE]
> 在 C++ 中，返回的字符串不包含终止 null 字符。 如果给定 `pceltFetched` ， 将指定字符串中的字符数。

## <a name="example"></a>示例

```cpp
CStringW RetrievePropertyString(IDebugProperty2 *pPropInfo)
{
    CStringW returnString = L"";
    CComQIPtr<IDebugProperty3> pProp3 = pPropInfo->pProperty;
    If (pProp3 != NULL) {
        ULONG dwStrLen = 0;
        HRESULT hr;
        hr = pProp3->GetStringCharLength(&dwStrLen);
        if (SUCCEEDED(hr) && dwStrLen > 0) {
            ULONG dwRead;
            CStrBufW buf(returnString,dwStrLen,CStrBuf::SET_LENGTH);
            hr = pProp3->GetStringChars(dwStrLen,
                                        reinterpret_cast<WCHAR*>(static_cast<CStringW::PXSTR>(buf)),
                                        &dwRead);
        }
    }
    return(returnString);
}
```

## <a name="see-also"></a>请参阅
- [GetStringCharLength](../../../extensibility/debugger/reference/idebugproperty3-getstringcharlength.md)
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)

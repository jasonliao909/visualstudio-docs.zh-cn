---
description: 获取引用的选定子项的列表。
title: IDebugReference2：：EnumChildren |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugReference2::EnumChildren
helpviewer_keywords:
- IDebugReference2::EnumChildren
ms.assetid: 35b3c2f3-69f4-4013-b555-f847221f62e8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: bab404519695b71c84c82216606b59529b1d4386
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122029835"
---
# <a name="idebugreference2enumchildren"></a>IDebugReference2::EnumChildren
获取引用的选定子项的列表。 保留供将来使用。

## <a name="syntax"></a>语法

```cpp
HRESULT EnumChildren ( 
   DEBUGREF_INFO_FLAGS        dwFields,
   DWORD                      dwRadix,
   DBG_ATTRIB_FLAGS           dwAttribFilter,
   LPCOLESTR                  pszNameFilter,
   DWORD                      dwTimeout,
   IEnumDebugReferenceInfo2** ppEnum
);
```

```csharp
int EnumChildren ( 
   enum_DEBUGREF_INFO_FLAGS     dwFields,
   uint                         dwRadix,
   enum_DBG_ATTRIB_FLAGS        dwAttribFilter,
   string                       pszNameFilter,
   uint                         dwTimeout,
   out IEnumDebugReferenceInfo2 ppEnum
);
```

## <a name="parameters"></a>参数
`dwFields`\
[in]集合中标志的组合[DEBUGREF_INFO_FLAGS](../../../extensibility/debugger/reference/debugref-info-flags.md)枚举，指定要填充枚举DEBUG_REFERENCE_INFO中的哪些字段。 [](../../../extensibility/debugger/reference/debug-reference-info.md)

`dwRadix`\
[in]用于设置任何数值信息格式的基数。

`dwAttribFilter`\
[in]来自 DBG_ATTRIB_FLAGS [标志的组合](../../../extensibility/debugger/reference/dbg-attrib-flags.md) ，该枚举用作筛选器，并结合 参数选择要 `pszNameFilter` 枚举的结构。

`pszNameFilter`\
[in]一个字符串，指定筛选器（如"MyX"）与 参数结合使用，以选择要 `dwAttribFilter` 枚举的结构。

`dwTimeout`\
[in]从此方法返回之前等待的最大时间（以毫秒为单位）。 使用 `INFINITE` 无限期等待。

`ppEnum`\
[out]返回包含所请求子属性列表的 [IEnumDebugReferenceInfo2](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2.md) 对象。

## <a name="return-value"></a>返回值
 始终返回 `E_NOTIMPL`。

## <a name="see-also"></a>请参阅
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
- [DEBUGREF_INFO_FLAGS](../../../extensibility/debugger/reference/debugref-info-flags.md)
- [DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md)
- [IEnumDebugReferenceInfo2](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2.md)

---
description: 获取DEBUG_REFERENCE_INFO引用的对象结构。
title: IDebugReference2：：GetReferenceInfo |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugReference2::GetReferenceInfo
helpviewer_keywords:
- IDebugReference2::GetReferenceInfo
ms.assetid: ae611714-f114-4cf2-b5bb-37461e6ff289
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 88dc8d4bdbc0e354ccc327aa0c5b6968091c19c6
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602405"
---
# <a name="idebugreference2getreferenceinfo"></a>IDebugReference2::GetReferenceInfo
获取 [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md) 引用的对象结构。 保留供将来使用。

## <a name="syntax"></a>语法

```cpp
HRESULT GetReferenceInfo ( 
   DEBUGREF_INFO_FLAGS   dwFields,
   DWORD                 nRadix,
   DWORD                 dwTimeout,
   IDebugReference2**    rgpArgs,
   DWORD                 dwArgCount,
   DEBUG_REFERENCE_INFO* pReferenceInfo
);
```

```csharp
int GetReferenceInfo ( 
   enum_DEBUGREF_INFO_FLAGS  dwFields,
   uint                      nRadix,
   uint                      dwTimeout,
   IDebugReference2[]        rgpArgs,
   uint                      dwArgCount,
   DEBUG_REFERENCE_INFO[]    pReferenceInfo
);
```

## <a name="parameters"></a>parameters
`dwFields`\
[in]来自 DEBUGREF_INFO_FLAGS [标志的组合](../../../extensibility/debugger/reference/debugref-info-flags.md) ，用于确定要填充在 DEBUG_REFERENCE_INFO [中的字段](../../../extensibility/debugger/reference/debug-reference-info.md) 。

`nRadix`\
[in]用于设置任何数值信息格式的基数。

`dwTimeout`\
[in]从此方法返回之前等待的最大时间（以毫秒为单位）。 使用 `INFINITE` 无限期等待。

`rgpArgs`\
[in] [IDebugReference2 对象的](../../../extensibility/debugger/reference/idebugreference2.md) 数组。 保留供将来使用;设置为 null 值。

`dwArgCount`\
[in]数组中的引用参数 `rgpArgs` 数。 保留供将来使用;设置为 0。

`pReferenceInfo`\
[out]一 [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md) 一个结构，该结构使用属性的说明进行填充。

## <a name="return-value"></a>返回值
 始终返回 `E_NOTIMPL`。

## <a name="see-also"></a>另请参阅
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
- [DEBUGREF_INFO_FLAGS](../../../extensibility/debugger/reference/debugref-info-flags.md)
- [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)

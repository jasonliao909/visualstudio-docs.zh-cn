---
description: 检索枚举序列中指定数量的自定义属性。
title: IEnumDebugCustomAttributes：：Next |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumCustomAttributes::Next
helpviewer_keywords:
- IEnumDebugCustomAttributes::Next
ms.assetid: e36f856b-2619-42d1-b73e-4f2390fc22bd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d840d079df50d6df9fa08235dcf19f47c7d08f89
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122103372"
---
# <a name="ienumdebugcustomattributesnext"></a>IEnumDebugCustomAttributes::Next
检索枚举序列中指定数量的自定义属性。

## <a name="syntax"></a>语法

```cpp
HRESULT Next ( 
   ULONG      celt,
   CODE_PATH* rgelt,
   ULONG*     pceltFetched
);
```

```csharp
int Next(
   uint                        celt,
   out IDebugCustomAttribute[] rgelt,
   ref uint                    pceltFetched
);
```

## <a name="parameters"></a>参数
`celt`\
[in]要检索的元素数。 还指定数组的最大 `rgelt` 大小。

`rgelt`\
[out]要填充 [的 IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md) 对象的数组。

`pceltFetched`\
[out]返回 中实际返回的元素数 `rgelt` 。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果可能返回的元素数少于请求的元素数，则返回 `S_FALSE` ;否则返回错误代码。

## <a name="see-also"></a>请参阅
- [IEnumDebugCustomAttributes](../../../extensibility/debugger/reference/ienumdebugcustomattributes.md)
- [IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md)

---
description: 从代码上下文枚举返回下一组元素。
title: IEnumDebugCodeContexts2：：Next |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugCodeContexts2::Next
helpviewer_keywords:
- IEnumDebugCodeContexts2::Next
ms.assetid: 0d8aa2db-0994-4166-b364-2e25d936fffc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5940b9a53321841f0eec34c8b0cd14694eaa60d6
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122103398"
---
# <a name="ienumdebugcodecontexts2next"></a>IEnumDebugCodeContexts2::Next
返回 枚举中的下一组元素。

## <a name="syntax"></a>语法

```cpp
HRESULT Next(
   ULONG                celt,
   IDebugCodeContext2** rgelt,
   ULONG*               pceltFetched
);
```

```csharp
int Next(
   uint                 celt,
   IDebugCodeContext2[] rgelt,
   ref uint             pceltFetched
);
```

## <a name="parameters"></a>参数
`celt`\
[in]要检索的元素数。 还指定数组的最大 `rgelt` 大小。

`rgelt`\
[in， out]要填充 [的 IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) 元素的数组。

`pceltFetched`\
[out]返回 中实际返回的元素数 `rgelt` 。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果可能返回的元素数少于请求的元素数，则返回 `S_FALSE` ;否则返回错误代码。

## <a name="see-also"></a>请参阅
- [IEnumDebugCodeContexts2](../../../extensibility/debugger/reference/ienumdebugcodecontexts2.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)

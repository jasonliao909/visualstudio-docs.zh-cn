---
description: 设置来自其他引用的引用的值。
title: IDebugReference2：： SetValueAsReference |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugReference2::SetValueAsReference
helpviewer_keywords:
- IDebugReference2::SetValueAsReference
ms.assetid: 94a545d2-16b9-45e9-b2e7-4e49ff90aad0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 48030e2314764767b049502ce081a2711a00111b
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122132530"
---
# <a name="idebugreference2setvalueasreference"></a>IDebugReference2::SetValueAsReference
设置来自其他引用的引用的值。 保留供将来使用。

## <a name="syntax"></a>语法

```cpp
HRESULT SetValueAsReference ( 
   IDebugReference2** rgpArgs,
   DWORD              dwArgCount,
   IDebugReference2*  pValue,
   DWORD              dwTimeout
);
```

```cpp
int SetValueAsReference ( 
   IDebugReference2[] rgpArgs,
   uint               dwArgCount,
   IDebugReference2   pValue,
   uint               dwTimeout
);
```

## <a name="parameters"></a>参数
`rgpArgs`\
中用于确定如何设置引用值的 [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) 对象数组。

`dwArgCount`\
中数组中的引用数。

`pValue`\
中要从其设置属性值的 [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) 对象。

`dwTimeout`\
中从此方法返回前等待的最长时间（以毫秒为单位）。 使用 `INFINITE` 无限期等待。

## <a name="return-value"></a>返回值
 始终返回 `E_NOTIMPL`。

## <a name="see-also"></a>请参阅
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)

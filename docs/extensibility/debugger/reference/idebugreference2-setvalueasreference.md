---
description: 设置来自另一个引用的引用的值。
title: IDebugReference2：：SetValueAsReference |Microsoft Docs
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
ms.openlocfilehash: 83ee60089e2cbe3b1f3c907ea37fe1f87e96ed76b1768d43c51619c75a5b89f0
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121338522"
---
# <a name="idebugreference2setvalueasreference"></a>IDebugReference2::SetValueAsReference
设置来自另一个引用的引用的值。 保留供将来使用。

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
[in]用于确定如何 [设置引用值的 IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) 对象的数组。

`dwArgCount`\
[in]数组中的引用数。

`pValue`\
[in]要 [设置属性值的 IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) 对象。

`dwTimeout`\
[in]从此方法返回之前等待的最大时间（以毫秒为单位）。 使用 `INFINITE` 无限期等待。

## <a name="return-value"></a>返回值
 始终返回 `E_NOTIMPL`。

## <a name="see-also"></a>另请参阅
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)

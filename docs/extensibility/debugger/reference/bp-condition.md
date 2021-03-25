---
description: 描述引发断点的条件。
title: BP_CONDITION |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_CONDITION
helpviewer_keywords:
- BP_CONDITION structure
ms.assetid: 407f87a3-2878-429b-8c65-b68feb36622a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 560cf7184e5fa7b25e35410313535675713742aa
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105085333"
---
# <a name="bp_condition"></a>BP_CONDITION
描述引发断点的条件。

## <a name="syntax"></a>语法

```cpp
typedef struct _BP_CONDITION {
    IDebugThread2* pThread;
    BP_COND_STYLE  styleCondition;
    BSTR           bstrContext;
    BSTR           bstrCondition;
    UINT           nRadix;
} BP_CONDITION;
```

```csharp
public struct BP_CONDITION {
    public IDebugThread2 pThread;
    public uint          styleCondition;
    public string        bstrContext;
    public string        bstrCondition;
    public uint          nRadix;
};
```

## <a name="members"></a>成员
`pThread`\
[IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)对象，表示包含断点的应用程序的活动线程。

`styleCondition`\
[BP_COND_STYLE](../../../extensibility/debugger/reference/bp-cond-style.md)枚举中的一个值，该值描述此断点条件的样式。

`bstrContext`\
断点的位置。

`bstrCondition`\
断点的触发条件。

`nRadix`\
用于计算任何数值信息的基数。

## <a name="remarks"></a>备注
此结构是 [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md) 和 [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md) 结构的成员。

此结构也作为参数传递给 [SetCondition](../../../extensibility/debugger/reference/idebugboundbreakpoint2-setcondition.md) 和 [SetCondition](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-setcondition.md) 方法。

## <a name="requirements"></a>要求
标头： msdbg

命名空间： VisualStudio

程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)
- [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)
- [SetCondition](../../../extensibility/debugger/reference/idebugboundbreakpoint2-setcondition.md)
- [SetCondition](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-setcondition.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [BP_COND_STYLE](../../../extensibility/debugger/reference/bp-cond-style.md)

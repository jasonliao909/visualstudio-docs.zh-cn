---
description: 描述触发断点的条件。
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
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8def7604362e7c1b84adf55dad8a9e10e31e7bb09331e24730e9abbcffcdbccb
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121342695"
---
# <a name="bp_condition"></a>BP_CONDITION
描述触发断点的条件。

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
一个来自 [BP_COND_STYLE](../../../extensibility/debugger/reference/bp-cond-style.md) 枚举的值，该值描述此断点条件的样式。

`bstrContext`\
断点的位置。

`bstrCondition`\
断点的触发条件。

`nRadix`\
用于评估任何数值信息的基数。

## <a name="remarks"></a>备注
此结构是 BP_REQUEST_INFO[和](../../../extensibility/debugger/reference/bp-request-info.md)BP_REQUEST_INFO2[的成员。](../../../extensibility/debugger/reference/bp-request-info2.md)

此结构也作为参数传递给 [SetCondition](../../../extensibility/debugger/reference/idebugboundbreakpoint2-setcondition.md) 和 [SetCondition](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-setcondition.md) 方法。

## <a name="requirements"></a>要求
标头：msdbg.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)
- [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)
- [SetCondition](../../../extensibility/debugger/reference/idebugboundbreakpoint2-setcondition.md)
- [SetCondition](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-setcondition.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [BP_COND_STYLE](../../../extensibility/debugger/reference/bp-cond-style.md)

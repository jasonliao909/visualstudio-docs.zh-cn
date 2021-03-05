---
description: 描述触发条件断点的计数和条件。
title: BP_PASSCOUNT |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_PASSCOUNT
helpviewer_keywords:
- BP_PASSCOUNT structure
ms.assetid: 791ac175-b897-4c70-873e-240da7e0ac89
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9c1e44ede0f39b3d1b33967311365508da6a701d
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102144151"
---
# <a name="bp_passcount"></a>BP_PASSCOUNT
描述触发条件断点的计数和条件。

## <a name="syntax"></a>语法

```cpp
typedef struct _BP_PASSCOUNT {
    DWORD              dwPassCount;
    BP_PASSCOUNT_STYLE stylePassCount;
} BP_PASSCOUNT;
```

```csharp
public struct BP_PASSCOUNT {
    public uint dwPassCount;
    public uint stylePassCount;
};
```

## <a name="members"></a>成员
`dwPassCount`\
在引发断点之前传递该断点的次数。

`stylePassCount`\
[BP_PASSCOUNT_STYLE](../../../extensibility/debugger/reference/bp-passcount-style.md)枚举中的一个值，该值指定断点传递计数的样式。

## <a name="remarks"></a>备注
此结构是 [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md) 结构的成员。

此结构也作为参数传递给[SetPassCount](../../../extensibility/debugger/reference/idebugboundbreakpoint2-setpasscount.md) 和[SetPassCount](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-setpasscount.md) 方法。

## <a name="requirements"></a>要求
标头： msdbg

命名空间： VisualStudio

程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)
- [SetPassCount](../../../extensibility/debugger/reference/idebugboundbreakpoint2-setpasscount.md)
- [SetPassCount](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-setpasscount.md)
- [BP_PASSCOUNT_STYLE](../../../extensibility/debugger/reference/bp-passcount-style.md)

---
title: BP_UNBOUND_REASON |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_UNBOUND_REASON
helpviewer_keywords:
- BP_UNBOUND_REASON enumeration
ms.assetid: 939b6f9c-113b-471d-9f30-b03871af6285
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c4750b4d1a9c1f972c0445dfcf3ea2f4fa5be328
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99842650"
---
# <a name="bp_unbound_reason"></a>BP_UNBOUND_REASON
提供取消绑定断点的原因。

## <a name="syntax"></a>语法

```cpp
enum enum_BP_UNBOUND_REASON {
    BPUR_UNKNOWN           = 0x0000,
    BPUR_CODE_UNLOADED     = 0x0002,
    BPUR_BREAKPOINT_REBIND = 0x0003,
    BPUR_BREAKPOINT_ERROR  = 0x0004
};
typedef DWORD BP_UNBOUND_REASON;
```

```csharp
public enum enum_BP_UNBOUND_REASON {
    BPUR_UNKNOWN           = 0x0000,
    BPUR_CODE_UNLOADED     = 0x0002,
    BPUR_BREAKPOINT_REBIND = 0x0003,
    BPUR_BREAKPOINT_ERROR  = 0x0004
};
```

## <a name="fields"></a>字段
`BPUR_UNKNOWN`\
原因未知。

`BPUR_CODE_UNLOADED`\
包含断点的代码已卸载。

`BPUR_BREAKPOINT_REBIND`\
断点已重新绑定到另一个位置。 当断点移动时，或者当断点绑定到的文件的路径不再有效时，可能会发生这种情况。

`BPUR_ BREAKPOINT_ERROR`\
确定断点在绑定后出错。 这适用于其条件不再有效的托管断点。

## <a name="remarks"></a>备注
由 [GetReason](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2-getreason.md) 方法返回。

## <a name="requirements"></a>要求
标头： msdbg

命名空间： VisualStudio

程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetReason](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2-getreason.md)

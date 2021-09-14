---
description: 给出断点未绑定的原因。
title: BP_UNBOUND_REASON |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_UNBOUND_REASON
helpviewer_keywords:
- BP_UNBOUND_REASON enumeration
ms.assetid: 939b6f9c-113b-471d-9f30-b03871af6285
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 96492dbc68869ab63b1da14c6a1c7d8b08cc7a66
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602497"
---
# <a name="bp_unbound_reason"></a>BP_UNBOUND_REASON
给出断点未绑定的原因。

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
断点已重新出现到其他位置。 当断点移动或断点绑定到具有不再有效的路径的文件时，在"编辑并继续"操作后可能会发生这种情况。

`BPUR_ BREAKPOINT_ERROR`\
断点在绑定后被确定为出错。 这种情况发生在其条件不再有效的托管断点上。

## <a name="remarks"></a>备注
由 [GetReason 方法](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2-getreason.md) 返回。

## <a name="requirements"></a>要求
标头：msdbg.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetReason](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2-getreason.md)

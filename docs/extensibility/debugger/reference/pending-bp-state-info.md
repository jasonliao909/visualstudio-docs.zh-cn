---
description: 包含有关已准备好绑定到代码位置的断点的状态的信息。
title: PENDING_BP_STATE_INFO |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PENDING_BP_STATE_INFO
helpviewer_keywords:
- PENDING_BP_STATE_INFO structure
ms.assetid: 4d73ceff-43f9-4e95-8dba-88e1fab2def3
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 16d73973b9d6170023f605dd42e7d451b32fd6bb
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122042772"
---
# <a name="pending_bp_state_info"></a>PENDING_BP_STATE_INFO
包含有关已准备好绑定到代码位置的断点的状态的信息。

## <a name="syntax"></a>语法

```cpp
typedef struct _tagPENDING_BP_STATE_INFO { 
   PENDING_BP_STATE       state;
   PENDING_BP_STATE_FLAGS flags;
} PENDING_BP_STATE_INFO;
```

```csharp
public struct PENDING_BP_STATE_INFO { 
   public uint state;
   public uint flags;
};
```

## <a name="members"></a>成员
 `state`\
 指定挂起 [断PENDING_BP_STATE](../../../extensibility/debugger/reference/pending-bp-state.md) 状态的值。

 `flags`\
 来自 PENDING_BP_STATE_FLAGS [标志的组合](../../../extensibility/debugger/reference/pending-bp-state-flags.md) ，用于指定断点是否虚拟化。

## <a name="remarks"></a>备注
 此结构将传递到 [GetState](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getstate.md) 方法中填充它。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetState](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getstate.md)
- [PENDING_BP_STATE](../../../extensibility/debugger/reference/pending-bp-state.md)
- [PENDING_BP_STATE_FLAGS](../../../extensibility/debugger/reference/pending-bp-state-flags.md)

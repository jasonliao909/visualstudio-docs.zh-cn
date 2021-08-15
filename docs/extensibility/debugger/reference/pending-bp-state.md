---
description: 指定挂起断点的状态 (尚未绑定到该断点的) 。
title: PENDING_BP_STATE |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PENDING_BP_STATE
helpviewer_keywords:
- PENDING_BP_STATE enumeration
ms.assetid: ac04ad72-fa92-4a15-ade2-0d0bbbadfc7f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f6079a227be831f44476a233849b735fadfc9e82564ea39af52637343caaa28e
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121448580"
---
# <a name="pending_bp_state"></a>PENDING_BP_STATE
指定挂起断点的状态 (尚未绑定到该断点的) 。

## <a name="syntax"></a>语法

```cpp
enum enum_PENDING_BP_STATE { 
   PBPS_NONE     = 0x0000,
   PBPS_DELETED  = 0x0001,
   PBPS_DISABLED = 0x0002,
   PBPS_ENABLED  = 0x0003
};
typedef DWORD PENDING_BP_STATE;
```

```csharp
public enum enum_PENDING_BP_STATE { 
   PBPS_NONE     = 0x0000,
   PBPS_DELETED  = 0x0001,
   PBPS_DISABLED = 0x0002,
   PBPS_ENABLED  = 0x0003
};
```

## <a name="fields"></a>字段
 `PBPS_NONE`\
 零的占位符。 永远不会返回此值。

 `PBPS_DELETED`\
 指示挂起的断点已删除。

 `PBPS_DISABLED`\
 指示已禁用挂起断点。

 `PBPS_ENABLED`\
 指示已启用挂起断点。

## <a name="remarks"></a>备注
 使用 作为 `state` 结构PENDING_BP_STATE_INFO成员[](../../../extensibility/debugger/reference/pending-bp-state-info.md)。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [PENDING_BP_STATE_INFO](../../../extensibility/debugger/reference/pending-bp-state-info.md)

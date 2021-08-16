---
description: 指定是否存在绑定断点，并指定是否启用该断点。
title: BP_STATE |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_STATE
helpviewer_keywords:
- BP_STATE enumeration
ms.assetid: 08aa6a3f-3e5f-4c83-8eca-7b7b5f8e208d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0d8ff002c7f17abe0f33900fb7f798405dde78ee755965bfe2d24713eaea33d6
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121434446"
---
# <a name="bp_state"></a>BP_STATE
指定是否存在绑定断点，并指定是否启用该断点。

## <a name="syntax"></a>语法

```cpp
enum enum_BP_STATE {
    BPS_NONE     = 0x0000,
    BPS_DELETED  = 0x0001,
    BPS_DISABLED = 0x0002,
    BPS_ENABLED  = 0x0003
};
typedef DWORD BP_STATE;
```

```csharp
public enum enum_BP_STATE {
    BPS_NONE     = 0x0000,
    BPS_DELETED  = 0x0001,
    BPS_DISABLED = 0x0002,
    BPS_ENABLED  = 0x0003
};
```

## <a name="fields"></a>字段
`BPS_NONE`\
指定不存在断点。

`BPS_DELETED`\
指定已删除断点。

`BPS_DISABLED`\
指定禁用断点。

`BPS_ENABLED`\
指定启用断点。

## <a name="remarks"></a>备注
从 [GetState 方法](../../../extensibility/debugger/reference/idebugboundbreakpoint2-getstate.md) 返回。

## <a name="requirements"></a>要求
标头：msdbg.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetState](../../../extensibility/debugger/reference/idebugboundbreakpoint2-getstate.md)

---
description: 附加到关联的程序，或将附加进程延迟到 Attach 方法。
title: IDebugProgramNodeAttach2：：OnAttach |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNodeAttach2::OnAttach
helpviewer_keywords:
- IDebugProgramNodeAttach2::OnAttach
ms.assetid: 5fe52761-a508-4ab5-abdb-334fb6590334
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0650005ca04b01265f6e675db9426856389235caadfc36bb457280d7fbba1fb6
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121402631"
---
# <a name="idebugprogramnodeattach2onattach"></a>IDebugProgramNodeAttach2::OnAttach
附加到关联的程序，或将附加进程延迟到 [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) 方法。

## <a name="syntax"></a>语法

```cpp
HRESULT OnAttach(
   [in] REFGUID guidProgramId
);
```

```csharp
int OnAttach(
   ref Guid guidProgramId
};
```

## <a name="parameters"></a>参数
`guidProgramId`\
[in] `GUID` ，以分配给关联的程序。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果 `S_FALSE` 不应 [调用 Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) 方法，则返回 。 否则，返回错误代码。

## <a name="remarks"></a>备注
 在调用 Attach 方法之前，在 [附加过程中](../../../extensibility/debugger/reference/idebugengine2-attach.md) 调用此方法。 方法可以执行附加进程本身 (在这种情况下，此方法返回) 或将附加进程延迟到方法 (方法返回 `OnAttach` `S_FALSE` `IDebugEngine2::Attach` `OnAttach` `S_OK`) 。 在任一事件中， 方法都可以将正在 `OnAttach` `GUID` 调试的程序的 设置为给定的 `GUID` 。

## <a name="see-also"></a>另请参阅
- [IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md)
- [附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)

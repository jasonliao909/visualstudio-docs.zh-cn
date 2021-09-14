---
description: 通知调试引擎 (DE) 指定的程序已以非典型方式终止，并且 DE 应清除对该程序的所有引用并发送程序销毁事件。
title: IDebugEngine2：:D estroyProgram |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::DestroyProgram
helpviewer_keywords:
- IDebugEngine2::DestroyProgram
ms.assetid: 0c9e2698-c70f-4770-a7bb-39650e9c3a1f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 49256244f5839341c66f5a308505c18c0737eace
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665420"
---
# <a name="idebugengine2destroyprogram"></a>IDebugEngine2::DestroyProgram
通知调试引擎 (DE) 指定的程序已以非典型方式终止，并且 DE 应清除对该程序的所有引用并发送程序销毁事件。

## <a name="syntax"></a>语法

```cpp
HRESULT DestroyProgram( 
   IDebugProgram2* pProgram
);
```

```cpp
int DestroyProgram( 
   IDebugProgram2 pProgram
);
```

## <a name="parameters"></a>parameters
`pProgram`\
[in]一 [个 IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) 对象，表示已以非典型方式终止的程序。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 调用此方法后，DE 随后会向会话调试管理器发送 [IDebugProgramDestroyEvent2](../../../extensibility/debugger/reference/idebugprogramdestroyevent2.md) 事件 (SDM) 。

 如果 DE 与 (在同一进程中 `E_NOTIMPL`) ，则此方法不会实现。 只有当 DE 与 SDM 在同一进程中运行时，才实现此方法。

## <a name="see-also"></a>另请参阅
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [IDebugProgramDestroyEvent2](../../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)

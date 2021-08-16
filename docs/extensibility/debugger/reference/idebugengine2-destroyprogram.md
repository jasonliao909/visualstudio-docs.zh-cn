---
description: 通知调试引擎 (DE) 指定的程序已被异常终止，并应清除对程序的所有引用并发送程序销毁事件。
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
ms.openlocfilehash: a237732b67182225722502c3f35e89a630cba6e1e68e9a5b891e299580dc1e73
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121342266"
---
# <a name="idebugengine2destroyprogram"></a>IDebugEngine2::DestroyProgram
通知调试引擎 (DE) 指定的程序已被异常终止，并应清除对程序的所有引用并发送程序销毁事件。

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

## <a name="parameters"></a>参数
`pProgram`\
中一个 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) 对象，该对象表示已被异常终止的程序。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 在调用此方法之后，以后再将 [IDebugProgramDestroyEvent2](../../../extensibility/debugger/reference/idebugprogramdestroyevent2.md) 事件发送回会话调试管理器 (SDM) 。

 此方法未实现 (`E_NOTIMPL` 如果取消操作与正在调试的程序在同一进程中运行，将返回) 。 仅当在与 SDM 相同的进程中运行时，才实现此方法。

## <a name="see-also"></a>另请参阅
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [IDebugProgramDestroyEvent2](../../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)

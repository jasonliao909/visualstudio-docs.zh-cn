---
description: 由调试引擎 (DE) 启动和终止程序。
title: IDebugEngineLaunch2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngineLaunch2
helpviewer_keywords:
- IDebugEngineLaunch2 interface
ms.assetid: 5eaf2ad8-3fbf-446e-b48b-5327ad3f5255
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 17f75a0a127b45f0fa1bc55c1399592e35cc1383
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122089168"
---
# <a name="idebugenginelaunch2"></a>IDebugEngineLaunch2
由调试引擎 (DE) 启动和终止程序。

## <a name="syntax"></a>语法

```
IDebugEngineLaunch2 : IDebugEngine2
```

## <a name="notes-for-implementers"></a>实现者说明
 如果自定义 DE 对启动无法完全由自定义端口处理的进程有特殊要求，则此接口由自定义 DE 实现。 当 DE 是解释器一部分并且正在调试的进程是脚本时，通常就是这种情况：首先需要启动解释器，然后加载并启动脚本。 端口可以启动解释器，但脚本可能需要特殊处理 (DE 在解释器中) 。 只有在启动自定义端口无法处理的程序有唯一要求时，才实现此接口。

## <a name="notes-for-callers"></a>调用方说明
 如果 SDM 可以使用 QueryInter) face) [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md) 接口获取此接口，则此接口由 SDM (会话调试管理器 (调用。 如果可以获取此接口，则 SDM 知道 DE 具有特殊要求，并调用此接口来启动程序，而不是让端口启动程序。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法 `IDebugEngineLaunch2` 。

|方法|说明|
|------------|-----------------|
|[LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)|通过 DE 启动进程。|
|[ResumeProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-resumeprocess.md)|恢复进程执行。|
|[CanTerminateProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-canterminateprocess.md)|确定是否可以终止进程。|
|[TerminateProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-terminateprocess.md)|终止进程。|

## <a name="requirements"></a>要求
 标头：Msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)

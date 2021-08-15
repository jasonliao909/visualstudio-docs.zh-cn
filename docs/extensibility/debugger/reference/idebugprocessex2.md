---
description: 此接口允许会话调试管理器 (SDM) 通知进程正在附加到进程或正在从进程中分离。
title: IDebugProcessEx2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcessEx2
helpviewer_keywords:
- IDebugProcessEx2 interface
ms.assetid: 44e309ba-1d6f-499b-aa7e-9b34858a6d57
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 11f2c1cbefa4100ac9b025fbdcc1fed119531434ea9dbec033b8233a2ad19730
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121338899"
---
# <a name="idebugprocessex2"></a>IDebugProcessEx2
此接口允许会话调试管理器 (SDM) 通知进程正在附加到进程或正在从进程中分离。

## <a name="syntax"></a>语法

```
IDebugProcessEx2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 自定义端口供应商在 [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md) 接口的同一对象上实现此接口，以便：

- 支持跟踪连接到进程的会话

- 支持跨多个调试引擎自动附加

  自定义端口供应商可以选择实现此接口。

## <a name="notes-for-callers"></a>调用方说明

- SDM 在接口上调用 [QueryInterface](/cpp/atl/queryinterface) `IDebugProcess2` 以获取此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法 `IDebugProcessEx2` 。

|方法|说明|
|------------|-----------------|
|[附加](../../../extensibility/debugger/reference/idebugprocessex2-attach.md)|通知进程会话现在正在调试进程。|
|[分离](../../../extensibility/debugger/reference/idebugprocessex2-detach.md)|通知进程会话不再调试进程。|
|[AddImplicitProgramNodes](../../../extensibility/debugger/reference/idebugprocessex2-addimplicitprogramnodes.md)|为调试引擎列表添加程序节点。|

## <a name="remarks"></a>备注
 此接口在 SDM 和进程之间是私有的。

## <a name="requirements"></a>要求
 标头：Portpriv.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)

---
description: 此接口使会话调试管理器 (SDM) 通知它附加到进程或从进程分离的进程。
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
ms.workload:
- vssdk
ms.openlocfilehash: 1bd22a779cd0a474b5df03d2315402dbe1a25239
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105081511"
---
# <a name="idebugprocessex2"></a>IDebugProcessEx2
此接口使会话调试管理器 (SDM) 通知它附加到进程或从进程分离的进程。

## <a name="syntax"></a>语法

```
IDebugProcessEx2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 自定义端口供应商在与 [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md) 接口相同的对象上实现此接口，以便：

- 支持跟踪连接到进程的会话

- 支持跨多个调试引擎自动附加

  自定义端口供应商可以在选择的情况下实现此接口。

## <a name="notes-for-callers"></a>调用方说明

- SDM 在接口[](/cpp/atl/queryinterface)上调用 QueryInterface `IDebugProcess2` 以获取此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法 `IDebugProcessEx2` 。

|方法|说明|
|------------|-----------------|
|[附加](../../../extensibility/debugger/reference/idebugprocessex2-attach.md)|通知进程会话正在调试该进程。|
|[分离](../../../extensibility/debugger/reference/idebugprocessex2-detach.md)|通知进程：会话不再调试该进程。|
|[AddImplicitProgramNodes](../../../extensibility/debugger/reference/idebugprocessex2-addimplicitprogramnodes.md)|为调试引擎列表添加程序节点。|

## <a name="remarks"></a>备注
 此接口在 SDM 和进程之间是私有的。

## <a name="requirements"></a>要求
 标头： Portpriv

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)

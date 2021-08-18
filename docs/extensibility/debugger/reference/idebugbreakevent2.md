---
description: 此接口告知会话调试管理器 (SDM) 异步中断已成功完成。
title: IDebugBreakEvent2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakEvent2
helpviewer_keywords:
- IDebugBreakEvent2 interface
ms.assetid: 57dfdbc2-4e68-4dbf-9579-006cd6fb1c62
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 1816d2a6c53c4a1840f6511676dafff7a3710394
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122119757"
---
# <a name="idebugbreakevent2"></a>IDebugBreakEvent2
此接口告知会话调试管理器 (SDM) 异步中断已成功完成。

## <a name="syntax"></a>语法

```
IDebugBreakEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 DE 实现此接口以支持程序中的用户中断。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)接口必须在与此接口相同的对象上实现 (SDM 使用[QueryInterface](/cpp/atl/queryinterface)访问接口 `IDebugEvent2`) 。

## <a name="notes-for-callers"></a>调用方说明
 当用户请求暂停正在调试的程序时，SDM 调用[CauseBreak。](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md) 成功暂停程序后，DE 将发送 `IDebugBreakEvent2` 事件。 此事件是通过使用 SDM 在附加到正在调试的程序时提供的 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) 回调函数发送的。

## <a name="remarks"></a>备注
 例如，用户可以选择"调试"菜单上的"全部中断"命令，以中断运行无限循环的程序。 SDM 通过调用 [CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)告知程序停止。 DE 在 `IDebugBreakEvent2` 程序最终停止时发送。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)

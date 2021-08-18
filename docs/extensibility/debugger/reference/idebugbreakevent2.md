---
description: 此接口告诉会话调试管理器 (SDM) 异步中断已成功完成。
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
ms.openlocfilehash: b07b7203f8ce3d557b0bbb2d4c1ca410e481aec67555da5f21f0563702e71656
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121293035"
---
# <a name="idebugbreakevent2"></a>IDebugBreakEvent2
此接口告诉会话调试管理器 (SDM) 异步中断已成功完成。

## <a name="syntax"></a>语法

```
IDebugBreakEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 DE 实现此接口以支持程序中的用户中断。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)接口必须在与此接口相同的对象上实现 (SDM 使用[QueryInterface](/cpp/atl/queryinterface)访问 `IDebugEvent2` 接口) 。

## <a name="notes-for-callers"></a>调用方说明
 当用户请求暂停正在调试的程序时，SDM 将调用 [CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md) 。 如果程序成功暂停，则取消发送 `IDebugBreakEvent2` 事件。 此事件在附加到正在调试的程序时，使用 SDM 提供的 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) 回调函数发送。

## <a name="remarks"></a>备注
 例如，用户可以选择 "**调试**" 菜单上的 "**全部中断**" 命令，以中断正在运行无限循环的程序。 SDM 通过调用 [CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)来通知程序停止。 `IDebugBreakEvent2`当程序最终停止时，会发送 DE。

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)

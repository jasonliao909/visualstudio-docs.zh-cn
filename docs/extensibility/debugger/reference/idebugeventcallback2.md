---
description: 此接口由 DE (引擎) ，以将调试事件发送到 SDM (会话) 。
title: IDebugEventCallback2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEventCallback2
helpviewer_keywords:
- IDebugEventCallback2
ms.assetid: 2c935ee0-2e22-4be0-a852-73736f33c8c9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: e769f4c960d49cb66f92a72f4a402c81c8f54b7f25f041251680138c84f4f07b
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121292632"
---
# <a name="idebugeventcallback2"></a>IDebugEventCallback2
此接口由 DE (引擎) ，以将调试事件发送到 SDM (会话) 。

## <a name="syntax"></a>语法

```
IDebugEventCallback2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] 实现此接口以从调试引擎接收事件。

## <a name="notes-for-callers"></a>调用方说明
 当 SDM 调用 Attach、Attach 或[LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)时，调试引擎通常会接收此接口。 [](../../../extensibility/debugger/reference/idebugprogram2-attach.md) [](../../../extensibility/debugger/reference/idebugengine2-attach.md) 调试引擎通过调用事件 将事件发送到 SDM。 [](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法 `IDebugEventCallback2` 。

|方法|说明|
|------------|-----------------|
|[事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)|将调试事件的通知发送到 SDM。|

## <a name="remarks"></a>备注
 尽管 [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) 和 [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) 指定它们接受接口，但这不是这种情况，并且接口指针 `IDebugEventCallback2` 将始终为 null 值。 相反，调试引擎必须使用在调用 `IDebugEventCallback2` [Attach、Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)或[](../../../extensibility/debugger/reference/idebugprogram2-attach.md)[LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)时收到的 接口。

 如果包在托管代码中实现 [IDebugEventCallback，](../../../extensibility/debugger/reference/idebugeventcallback2.md) 强烈建议在传递给事件 的各种接口 <xref:System.Runtime.InteropServices.Marshal.ReleaseComObject%2A> 上 [调用](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)
- [附加](../../../extensibility/debugger/reference/idebugprogram2-attach.md)
- [附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)

---
description: 此方法发送的事件表示在端口上创建和销毁进程和程序。
title: IDebugPortEvents2：：Event |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortEvents2::Event
helpviewer_keywords:
- IDebugPortEvents2::Event
ms.assetid: 5cc813f7-04a1-4462-9ea7-fbddcf0e0143
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 30731bddcde55f34cf3e568434909bcd68f728735d44b757ec0da898f31189d6
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121323464"
---
# <a name="idebugportevents2event"></a>IDebugPortEvents2::Event
此方法发送的事件表示在端口上创建和销毁进程和程序。

## <a name="syntax"></a>语法

```cpp
HRESULT Event(
   IDebugCoreServer2* pServer,
   IDebugPort2*       pPort,
   IDebugProcess2*    pProcess,
   IDebugProgram2*    pProgram,
   IDebugEvent2*      pEvent,
   REFIID             riidEvent
);
```

```csharp
int Event(
   IDebugCoreServer2 pServer,
   IDebugPort2       pPort,
   IDebugProcess2    pProcess,
   IDebugProgram2    pProgram,
   IDebugEvent2      pEvent,
   ref Guid          riidEvent
);
```

## <a name="parameters"></a>参数
`pMachine`\
[in]一 [个 IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md) 对象，该对象表示调试服务器 (发生事件) 实例都有 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] 一个。

`pPort`\
[in]一 [个 IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) 对象，表示事件发生的端口。

`pProcess`\
[in]一 [个 IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md) 对象，表示事件发生的进程。

`pProgram`\
[in]一 [个 IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) 对象，表示事件发生的程序。

`pEvent`\
[in]标识 [事件的 IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) 对象。 可能的事件如下所示：

- [IDebugProcessCreateEvent2](../../../extensibility/debugger/reference/idebugprocesscreateevent2.md)

- [IDebugProcessDestroyEvent2](../../../extensibility/debugger/reference/idebugprocessdestroyevent2.md)

- [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)

- [IDebugProgramDestroyEvent2](../../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)

`riidEvent`\
[in]事件的 GUID。 由于事件在调用此方法之前被强制转换到 [IDebugEvent2，](../../../extensibility/debugger/reference/idebugevent2.md) 因此此标识符可以更轻松地确定要发送的事件。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md)
- [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)

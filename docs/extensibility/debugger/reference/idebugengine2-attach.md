---
description: 将调试引擎 (DE) 程序或程序。
title: IDebugEngine2：：Attach |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::Attach
helpviewer_keywords:
- IDebugEngine2::Attach
ms.assetid: 173dcbda-5019-4c5e-bca9-a071838b5739
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f733dc1ad1ee3e87c5d28721a308c22f3fc2e0fb
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122119160"
---
# <a name="idebugengine2attach"></a>IDebugEngine2::Attach
将调试引擎 (DE) 程序或程序。 由会话调试管理器 (SDM) DE 在进程内运行 SDM 时调用。

## <a name="syntax"></a>语法

```cpp
HRESULT Attach( 
   IDebugProgram2**      pProgram,
   IDebugProgramNode2**  rgpProgramNodes,
   DWORD                 celtPrograms,
   IDebugEventCallback2* pCallback,
   ATTACH_REASON         dwReason
);
```

```csharp
int Attach( 
   IDebugProgram2[]     pProgram,
   IDebugProgramNode2[] rgpProgramNodes,
   uint                 celtPrograms,
   IDebugEventCallback2 pCallback,
   Enum_ATTACH_REASON   dwReason
);
```

## <a name="parameters"></a>参数
`pProgram`\
[in] [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) 对象的数组，这些对象表示要附加到的程序。 这些是端口程序。

`rgpProgramNodes`\
[in] [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) 对象的数组，这些对象表示程序节点，每个程序各有一个。 此数组中的程序节点表示与 中的程序相同的程序 `pProgram` 。 提供程序节点，以便 DE 能够标识要附加到的程序。

`celtPrograms`\
[in]和 数组中的程序和/或 `pProgram` 程序 `rgpProgramNodes` 节点数。

`pCallback`\
[in]用于将调试事件发送到 SDM 的 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) 对象。

`dwReason`\
[in]一个来自 [ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md) 枚举的值，该值指定附加这些程序的原因。 有关详细信息，请参阅“备注”部分。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 附加到程序有三个原因，如下所示：

- `ATTACH_REASON_LAUNCH` 指示 DE 正在附加到程序，因为用户启动了包含该程序的进程。

- `ATTACH_REASON_USER` 指示用户已显式请求 DE 附加到程序 (或包含程序组) 。

- `ATTACH_REASON_AUTO` 指示 DE 正在附加到特定程序，因为它已在调试特定进程中的其他程序。 这也称为自动附加。

  调用此方法时，DE 需要按顺序发送这些事件：

1. 如果尚未为调试引擎实例的特定实例发送[IDebugEngineCreateEvent (2，) ](../../../extensibility/debugger/reference/idebugenginecreateevent2.md)

2. [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)

3. [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md)

   此外，如果附加的原因是 `ATTACH_REASON_LAUNCH` ，DE 需要发送 [IDebugEntryPointEvent2](../../../extensibility/debugger/reference/idebugentrypointevent2.md) 事件。

   DE 获取与正在调试的程序相对应的 [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) 对象后，可以查询该对象以寻找任何专用接口。

   在调用 或 给定的数组中的程序节点的方法之前，应在表示程序节点的接口上启用模拟（ `pProgram` `rgpProgramNodes` `IDebugProgram2` 如果需要）。 但是，通常不需要执行此步骤。 有关详细信息，请参阅 [安全问题](../../../extensibility/debugger/security-issues.md)。

## <a name="see-also"></a>请参阅
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md)
- [IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md)
- [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)
- [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md)
- [IDebugEntryPointEvent2](../../../extensibility/debugger/reference/idebugentrypointevent2.md)

---
title: IDebugProgramNode2：：Attach_V7 |Microsoft Docs
description: 此接口方法是 2005 年 5 月之前使用的已弃用的旧附加Visual Studio方法。
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNode2::Attach
helpviewer_keywords:
- IDebugProgramNode2::Attach_V7
- IDebugProgramNode2::Attach
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fbad29417b7c53284c0a00281f9c702c8bb5e342e44bcd84b6106799e9d7560f
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121261627"
---
# <a name="idebugprogramnode2attach_v7"></a>IDebugProgramNode2::Attach_V7

> [!Note]
> 废弃。 请勿使用。

## <a name="syntax"></a>语法

```cpp
HRESULT Attach_V7 (
   IDebugProgram2*       pMDMProgram,
   IDebugEventCallback2* pCallback,
   DWORD                 dwReason
);
```

```csharp
int Attach_V7 (
   IDebugProgram2       pMDMProgram,
   IDebugEventCallback2 pCallback,
   uint                 dwReason
);
```

## <a name="parameters"></a>参数

`pMDMProgram`\
[in] [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) 接口，表示要附加到的程序。

`pCallback`\
[in]用于将调试事件发送到 SDM 的 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) 接口。

`dwReason`\
[in]指定附加 [ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md) 的枚举中的值。

## <a name="return-value"></a>返回值

实现应始终返回 `E_NOTIMPL` 。

## <a name="remarks"></a>备注

> [!WARNING]
> 从 Visual Studio 2005 起，此方法不再使用，应始终返回 `E_NOTIMPL` 。 如果程序节点需要指示无法附加到或程序节点只是设置程序 ，请参阅 [IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md) 接口，了解替代方法 `GUID` 。 否则，请实现 [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) 方法。

## <a name="prior-to-visual-studio-2005"></a>2005 Visual Studio之前

只有当 DE 在正在调试的程序的地址空间中运行时，才需要实现此方法。 否则，此方法应返回 `S_FALSE` 。

调用此方法时，DE 必须发送 [IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md) 事件对象（如果尚未为此 [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md) 接口实例发送该对象）以及 [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md) 和 [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md) 事件对象。 然后，如果 参数为 ，则发送 [IDebugEntryPointEvent2](../../../extensibility/debugger/reference/idebugentrypointevent2.md) `dwReason` 事件对象 `ATTACH_REASON_LAUNCH` 。

DE 必须对[IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)事件对象提供的[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)对象调用[GetProgramId](../../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)方法，并且必须将该程序的 GUID 存储在 DE 实现的对象的实例数据 `IDebugProgram2` 中。

## <a name="see-also"></a>另请参阅

- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
- [IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md)
- [附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md)
- [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)
- [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md)
- [IDebugEntryPointEvent2](../../../extensibility/debugger/reference/idebugentrypointevent2.md)
- [ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md)

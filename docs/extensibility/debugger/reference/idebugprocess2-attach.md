---
description: 将 (SDM) 的会话调试管理器附加到进程。
title: IDebugProcess2：： Attach |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::Attach
helpviewer_keywords:
- IDebugProcess2::Attach
ms.assetid: 40d78417-fde2-45c3-96c9-16e06bd9008d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2ebada428727dd356584de0a50cf31d3e407e7515295bede2d0957717054eaed
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121416516"
---
# <a name="idebugprocess2attach"></a>IDebugProcess2::Attach
将 (SDM) 的会话调试管理器附加到进程。

## <a name="syntax"></a>语法

```cpp
HRESULT Attach( 
   IDebugEventCallback2* pCallback,
   GUID*                 rgguidSpecificEngines,
   DWORD                 celtSpecificEngines,
   HRESULT*              rghrEngineAttach
);
```

```csharp
int Attach( 
   IDebugEventCallback2 pCallback,
   Guid[]               rgguidSpecificEngines,
   uint                 celtSpecificEngines,
   int[]                rghrEngineAttach
);
```

## <a name="parameters"></a>参数
`pCallback`\
中用于调试事件通知的 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) 对象。

`rgguidSpecificEngines`\
中用于调试进程中运行的程序的调试引擎的 Guid 数组。 此参数可以为 null 值。 有关详细信息，请参阅“备注”。

`celtSpecificEngines`\
中数组中的调试引擎数 `rgguidSpecificEngines` 和 `rghrEngineAttach` 数组大小。

`rghrEngineAttach`\
[in，out]由调试引擎返回的 HRESULT 代码的数组。 此数组的大小是在参数中指定的 `celtSpecificEngines` 。 每个代码通常是 `S_OK` 或 `S_ATTACH_DEFERRED` 。 后一种方式表明 DE 当前未附加到任何程序。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。 下表显示了其他可能的值。

|值|说明|
|-----------|-----------------|
|`E_ATTACH_DEBUGGER_ALREADY_ATTACHED`|指定的进程已附加到调试器。|
|`E_ATTACH_DEBUGGEE_PROCESS_SECURITY_VIOLATION`|附加过程中发生了安全冲突。|
|`E_ATTACH_CANNOT_ATTACH_TO_DESKTOP`|不能将桌面进程附加到调试器。|

## <a name="remarks"></a>备注
 附加到进程会将 SDM 附加到该进程中运行的所有程序，调试引擎可以调试该进程中 (DE) 在数组中指定的程序 `rgguidSpecificEngines` 。 将 `rgguidSpecificEngines` 参数设置为 null 值，或将该参数添加到 `GUID_NULL` 要附加到进程中的所有程序的数组中。

 进程中发生的所有调试事件都将发送到给定的 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) 对象。 `IDebugEventCallback2`当 SDM 调用此方法时，将提供此对象。

## <a name="see-also"></a>请参阅
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)

---
description: 将会话调试管理器 (SDM) 进程。
title: IDebugProcess2：：Attach |Microsoft Docs
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
将会话调试管理器 (SDM) 进程。

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
[in]用于 [调试事件通知的 IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) 对象。

`rgguidSpecificEngines`\
[in]调试引擎的 GUID 数组，用于调试进程中运行的程序。 此参数可以是 null 值。 有关详细信息，请参阅“备注”。

`celtSpecificEngines`\
[in]数组中的调试引擎 `rgguidSpecificEngines` 数和数组 `rghrEngineAttach` 的大小。

`rghrEngineAttach`\
[in， out]调试引擎返回的 HRESULT 代码数组。 此数组的大小在 参数中 `celtSpecificEngines` 指定。 每个代码通常是 或 `S_OK` `S_ATTACH_DEFERRED` 。 后者指示 DE 当前未附加到任何程序。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。 下表显示了其他可能的值。

|值|说明|
|-----------|-----------------|
|`E_ATTACH_DEBUGGER_ALREADY_ATTACHED`|指定的进程已附加到调试器。|
|`E_ATTACH_DEBUGGEE_PROCESS_SECURITY_VIOLATION`|附加过程中发生了安全冲突。|
|`E_ATTACH_CANNOT_ATTACH_TO_DESKTOP`|桌面进程无法附加到调试器。|

## <a name="remarks"></a>备注
 附加到进程将 SDM 附加到进程中运行的所有程序，这些程序可通过调试引擎调试 (在) 中指定的 DE `rgguidSpecificEngines` 命令。 将 `rgguidSpecificEngines` 参数设置为 null 值，或在数组中包括 `GUID_NULL` 以附加到进程中的所有程序。

 进程中发生的所有调试事件都发送到给定的 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) 对象。 SDM `IDebugEventCallback2` 调用此方法时提供此对象。

## <a name="see-also"></a>另请参阅
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)

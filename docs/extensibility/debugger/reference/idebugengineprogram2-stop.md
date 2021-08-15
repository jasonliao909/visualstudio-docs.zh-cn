---
description: 停止此程序中运行的所有线程。
title: IDebugEngineProgram2：：Stop |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngineProgram2::Stop
helpviewer_keywords:
- IDebugEngineProgram2::Stop
ms.assetid: 6e1c3d56-fb67-4a5b-80f9-8ee5131972bf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 308e3b59c5f1a542c2e0b3e10c573c5990d0f85acf2f6b18aa71af9cd84ccd70
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121342214"
---
# <a name="idebugengineprogram2stop"></a>IDebugEngineProgram2::Stop
停止此程序中运行的所有线程。

## <a name="syntax"></a>语法

```cpp
HRESULT Stop( 
   void 
);
```

```csharp
int Stop();
```

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 在多程序环境中调试此程序时，将调用此方法。 收到来自其他程序的停止事件时，将对此程序调用此方法。 此方法的实现应该是异步的;也就是说，并非所有线程都应在此方法返回之前停止。 此方法的实现可能与在此程序上调用 [CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md) 方法一样简单。

 程序停止时，实现者应发送[IDebugStopCompleteEvent2。](../../../extensibility/debugger/reference/idebugstopcompleteevent2.md)

## <a name="see-also"></a>另请参阅
- [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)
- [CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)

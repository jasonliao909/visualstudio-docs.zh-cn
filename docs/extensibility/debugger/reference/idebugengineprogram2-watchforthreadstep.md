---
description: 监视执行 (或停止监视) 线程上发生的执行事件。
title: IDebugEngineProgram2：：WatchForThreadStep |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngineProgram2::WatchForThreadStep
helpviewer_keywords:
- IDebugEngineProgram2::WatchForThreadStep
ms.assetid: b70922a3-1313-409a-b3b7-50c7cd13e394
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a6acb6dfe32adba3dccd30e38e2bb3b18d4dc5d2c190a966c05beb34df7395a3
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121389990"
---
# <a name="idebugengineprogram2watchforthreadstep"></a>IDebugEngineProgram2::WatchForThreadStep
监视执行 (或停止监视) 线程上发生的执行事件。

## <a name="syntax"></a>语法

```cpp
HRESULT WatchForThreadStep( 
   IDebugProgram2* pOriginatingProgram,
   DWORD           dwTid,
   BOOL            fWatch,
   DWORD           dwFrame
);
```

```csharp
int WatchForThreadStep( 
   IDebugProgram2 pOriginatingProgram,
   uint           dwTid,
   int            fWatch,
   uint           dwFrame
);
```

## <a name="parameters"></a>参数
`pOriginatingProgram`\
[in]表示 [要逐步执行的程序的 IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) 对象。

`dwTid`\
[in]指定要监视的线程的标识符。

`fWatch`\
[in]非零 () 表示开始监视 由 标识的线程上的执行;否则，零 () 表示停止监视 上的 `TRUE` `dwTid` `FALSE` 执行 `dwTid` 。

`dwFrame`\
[in]指定控制步骤类型的帧索引。 如果此值为零 (0) ，则步骤类型为"单步执行"，只要执行 标识的线程，程序就会 `dwTid` 停止。 当 为非零时，步骤类型为"单步执行"，并且程序应仅在 标识的线程在堆栈上等于或高于 的帧中运行时 `dwFrame` `dwTid` 停止 `dwFrame` 。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 当会话调试管理器 (SDM) 由 参数标识的程序时，它会通过调用此方法通知 `pOriginatingProgram` 所有其他附加程序。

 此方法仅适用于同线程单步执行。

## <a name="see-also"></a>请参阅
- [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)

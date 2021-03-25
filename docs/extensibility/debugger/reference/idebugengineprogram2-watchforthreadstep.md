---
description: 监视执行 (或停止监视执行) 在给定线程上发生。
title: IDebugEngineProgram2：： WatchForThreadStep |Microsoft Docs
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
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9ddf7de557a5059a83aabdbfad7045e8dacbc71b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105093829"
---
# <a name="idebugengineprogram2watchforthreadstep"></a>IDebugEngineProgram2::WatchForThreadStep
监视执行 (或停止监视执行) 在给定线程上发生。

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
中表示正在进行的程序的 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) 对象。

`dwTid`\
中指定要监视的线程的标识符。

`fWatch`\
中非零 (`TRUE`) 表示开始监视由标识的线程上的执行 `dwTid` ; 否则，零 (`FALSE`) 表示停止在上监视执行 `dwTid` 。

`dwFrame`\
中指定控制步骤类型的帧索引。 如果此值为零 (0) ，则步骤类型为 "单步执行"，并在通过执行识别的线程时，程序应停止 `dwTid` 。 如果 `dwFrame` 为非零，则步骤类型为 "逐过程"，程序应仅在 `dwTid` 其索引与堆栈上的索引等于或高于的帧中运行时才应停止 `dwFrame` 。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 当会话调试管理器 (SDM) 执行由参数标识的程序时， `pOriginatingProgram` 它会通过调用此方法通知所有其他附加程序。

 此方法仅适用于线程单步执行。

## <a name="see-also"></a>另请参阅
- [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)

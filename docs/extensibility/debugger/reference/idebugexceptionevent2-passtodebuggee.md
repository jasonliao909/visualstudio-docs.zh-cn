---
description: 指定是否应在执行恢复时将异常传递给正在调试的程序，或是否应丢弃异常。
title: IDebugExceptionEvent2：:P assToDebuggee |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExceptionEvent2::PassToDebuggee
helpviewer_keywords:
- IDebugExceptionEvent2::PassToDebuggee
ms.assetid: a20d0f0b-2ca0-4437-bd22-9213c81d2738
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 96843835eb1873b6b754f651b853413680981a795e94e97b6aef6cfbd753e5e2
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121307617"
---
# <a name="idebugexceptionevent2passtodebuggee"></a>IDebugExceptionEvent2::PassToDebuggee
指定是否应在执行恢复时将异常传递给正在调试的程序，或是否应丢弃异常。

## <a name="syntax"></a>语法

```cpp
HRESULT PassToDebuggee(
   BOOL fPass
);
```

```csharp
int PassToDebuggee(
   int fPass
);
```

## <a name="parameters"></a>参数
`fPass`\
中 `TRUE` 如果异常应传递到执行恢复时正在调试的程序，则为非零 () 如果应丢弃异常，则为零 (`FALSE`) 。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 调用此方法实际上不会导致在正在调试的程序中执行任何代码。 调用只是为下一个代码执行设置状态。 例如，对 [CanPassToDebuggee](../../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md) 方法的调用可能会返回 `S_OK` [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)。`dwState` 字段设置为 `EXCEPTION_STOP_SECOND_CHANCE` 。

 IDE 可能会收到 [IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md) 事件并调用 [Continue](../../../extensibility/debugger/reference/idebugprogram2-continue.md) 方法。 如果未调用方法，调试引擎 (DE) 应具有处理事例的默认行为 `PassToDebuggee` 。

## <a name="see-also"></a>另请参阅
- [IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md)
- [CanPassToDebuggee](../../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md)
- [继续](../../../extensibility/debugger/reference/idebugprogram2-continue.md)

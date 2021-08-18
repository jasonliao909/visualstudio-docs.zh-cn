---
description: 指定是应在继续执行时将异常传递给正在调试的程序，还是应放弃异常。
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
ms.openlocfilehash: fd9360bfc5647c5edd244818f64570c6ca5554f7
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122118926"
---
# <a name="idebugexceptionevent2passtodebuggee"></a>IDebugExceptionEvent2::PassToDebuggee
指定是应在继续执行时将异常传递给正在调试的程序，还是应放弃异常。

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
[in]如果 () 在继续执行时将异常传递给正在调试的程序，则不为零;如果应丢弃异常，则 () 为零 `TRUE` `FALSE` 。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 调用此方法实际上不会导致在调试程序中执行任何代码。 调用只是为了设置下一个代码执行的状态。 例如，对[CanPassToDebuggee](../../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md)方法的调用可能会随 `S_OK` EXCEPTION_INFO 返回。 [](../../../extensibility/debugger/reference/exception-info.md)`dwState` 字段设置为 `EXCEPTION_STOP_SECOND_CHANCE` 。

 IDE 可能会接收 [IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md) 事件并调用 [Continue](../../../extensibility/debugger/reference/idebugprogram2-continue.md) 方法。 如果未调用 (，) DE 脚本的调试引擎应具有处理案例 `PassToDebuggee` 的默认行为。

## <a name="see-also"></a>请参阅
- [IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md)
- [CanPassToDebuggee](../../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md)
- [继续](../../../extensibility/debugger/reference/idebugprogram2-continue.md)

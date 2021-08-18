---
description: 由当前堆栈帧上的调试器在要截获当前异常时调用。
title: IDebugStackFrame3：：InterceptCurrentException |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame3::InterceptCurrentException
helpviewer_keywords:
- IDebugStackFrame3::InterceptCurrentException
ms.assetid: 116c7324-7645-4c15-b484-7a5cdd065ef5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6604c4a47e44df05d02b3b6c24c9efe12eeac0f2478ff28037e9bdb3c2a2e18a
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121338431"
---
# <a name="idebugstackframe3interceptcurrentexception"></a>IDebugStackFrame3::InterceptCurrentException
由当前堆栈帧上的调试器在要截获当前异常时调用。

## <a name="syntax"></a>语法

```cpp
HRESULT InterceptCurrentException(
   INTERCEPT_EXCEPTION_ACTION dwFlags,
   UINT64*                    pqwCookie
);
```

```csharp
int InterceptCurrentException(
   uint dwFlags,
   out  ulong pqwCookie
);
```

## <a name="parameters"></a>参数
`dwFlags`\
[in]指定不同的操作。 目前，仅 [INTERCEPT_EXCEPTION_ACTION](../../../extensibility/debugger/reference/intercept-exception-action.md) 值 `IEA_INTERCEPT` ，必须指定该值。

`pqwCookie`\
[out]标识特定异常的唯一值。

## <a name="return-value"></a>返回值
 如果成功，则返回S_OK;否则，返回错误代码。

 下面是最常见的错误返回结果。

|错误|说明|
|-----------|-----------------|
|`E_EXCEPTION_CANNOT_BE_INTERCEPTED`|无法截获当前异常。|
|`E_EXCEPTION_CANNOT_UNWIND_ABOVE_CALLBACK`|当前执行帧尚未搜索处理程序。|
|`E_INTERCEPT_CURRENT_EXCEPTION_NOT_SUPPORTED`|此帧不支持此方法。|

## <a name="remarks"></a>备注
 引发异常时，调试器在异常处理过程中从关键点的运行时获得控制权。 在这些关键时刻，调试器可以询问当前堆栈帧帧是否要截获异常。 这样，即使堆栈帧没有异常处理程序（例如，程序代码中的 try/catch 块 (，被截获的异常实质上也是堆栈帧的一个) 。

 当调试器想要了解异常是否应被截获时，它会在当前堆栈帧对象上调用此方法。 此方法负责处理异常的所有详细信息。 如果未 [实现 IDebugStackFrame3](../../../extensibility/debugger/reference/idebugstackframe3.md) 接口或方法返回任何错误，则调试器将继续 `InterceptStackException` 正常处理异常。

> [!NOTE]
> 只能在托管代码中截获异常，即当正在调试的程序在 .NET 运行时下运行时。 当然，第三方语言实现者可以在其自己的调试引擎中实现 `InterceptStackException` （如果已选择）。

 拦截完成后，发出 [IDebugInterceptExceptionCompleteEvent2](../../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2.md) 信号。

## <a name="see-also"></a>请参阅
- [IDebugStackFrame3](../../../extensibility/debugger/reference/idebugstackframe3.md)
- [INTERCEPT_EXCEPTION_ACTION](../../../extensibility/debugger/reference/intercept-exception-action.md)
- [IDebugInterceptExceptionCompleteEvent2](../../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2.md)

---
description: 确定调试引擎 (DE) 是否支持将此异常传递给执行恢复时正在调试的程序的选项。
title: IDebugExceptionEvent2：： CanPassToDebuggee |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExceptionEvent2::CanPassToDebuggee
helpviewer_keywords:
- IDebugExceptionEvent2::CanPassToDebuggee
ms.assetid: ae4bbe0a-fbe1-49be-a310-ea64279a434b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7fbc5cd55516f018a0a0877a114169a436b97fe1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084839"
---
# <a name="idebugexceptionevent2canpasstodebuggee"></a>IDebugExceptionEvent2::CanPassToDebuggee
确定调试引擎 (DE) 是否支持将此异常传递给执行恢复时正在调试的程序的选项。

## <a name="syntax"></a>语法

```cpp
HRESULT CanPassToDebuggee(
   void
);
```

```csharp
int CanPassToDebuggee();
```

## <a name="return-value"></a>返回值
 返回 `S_OK` (可以将异常传递给程序) 或 `S_FALSE` (无法在) 上传递异常。

## <a name="remarks"></a>备注
 DE 必须具有用于传递到调试对象的默认操作。 IDE 可能会收到 [IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md) 事件并调用 [Continue](../../../extensibility/debugger/reference/idebugprocess3-continue.md) 方法，而不调用 `CanPassToDebuggee` 方法。 因此，DE 应具有在上传递异常的默认情况。

## <a name="see-also"></a>另请参阅
- [IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md)
- [继续](../../../extensibility/debugger/reference/idebugprocess3-continue.md)

---
description: 确定调试引擎是否 (DE) 支持在继续执行时将此异常传递给正在调试的程序的选项。
title: IDebugExceptionEvent2：：CanPassToDebuggee |Microsoft Docs
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
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fb2d6ff025ab98e20a2251df993e400912ac1eef
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122127150"
---
# <a name="idebugexceptionevent2canpasstodebuggee"></a>IDebugExceptionEvent2::CanPassToDebuggee
确定调试引擎是否 (DE) 支持在继续执行时将此异常传递给正在调试的程序的选项。

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
 返回 (异常可以传递到程序) ， (异常 `S_OK` `S_FALSE` 不能传递到) 。

## <a name="remarks"></a>备注
 DE 必须具有用于传递给调试对象的默认操作。 IDE 可能会接收 [IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md) 事件并调用 [Continue](../../../extensibility/debugger/reference/idebugprocess3-continue.md) 方法，而无需调用 `CanPassToDebuggee` 方法。 因此，DE 应具有一个默认情况，用于或不传递异常。

## <a name="see-also"></a>请参阅
- [IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md)
- [继续](../../../extensibility/debugger/reference/idebugprocess3-continue.md)

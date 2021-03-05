---
description: 继续执行线程。
title: IDebugThread2：： Resume |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugThread2::Resume
helpviewer_keywords:
- IDebugThread2::Resume
ms.assetid: 36aad682-b0b9-40a2-b3fc-f0e61d41cdbc
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 64a7d5509ac098f6b3a47c3606b6ec530bb6b65b
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102164495"
---
# <a name="idebugthread2resume"></a>IDebugThread2::Resume
继续执行线程。

## <a name="syntax"></a>语法

```cpp
HRESULT Resume ( 
   DWORD *pdwSuspendCount
);
```

```csharp
int Resume ( 
   out uint pdwSuspendCount
);
```

## <a name="parameters"></a>参数
`pdwSuspendCount`\
弄返回恢复操作后的挂起计数。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 对此方法的每个调用都将减少挂起计数，直到达到0，此时将实际恢复执行。 此挂起计数显示在 " **线程** 调试" 窗口中。

 对于对此方法的每个调用，必须有对 [挂起](../../../extensibility/debugger/reference/idebugthread2-suspend.md) 方法的以前调用。 "挂起计数" 确定到 `IDebugThread2::Suspend` 目前为止已调用方法的次数。

## <a name="see-also"></a>另请参阅
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [挂起](../../../extensibility/debugger/reference/idebugthread2-suspend.md)

---
description: 恢复线程的执行。
title: IDebugThread2：：Resume |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugThread2::Resume
helpviewer_keywords:
- IDebugThread2::Resume
ms.assetid: 36aad682-b0b9-40a2-b3fc-f0e61d41cdbc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3bde7f2f80e64b04bdccc0c75006553f813b5763a352e1ecbae22d37781c70f0
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121292007"
---
# <a name="idebugthread2resume"></a>IDebugThread2::Resume
恢复线程的执行。

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
[out]返回恢复操作后的挂起计数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 每次调用此方法时，挂起计数会一直减到 0，此时实际会恢复执行。 此挂起计数显示在"线程调试 **"** 窗口中。

 每次调用此方法时，都必须以前调用 [Suspend](../../../extensibility/debugger/reference/idebugthread2-suspend.md) 方法。 挂起计数确定到目前为止调用方法 `IDebugThread2::Suspend` 多少次。

## <a name="see-also"></a>请参阅
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [挂起](../../../extensibility/debugger/reference/idebugthread2-suspend.md)

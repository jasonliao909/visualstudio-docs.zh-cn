---
description: 挂起线程。
title: IDebugThread2：：挂起 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugThread2::Suspend
helpviewer_keywords:
- IDebugThread2::Suspend
ms.assetid: 1e20be85-aa12-48de-bb83-0bf0976e99ae
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1298bd394209927b4563ff325149865db59a3f65b061e29d18e826d9f57bf7fd
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121291982"
---
# <a name="idebugthread2suspend"></a>IDebugThread2::Suspend
挂起线程。

## <a name="syntax"></a>语法

```cpp
HRESULT Suspend ( 
   DWORD *pdwSuspendCount
);
```

```csharp
HRESULT Suspend ( 
   out uint pdwSuspendCount
);
```

## <a name="parameters"></a>参数
`pdwSuspendCount`\
弄返回挂起操作后的挂起计数。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 对此方法的每个调用会递增大于0的挂起计数。 此挂起计数显示在 " **线程** 调试" 窗口中。

 对于对此方法的每个调用，必须在以后调用 [Resume](../../../extensibility/debugger/reference/idebugthread2-resume.md) 方法。

## <a name="see-also"></a>另请参阅
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [恢复](../../../extensibility/debugger/reference/idebugthread2-resume.md)

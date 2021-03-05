---
description: 执行调试程序。
title: IDebugProgram3：： ExecuteOnThread |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProgram3::ExecuteOnThread
ms.assetid: 2f5211e3-7a3f-47bf-9595-dfc8b4895d0d
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b3d996fd7b8cda1d5e36322c85d49c9889dd66dd
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102145997"
---
# <a name="idebugprogram3executeonthread"></a>IDebugProgram3::ExecuteOnThread
执行调试程序。 返回线程，以便在执行程序时为调试器信息指定用户正在查看哪个线程。

## <a name="syntax"></a>语法

```cpp
HRESULT ExecuteOnThread(
   [in] IDebugThread2* pThread)
```

```csharp
int ExecuteOnThread(
   IDebugThread2 pThread
);
```

## <a name="parameters"></a>参数
`pThread`\
中一个 [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) 对象。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 调试器可以使用三种不同的方法在停止后恢复执行：

- Execute：取消任何前一步骤，并运行到下一个断点等。

- 步骤：取消任何旧步骤，并运行到新步骤完成。

- 继续：再次运行，并使任何旧步骤保持活动状态。

  `ExecuteOnThread`在确定要取消的步骤时，传递给的线程非常有用。 如果不知道该线程，运行 "执行" 将取消所有步骤。 了解线程后，只需取消活动线程上的步骤。

## <a name="see-also"></a>另请参阅
- [执行](../../../extensibility/debugger/reference/idebugprogram2-execute.md)
- [IDebugProgram3](../../../extensibility/debugger/reference/idebugprogram3.md)

---
description: 执行调试程序。
title: IDebugProgram3：：ExecuteOnThread |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProgram3::ExecuteOnThread
ms.assetid: 2f5211e3-7a3f-47bf-9595-dfc8b4895d0d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d0e903431dbdcc4853d205ea6107ca6e70b91647
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122126513"
---
# <a name="idebugprogram3executeonthread"></a>IDebugProgram3::ExecuteOnThread
执行调试程序。 返回线程以向调试器提供用户在执行程序时正在查看的线程的信息。

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
[in] [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) 对象。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 调试器可通过三种不同的方式在停止后恢复执行：

- 执行：取消上一步，并运行到下一个断点等。

- 步骤：取消任何旧步骤，并运行到新步骤完成。

- 继续：再次运行，使任何旧步骤保持活动状态。

  传递给 的 `ExecuteOnThread` 线程在决定取消哪个步骤时非常有用。 如果不知道线程，则运行 execute 会取消所有步骤。 了解线程后，只需取消活动线程上的步骤。

## <a name="see-also"></a>请参阅
- [执行](../../../extensibility/debugger/reference/idebugprogram2-execute.md)
- [IDebugProgram3](../../../extensibility/debugger/reference/idebugprogram3.md)

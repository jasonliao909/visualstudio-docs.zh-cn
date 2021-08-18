---
description: 从停止状态继续运行此过程。 任何以前的执行状态 (如步骤) 清除，并且进程将再次开始执行。
title: IDebugProcess3：：Execute |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess3::Execute
helpviewer_keywords:
- IDebugProcess3::Execute
ms.assetid: d831cd81-d7bf-4172-8517-aa699867791f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b32c80a904e9ec96fd5f49b3d54c75fce26327b3
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122126669"
---
# <a name="idebugprocess3execute"></a>IDebugProcess3::Execute
从停止状态继续运行此过程。 任何以前的执行状态 (如步骤) 清除，并且进程将再次开始执行。

> [!NOTE]
> 应使用此方法而不是执行[。](../../../extensibility/debugger/reference/idebugprogram2-execute.md)

## <a name="syntax"></a>语法

```cpp
HRESULT Execute(
   IDebugThread2* pThread
);
```

```csharp
int Execute(
   IDebugThread2 pThread
);
```

## <a name="parameters"></a>参数
`pThread`\
[in]表示 [要执行的线程的 IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) 对象。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 当用户从其他进程线程中的停止状态开始执行时，将对此进程调用此方法。 当用户从 IDE 的"调试"菜单中选择"开始"命令时，也会调用此方法。 此方法的实现可能很简单，就像在进程中的当前线程上调用 [Resume](../../../extensibility/debugger/reference/idebugthread2-resume.md) 方法一样简单。

> [!WARNING]
> 在处理此调用时，不要将停止事件 (同步) 事件发送到 Event; [](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)否则调试器可能会停止响应。

## <a name="see-also"></a>请参阅
- [IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [恢复](../../../extensibility/debugger/reference/idebugthread2-resume.md)
- [事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)

---
description: 使进程单步执行一条指令或语句。
title: IDebugProcess3：：Step |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess3::Step
helpviewer_keywords:
- IDebugProcess3::Step
ms.assetid: 6ad9094c-27cc-4927-8a7c-1b4d97b2e436
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 27dc90056c9c0e5c0521a4102cec4714c72b3cc9
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122132816"
---
# <a name="idebugprocess3step"></a>IDebugProcess3::Step
使进程单步执行一条指令或语句。

> [!NOTE]
> 应使用此方法而不是步骤[。](../../../extensibility/debugger/reference/idebugprogram2-step.md)

## <a name="syntax"></a>语法

```cpp
HRESULT Step(
   IDebugThread2* pThread,
   STEPKIND       sk,
   STEPUNIT       step,
);
```

```csharp
int Step(
   IDebugThread2 pThread,
   enum_STEPKIND sk,
   enum_STEPUNIT step
);
```

## <a name="parameters"></a>参数
`pThread`\
[in]表示 [正在单步执行线程的 IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) 对象。

`sk`\
[in] [STEPKIND 值之](../../../extensibility/debugger/reference/stepkind.md) 一。

`step`\
[in]STEPUNIT [值之](../../../extensibility/debugger/reference/stepunit.md) 一。

## <a name="return-value"></a>返回值
 如果成功，则返回S_OK;否则返回错误代码。

## <a name="remarks"></a>备注
 如果线程之间有任何线程同步或通信，则进程中的其他线程应在特定线程单步执行时运行。

 **警告** 在处理此调用时，不要将停止事件 (同步) 事件发送到 Event; [](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)否则调试器可能会停止响应。

## <a name="see-also"></a>请参阅
- [IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [STEPKIND](../../../extensibility/debugger/reference/stepkind.md)
- [STEPUNIT](../../../extensibility/debugger/reference/stepunit.md)
- [事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)

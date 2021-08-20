---
description: IDebugProgram2：：Continue 继续从已停止状态运行此程序。 任何以前的执行状态 (如步骤) ，程序将再次开始执行。
title: IDebugProgram2：：Continue |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::Continue
helpviewer_keywords:
- IDebugProgram2::Continue
ms.assetid: e5a6e02a-d21b-4a03-a034-e8de1f71ce2e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 60d9e3d62c49def63ea49592e8cfee1e651a6c78
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122159797"
---
# <a name="idebugprogram2continue"></a>IDebugProgram2::Continue
继续从已停止状态运行此程序。 任何以前的执行状态 (如步骤) ，程序将再次开始执行。

> [!NOTE]
> 不推荐使用此方法。 请 [改为使用 Continue](../../../extensibility/debugger/reference/idebugprocess3-continue.md) 方法。

## <a name="syntax"></a>语法

```cpp
HRESULT Continue( 
   IDebugThread2* pThread
);
```

```csharp
int Continue( 
   IDebugThread2 pThread
);
```

## <a name="parameters"></a>参数
`pThread` [in]表示 [线程的 IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) 对象。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 无论正在调试多少程序，或者哪个程序生成了停止事件，都会对此程序调用此方法。 实现必须保留以前的执行状态 (如步骤) 继续执行，就像在完成之前执行之前从未停止过一样。 也就是说，如果此程序中的线程正在执行单步执行操作，并且由于其他一些程序停止而停止，然后调用此方法，则程序必须完成原始的逐过程操作。

> [!WARNING]
> 在处理此调用时，不要将停止事件 (同步) 事件发送到 Event; [](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)否则调试器可能会停止响应。

## <a name="see-also"></a>请参阅
- [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)
- [事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)

---
description: 指定事件属性。
title: EVENTATTRIBUTES |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- EVENTATTRIBUTES
helpviewer_keywords:
- EVENTATTRIBUTES enumeration
ms.assetid: 04db10f7-df31-4464-98e8-b3777428179e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 043251ad59cc61cd250aa0213bbda8bf7d4e1fc16d5e839d15698ff6911c5ba2
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121390302"
---
# <a name="eventattributes"></a>EVENTATTRIBUTES
指定事件属性。

## <a name="syntax"></a>语法

```cpp
enum enum_EVENTATTRIBUTES {
    EVENT_ASYNCHRONOUS          = 0x0000,
    EVENT_SYNCHRONOUS           = 0x0001,
    EVENT_STOPPING              = 0x0002,
    EVENT_ASYNC_STOP            = 0x0002,
    EVENT_SYNC_STOP             = 0x0003,
    EVENT_IMMEDIATE             = 0x0004,
    EVENT_EXPRESSION_EVALUATION = 0x0008
};
typedef DWORD EVENTATTRIBUTES;
```

```csharp
public enum enum_EVENTATTRIBUTES {
    EVENT_ASYNCHRONOUS          = 0x0000,
    EVENT_SYNCHRONOUS           = 0x0001,
    EVENT_STOPPING              = 0x0002,
    EVENT_ASYNC_STOP            = 0x0002,
    EVENT_SYNC_STOP             = 0x0003,
    EVENT_IMMEDIATE             = 0x0004,
    EVENT_EXPRESSION_EVALUATION = 0x0008
};
```

## <a name="fields"></a>字段
`EVENT_ASYNCHRONOUS`\
指示事件是异步的，不需要对事件进行回复。

`EVENT_SYNCHRONOUS`\
指示事件是同步的;通过 [ContinueFromSynchronousEvent 进行回复](../../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md)。

`EVENT_STOPPING`\
指示这是一个停止事件。 必须与 或 `EVENT_ASYNCHRONOUS` 结合使用 `EVENT_SYNCHRONOUS` 。

`EVENT_ASYNC_STOP`\
指示异步停止事件。 当前没有此类事件。 此标志只是占位符。

`EVENT_SYNC_STOP`\
指示同步停止事件 (和 `EVENT_SYNCHRONOUS` `EVENT_STOPPING`) 。 在发送停止事件时，调试引擎 (DE) 使用此值。 通过调用"执行"、"步骤"或[](../../../extensibility/debugger/reference/idebugprogram2-execute.md)"继续[](../../../extensibility/debugger/reference/idebugprogram2-step.md)["进行答复](../../../extensibility/debugger/reference/idebugprogram2-continue.md)。

`EVENT_IMMEDIATE`\
指示立即同步发送到 IDE 的事件。 此标志与其他标志（如 、 或 ）结合使用，以指示事件的类型以及答复机制在 (`EVENT_ASYNCHRONOUS` `EVENT_SYNCHRONOUS` 已知) `EVENT_SYNC_STOP` 这一事实。

`EVENT_EXPRESSION_EVALUATION`\
事件是表达式计算的结果。

## <a name="remarks"></a>备注
这些值在 Event 方法 `dwAttrib` 的 参数 [中](../../../extensibility/debugger/reference/idebugeventcallback2-event.md) 传递。

这些值可以与位 合并 `OR` 。

## <a name="requirements"></a>要求
标头：msdbg.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [ContinueFromSynchronousEvent](../../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md)
- [事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)

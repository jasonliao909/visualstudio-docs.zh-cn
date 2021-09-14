---
description: 通知调试引擎 (DE) 是在当前代码位置停止还是继续执行。
title: IDebugCanStopEvent2：：CanStop |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCanStopEvent2::CanStop
helpviewer_keywords:
- IDebugCanStopEvent2::CanStop
ms.assetid: 7d61adbe-6b3d-41f3-86a1-45d9cc01a7f8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: dd575d6bb1afdf296eff6ec3ac3a08a9551618b8
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602629"
---
# <a name="idebugcanstopevent2canstop"></a>IDebugCanStopEvent2::CanStop
通知调试引擎 (DE) 是在当前代码位置停止还是继续执行。

## <a name="syntax"></a>语法

```cpp
HRESULT CanStop ( 
   BOOL fCanStop
);
```

```csharp
int CanStop ( 
   int fCanStop
);
```

## <a name="parameters"></a>parameters
`fCanStop`\
[in]如果 DE 应 () ，则不为零; `TRUE` 否则， () 。 `FALSE`

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 此事件的接收方通常调用 [GetReason](../../../extensibility/debugger/reference/idebugcanstopevent2-getreason.md) 方法以确定 DE 想要停止的原因，然后使用相应的响应 `IDebugCanStopEvent2::CanStop` 调用方法。

 如果 DE 停止，它将发送描述停止原因的事件。 通常发送两个事件 [：IDebugBreakEvent2](../../../extensibility/debugger/reference/idebugbreakevent2.md) 接口表示的用户或信号中断，以及 [IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md) 接口表示的断点事件。

## <a name="see-also"></a>另请参阅
- [IDebugCanStopEvent2](../../../extensibility/debugger/reference/idebugcanstopevent2.md)
- [IDebugBreakEvent2](../../../extensibility/debugger/reference/idebugbreakevent2.md)
- [IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md)
- [GetReason](../../../extensibility/debugger/reference/idebugcanstopevent2-getreason.md)

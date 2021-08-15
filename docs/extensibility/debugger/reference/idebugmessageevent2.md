---
description: 此接口由调试引擎 (DE) 用来向需要Visual Studio响应的用户发送消息。
title: IDebugMessageEvent2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMessageEvent2
helpviewer_keywords:
- IDebugMessageEvent2 interface
ms.assetid: a9ff3d00-e9ac-4cd6-bda9-584a4815aff8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 21bd32714b9f10174a1ebd3c2ad82dda16db715f9600318bd391f0c99e036463
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121307318"
---
# <a name="idebugmessageevent2"></a>IDebugMessageEvent2
此接口由调试引擎 (DE) 用来向需要Visual Studio响应的用户发送消息。

## <a name="syntax"></a>语法

```
IDebugMessageEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 DE 实现此接口，以将消息Visual Studio需要用户响应的接口。 必须在与此接口相同的对象上实现 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) 接口。 SDM 使用 [QueryInterface](/cpp/atl/queryinterface) 访问 `IDebugEvent2` 接口。

 此接口的实现必须Visual Studio [SetResponse](../../../extensibility/debugger/reference/idebugmessageevent2-setresponse.md)对 DE 的调用。 例如，可以通过将消息发送到 DE 的消息处理线程来实现此目的，或者实现此接口的对象可以保存对 DE 的引用，并通过将响应传递到 来调用 `IDebugMessageEvent2::SetResponse` DE。

## <a name="notes-for-callers"></a>调用方说明
 DE 创建并发送此事件对象，以向需要响应的用户显示消息。 事件是通过使用 SDM 在附加到正在调试的程序时提供的 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) 回调函数发送的。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法 `IDebugMessageEvent2` 。

|方法|说明|
|------------|-----------------|
|[GetMessage](../../../extensibility/debugger/reference/idebugmessageevent2-getmessage.md)|获取要显示的消息。|
|[SetResponse](../../../extensibility/debugger/reference/idebugmessageevent2-setresponse.md)|设置消息框中的响应（如果有）。|

## <a name="remarks"></a>备注
 如果 DE 需要用户对特定消息做出特定响应，则它将使用此接口。 例如，如果 DE 在尝试远程附加到程序后收到"拒绝访问"消息，则 DE 会向具有消息框样式 的 Visual Studio 发送此特定 `IDebugMessageEvent2` 消息 `MB_RETRYCANCEL` 。 这允许用户重试或取消附加操作。

 DE 指定如何处理此消息，具体方法为遵循 Win32 函数的约定， (`MessageBox` [AfxMessageBox](/cpp/mfc/reference/cstring-formatting-and-message-box-display#afxmessagebox) 了解) 。

 使用[IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md)接口将消息发送到Visual Studio不需要用户响应的用户。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md)

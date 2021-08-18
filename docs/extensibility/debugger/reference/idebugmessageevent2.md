---
description: 调试引擎使用此接口 (DE) 向需要用户响应的 Visual Studio 发送消息。
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
ms.openlocfilehash: 4940d8d19c76b9e64da4dbbb3b659519bace24e3
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122126981"
---
# <a name="idebugmessageevent2"></a>IDebugMessageEvent2
调试引擎使用此接口 (DE) 向需要用户响应的 Visual Studio 发送消息。

## <a name="syntax"></a>语法

```
IDebugMessageEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 DE 实现此接口，以将消息发送到需要用户响应 Visual Studio。 必须在与此接口相同的对象上实现 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) 接口。 SDM 使用 [QueryInterface](/cpp/atl/queryinterface) 访问 `IDebugEvent2` 接口。

 此接口的实现必须 Visual Studio 调用[SetResponse](../../../extensibility/debugger/reference/idebugmessageevent2-setresponse.md)的调用。 例如，可以通过将消息发布到已解除的消息处理线程来完成此操作，或者实现此接口的对象可以包含对 DE 的引用并回调传入的响应 `IDebugMessageEvent2::SetResponse` 。

## <a name="notes-for-callers"></a>调用方说明
 DE 创建并发送此事件对象，以向用户显示需要响应的消息。 此事件在附加到正在调试的程序时，使用 SDM 提供的 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) 回调函数发送。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法 `IDebugMessageEvent2` 。

|方法|说明|
|------------|-----------------|
|[GetMessage](../../../extensibility/debugger/reference/idebugmessageevent2-getmessage.md)|获取要显示的消息。|
|[SetResponse](../../../extensibility/debugger/reference/idebugmessageevent2-setresponse.md)|设置消息框中的响应（如果有）。|

## <a name="remarks"></a>备注
 如果需要特定消息的用户特定响应，则 DE 将使用此接口。 例如，如果在尝试远程附加到程序后取消了 "拒绝访问" 消息，则 de 会将此特定消息发送到 `IDebugMessageEvent2` 具有消息框样式的事件中的 Visual Studio `MB_RETRYCANCEL` 。 这允许用户重试或取消附加操作。

 DE 指定如何按照 Win32 函数的约定处理此消息 `MessageBox` (参阅 [AfxMessageBox](/cpp/mfc/reference/cstring-formatting-and-message-box-display#afxmessagebox) 了解详细信息) 。

 使用[IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md)接口将消息发送到不需要用户响应的 Visual Studio。

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md)

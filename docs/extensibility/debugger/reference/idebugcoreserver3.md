---
description: 此接口可用于访问有关进程正在其中运行的服务器的信息。
title: IDebugCoreServer3 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer3
helpviewer_keywords:
- IDebugCoreServer3 interface
ms.assetid: 51f5f41b-a5a4-4df0-a703-41f3d1811d7f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 38e839ef5c653bfe21541371f8320c74cfa4679b
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122127358"
---
# <a name="idebugcoreserver3"></a>IDebugCoreServer3
此接口可用于访问有关进程正在其中运行的服务器的信息。

## <a name="syntax"></a>语法

```
IDebugCoreServer3 : IDebugCoreServer2
```

## <a name="notes-for-implementers"></a>实施者注意事项
 Visual Studio 实现此接口。

## <a name="notes-for-callers"></a>调用方说明
 使用 [QueryInterface](/cpp/atl/queryinterface) 从 [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md) 接口获取此接口。 对 [GetServer](../../../extensibility/debugger/reference/idebugdefaultport2-getserver.md) 的调用也可以返回此接口。 自定义端口供应商最常使用此接口来启动 (本地或远程) 的服务器上的程序。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了 [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md) 接口上的方法，此接口还实现以下方法：

|方法|说明|
|------------|-----------------|
|[GetServerName](../../../extensibility/debugger/reference/idebugcoreserver3-getservername.md)|检索服务器的名称。|
|[GetServerFriendlyName](../../../extensibility/debugger/reference/idebugcoreserver3-getserverfriendlyname.md)|检索服务器名称的友好版本|
|[EnableAutoAttach](../../../extensibility/debugger/reference/idebugcoreserver3-enableautoattach.md)|告诉特定的调试引擎在进程启动时自动附加到进程。|
|[DiagnoseWebDebuggingError](../../../extensibility/debugger/reference/idebugcoreserver3-diagnosewebdebuggingerror.md)|在自动附加失败时检索特定错误代码。|
|[CreateInstanceInServer](../../../extensibility/debugger/reference/idebugcoreserver3-createinstanceinserver.md)|在服务器上创建调试引擎的实例。|
|[QueryIsLocal](../../../extensibility/debugger/reference/idebugcoreserver3-queryislocal.md)|检索一个标志，该标志指示服务器是否与调用方位于同一计算机上。|
|[GetConnectionProtocol](../../../extensibility/debugger/reference/idebugcoreserver3-getconnectionprotocol.md)|检索一个值，该值指示用于与服务器通信的协议。|
|[DisableAutoAttach](../../../extensibility/debugger/reference/idebugcoreserver3-disableautoattach.md)|对于此服务器知道的所有调试引擎，禁用所有自动附加设置。|

## <a name="remarks"></a>备注
 自定义端口供应商在调用[事件](../../../extensibility/debugger/reference/idebugportevents2-event.md)时接收[IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)接口。 `IDebugCoreServer3`可从该接口获取接口。

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)
- [GetServer](../../../extensibility/debugger/reference/idebugdefaultport2-getserver.md)

---
description: 此接口用于表示和获取网络上计算机上服务器的信息。
title: IDebugCoreServer2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer2
helpviewer_keywords:
- IDebugCoreServer2 interface
ms.assetid: 9c47d0a6-9eb1-464e-bd44-fa2b552d4d36
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: c3589ad1a0c5eab4564df0584a19d207a2fdd49d9ceff84d96667bb66d12770f
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121292775"
---
# <a name="idebugcoreserver2"></a>IDebugCoreServer2
此接口用于表示和获取网络上计算机上服务器的信息。

## <a name="syntax"></a>语法

```
IDebugCoreServer2 : IUknown
```

## <a name="notes-for-implementers"></a>实现者说明
 Visual Studio实现此接口来表示服务器。 每个 实例Visual Studio创建此接口的实例。

## <a name="notes-for-callers"></a>调用方说明
 自定义端口供应商在调用事件 时接收此 [接口](../../../extensibility/debugger/reference/idebugportevents2-event.md)。

 调试引擎可以通过调用 [GetServer](../../../extensibility/debugger/reference/idebugdefaultport2-getserver.md) (间接获取此接口，该调用返回 [IDebugCoreServer3（](../../../extensibility/debugger/reference/idebugcoreserver3.md)派生 `IDebugCoreServer2` 自) 。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法 `IDebugCoreServer2` 。

|方法|说明|
|------------|-----------------|
|[GetMachineInfo](../../../extensibility/debugger/reference/idebugcoreserver2-getmachineinfo.md)|获取计算机的名称和属性。|
|[GetMachineName](../../../extensibility/debugger/reference/idebugcoreserver2-getmachinename.md)|获取计算机的名称。|
|[GetPortSupplier](../../../extensibility/debugger/reference/idebugcoreserver2-getportsupplier.md)|获取计算机上存在的端口供应商。|
|[GetPort](../../../extensibility/debugger/reference/idebugcoreserver2-getport.md)|获取计算机上已存在的端口。|
|[EnumPorts](../../../extensibility/debugger/reference/idebugcoreserver2-enumports.md)|为计算机上的所有端口创建枚举器。|
|[EnumPortSuppliers](../../../extensibility/debugger/reference/idebugcoreserver2-enumportsuppliers.md)|为计算机上的所有端口供应商创建枚举器。|
|[GetMachineUtilities_V7](../../../extensibility/debugger/reference/idebugcoreserver2-getmachineutilities-v7.md)|获取计算机计算机实用工具。|

## <a name="remarks"></a>备注
 此接口还由 Visual Studio用于浏览网络上计算机上运行的进程。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
- [事件](../../../extensibility/debugger/reference/idebugportevents2-event.md)
- [GetServer](../../../extensibility/debugger/reference/idebugdefaultport2-getserver.md)
- [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)

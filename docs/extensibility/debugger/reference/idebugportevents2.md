---
description: 此接口在特定端口上通知侦听器 (通常是会话调试管理器 [SDM] 或调试引擎) 进程和程序创建和销毁。
title: IDebugPortEvents2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortEvents2
helpviewer_keywords:
- IDebugPortEvents2 interface
ms.assetid: 2c017094-3ba2-4067-83f9-147df1d96bce
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d8e1ccbb2726fb0f90fae2d31a4b07daad9bae91
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105065380"
---
# <a name="idebugportevents2"></a>IDebugPortEvents2
此接口在特定端口上通知侦听器 (通常是会话调试管理器 [SDM] 或调试引擎) 进程和程序创建和销毁。 此信息可用于显示在端口上运行的进程和程序的实时视图。

## <a name="syntax"></a>语法

```
IDebugPortEvents2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 Visual Studio 通常实现此接口以接收有关程序创建和析构的通知。 调试引擎还可以实现此接口来侦听此类端口事件。

## <a name="notes-for-callers"></a>调用方说明
 所有 [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) 接口都可以查询 <xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer> 接口。 然后， <xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer.FindConnectionPoint%2A> `IDebugPortEvents2` 在接口中调用的方法 <xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer> 来获取 <xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint> 接口。 最后， <xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint.Advise%2A> 调用接口中的 <xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint> 方法以通过 [事件](../../../extensibility/debugger/reference/idebugportevents2-event.md) 方法发送事件。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法 `IDebugPortEvents2` 。

|方法|说明|
|------------|-----------------|
|[事件](../../../extensibility/debugger/reference/idebugportevents2-event.md)|发送用于描述端口上的进程和程序的创建和析构的事件。|

## <a name="remarks"></a>备注
 `IDebugPortEvents2` SDM 还用于调试在已调试的进程中运行的程序。

 端口事件通过此接口传递到 SDM。

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)

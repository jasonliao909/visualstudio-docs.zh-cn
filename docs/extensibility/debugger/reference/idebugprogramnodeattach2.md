---
description: 允许程序节点收到尝试附加到关联程序的通知。
title: IDebugProgramNodeAttach2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNodeAttach2
helpviewer_keywords:
- IDebugProgramNodeAttach2 interface
ms.assetid: 46b37ac9-a026-4ad3-997b-f19e2f8deb73
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: a579d985cea401f855934b1966e387c7a5a1832a12f2f347b734f6a7e035f7f4
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121449178"
---
# <a name="idebugprogramnodeattach2"></a>IDebugProgramNodeAttach2
允许程序节点收到尝试附加到关联程序的通知。

## <a name="syntax"></a>语法

```
IDebugProgramNodeAttach2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 此接口是在实现 [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) 接口的同一个类上实现的，以便接收附加操作的通知，并提供取消附加操作的机会。

## <a name="notes-for-callers"></a>调用方说明
 通过调用 `QueryInterface` [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) 对象中的 方法获取此接口。 必须在 Attach 方法之前调用[OnAttach](../../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)方法，使程序节点有机会停止附加进程。 [](../../../extensibility/debugger/reference/idebugengine2-attach.md)

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 此接口实现以下方法：

|方法|说明|
|------------|-----------------|
|[OnAttach](../../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)|附加到关联的程序，或将附加进程延迟到 [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) 方法。|

## <a name="remarks"></a>备注
 此接口是弃用的方法的首选[Attach_V7方法。](../../../extensibility/debugger/reference/idebugprogramnode2-attach-v7.md) 所有调试引擎始终使用 函数加载，也就是说，它们实例化在正在调试 `CoCreateInstance` 的程序的地址空间之外。

 如果方法的以前实现只是设置正在调试的程序的 ，则只需要实现 `IDebugProgramNode2::Attach_V7` `GUID` [OnAttach](../../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md) 方法。

 如果方法的先前实现使用了提供的回调接口，则该功能需要移动到 Attach 方法的实现中，并且 `IDebugProgramNode2::Attach_V7` [](../../../extensibility/debugger/reference/idebugengine2-attach.md) `IDebugProgramNodeAttach2` 无需实现接口。

## <a name="requirements"></a>要求
 标头：Msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
- [附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)
- [Attach_V7](../../../extensibility/debugger/reference/idebugprogramnode2-attach-v7.md)

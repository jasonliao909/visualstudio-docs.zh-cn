---
description: 此接口表示已准备好绑定到代码位置的断点。
title: IDebugPendingBreakpoint2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPendingBreakpoint2
helpviewer_keywords:
- IDebugPendingBreakpoint2 interface
ms.assetid: d416b095-917e-475e-b796-ec0a03ffb8da
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 96de5582c4ae60c9775af5ca72e5a15b8a370a7e
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122160069"
---
# <a name="idebugpendingbreakpoint2"></a>IDebugPendingBreakpoint2
此接口表示已准备好绑定到代码位置的断点。

## <a name="syntax"></a>语法

```
IDebugPendingBreakpoint2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 调试引擎 (DE) 实现此接口，作为对断点的支持的一部分。

## <a name="notes-for-callers"></a>调用方说明
 对 [CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md) 的调用从 [IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md) 接口创建挂起的断点。 对 [Bind 的](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md) 调用将 `IDebugBreakpoint2` 创建一个接口，该接口表示程序中的绑定断点。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法 `IDebugPendingBreakpoint2` 。

|方法|说明|
|------------|-----------------|
|[CanBind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-canbind.md)|确定此挂起断点是否可以绑定到代码位置。|
|[绑定](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)|将这个挂起的断点绑定到一个或多个代码位置。|
|[GetState](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getstate.md)|获取此挂起断点的状态。|
|[GetBreakpointRequest](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getbreakpointrequest.md)|获取用于创建此挂起断点的断点请求。|
|[Virtualize](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-virtualize.md)|切换此挂起断点的虚拟化状态。|
|启用|切换此挂起断点的启用状态。|
|[SetCondition](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-setcondition.md)|设置或更改与此挂起断点关联的条件。|
|[SetPassCount](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-setpasscount.md)|设置或更改与此挂起断点关联的传递计数。|
|[EnumBoundBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md)|枚举从此挂起断点绑定的所有断点。|
|[EnumErrorBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md)|枚举此挂起断点导致的所有错误断点。|
|[删除](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-delete.md)|删除此挂起断点及其绑定的所有断点。|

## <a name="remarks"></a>备注
 `IDebugPendingBreakpoint2` 可以将 视为将断点绑定到可应用于一个或多个程序的代码所需的全部必要信息的提供程序。

 挂起的断点可能会生成多个绑定断点。 例如，C++样式模板中的断点可能会为该模板的每个唯一实例生成绑定断点。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)
- [GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugbreakpointboundevent2-getpendingbreakpoint.md)
- [GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugboundbreakpoint2-getpendingbreakpoint.md)
- [GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugerrorbreakpoint2-getpendingbreakpoint.md)

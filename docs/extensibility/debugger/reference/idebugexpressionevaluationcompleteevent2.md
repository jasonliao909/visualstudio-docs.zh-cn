---
description: 当异步表达式计算完成时，调试引擎 (DE) 将此接口 (SDM) 会话调试管理器。
title: IDebugExpressionEvaluationCompleteEvent2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpressionEvaluationCompleteEvent2
helpviewer_keywords:
- IDebugExpressionEvaluationCompleteEvent2
ms.assetid: d538fc19-55bf-4231-9595-eb01e84fd1d8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: f6690c2bd598b0662cc5ef54170726ac8efe99e2
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664530"
---
# <a name="idebugexpressionevaluationcompleteevent2"></a>IDebugExpressionEvaluationCompleteEvent2
当异步表达式计算完成时，调试引擎 (DE) 将此接口 (SDM) 会话调试管理器。

## <a name="syntax"></a>语法

```
IDebugExpressionEvaluationCompleteEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 DE 实现此接口以报告由对 [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)的调用启动的表达式计算完成。 必须在与此接口相同的对象上实现 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) 接口。 SDM 使用 [QueryInterface](/cpp/atl/queryinterface) 访问 `IDebugEvent2` 接口。

## <a name="notes-for-callers"></a>调用方说明
 DE 创建并发送此事件对象以报告表达式计算完成。 事件是通过使用 SDM 在附加到正在调试的程序时提供的 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) 回调函数发送的。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法 `IDebugExpressionEvaluationCompleteEvent2` 。

|方法|说明|
|------------|-----------------|
|[GetExpression](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getexpression.md)|获取原始表达式。|
|[GetResult](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getresult.md)|获取表达式计算的结果。|

## <a name="remarks"></a>备注
 DE 必须发送此事件，无论评估是否成功。

 如果评估未成功，则和 标志将不会在 `DEBUG_PROPINFO_VALUE` `DEBUG_PROPINFO_ATTRIB` [GetPropertyInfo](../../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) (返回的[DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)结构中设置 ([IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)对象由 DE 创建，如果评估失败，则返回 `IDebugExpressionEvaluationCompleteEvent2` 事件) 。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)

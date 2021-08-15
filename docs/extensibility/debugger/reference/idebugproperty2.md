---
description: 此接口表示堆栈帧属性、程序文档属性或其他属性。
title: IDebugProperty2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2
helpviewer_keywords:
- IDebugProperty2 interface
ms.assetid: a7d5c70f-a1a5-4120-9f70-184e01c25bff
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 7a368969251eb4f47746a1cb56491cf8f0dcf3d63664835177ea690b3ecab2b6
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121306993"
---
# <a name="idebugproperty2"></a>IDebugProperty2
此接口表示堆栈帧属性、程序文档属性或其他属性。 属性通常是表达式计算的结果。

> [!NOTE]
> 尽管 可以表示此类实体，但不应将"property"的这种使用与表示类的成员变量 `IDebugProperty2` 混淆。

## <a name="syntax"></a>语法

```
IDebugProperty2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 DE 实现此接口来表示特定类型的值。 例如，该值可以是表达式计算结果的数值、用于显示内存的内存上下文或寄存器及其值的列表。

## <a name="notes-for-callers"></a>调用方说明
 调用 [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) 或 [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) 以获取此接口，该接口表示计算结果。 `IDebugExpression2::EvaluateAsync` 通过向 SDM 发送 [IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md) 接口返回此接口，该接口又调用 [GetResult](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getresult.md) 来检索 属性。

- [GetDebugProperty](../../../extensibility/debugger/reference/idebugpropertycreateevent2-getdebugproperty.md) 返回此接口以提供关联的脚本文档。

- [GetReturnValue](../../../extensibility/debugger/reference/idebugreturnvalueevent2-getreturnvalue.md) 返回此接口以表示函数的返回值。

- [GetDebugProperty](../../../extensibility/debugger/reference/idebugprogram2-getdebugproperty.md) 返回此接口以表示程序的各种属性，例如名称或内存上下文。

- [GetDebugProperty](../../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md) 返回此接口以表示堆栈帧的各种属性，例如局部变量。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法 `IDebugProperty2` 。

|方法|说明|
|------------|-----------------|
|[GetPropertyInfo](../../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)|填充描述 [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) 的属性结构。|
|[SetValueAsString](../../../extensibility/debugger/reference/idebugproperty2-setvalueasstring.md)|设置字符串中属性的值。|
|[SetValueAsReference](../../../extensibility/debugger/reference/idebugproperty2-setvalueasreference.md)|从给定引用的值设置 属性的值。|
|[EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)|枚举属性的子项。|
|[GetParent](../../../extensibility/debugger/reference/idebugproperty2-getparent.md)|返回属性的父级。|
|[GetDerivedMostProperty](../../../extensibility/debugger/reference/idebugproperty2-getderivedmostproperty.md)|返回描述属性的最派生属性的属性。|
|[GetMemoryBytes](../../../extensibility/debugger/reference/idebugproperty2-getmemorybytes.md)|返回构成属性值的内存字节数。|
|[GetMemoryContext](../../../extensibility/debugger/reference/idebugproperty2-getmemorycontext.md)|返回属性值的内存上下文。|
|[GetSize](../../../extensibility/debugger/reference/idebugproperty2-getsize.md)|返回属性值的大小（以字节为单位）。|
|[GetReference](../../../extensibility/debugger/reference/idebugproperty2-getreference.md)|返回对此属性的值的引用。|
|[GetExtendedInfo](../../../extensibility/debugger/reference/idebugproperty2-getextendedinfo.md)|返回属性的扩展信息。|

## <a name="remarks"></a>备注
 接口表示的属性可视为具有名称、类型和地址 `IDebugProperty2` 的值。 在更一般的术语中， 可以表示具有层次结构（具有 `IDebugProperty2` 父节点和子节点）的所有内容。

 例如，属性通常是可传递的，仅持续到当前堆栈帧。 另一方面，只要值保留在内存中， [由 IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) 接口表示的引用就持续。

 IDE 可以使用 接口 `IDebugProperty2` 让用户能够运行时浏览和修改属性。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)

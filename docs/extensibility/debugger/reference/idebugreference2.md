---
description: 此接口表示对堆栈帧属性或其他某些属性的引用。
title: IDebugReference2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugReference2
helpviewer_keywords:
- IDebugReference2 interface
ms.assetid: 3cfed312-f532-4bce-84a5-1677c14567d7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: cb94ceba197e0006dee98392df01f836c45692c9
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665401"
---
# <a name="idebugreference2"></a>IDebugReference2
此接口表示对堆栈帧属性或其他某些属性的引用。

> [!NOTE]
> `IDebugReference2` 保留供将来使用，其所有方法都应返回 `E_NOTIMPL` 。

## <a name="syntax"></a>语法

```
IDebugReference2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 DE 实现此接口来表示对特定值类型的引用。 例如，该值可以是表达式计算结果的数值、用于显示内存的内存上下文或寄存器及其值的列表。

## <a name="notes-for-callers"></a>调用方说明
 调用 [GetReference](../../../extensibility/debugger/reference/idebugproperty2-getreference.md) 以获取此接口。 [GetParent](../../../extensibility/debugger/reference/idebugreference2-getparent.md) 和 [GetDerivedMostReference](../../../extensibility/debugger/reference/idebugreference2-getderivedmostreference.md) 也返回此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法 `IDebugReference2` 。

|方法|说明|
|------------|-----------------|
|[GetReferenceInfo](../../../extensibility/debugger/reference/idebugreference2-getreferenceinfo.md)|获取 [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md) 引用的结构。|
|[SetValueAsString](../../../extensibility/debugger/reference/idebugreference2-setvalueasstring.md)|从字符串设置此引用的值。|
|[SetValueAsReference](../../../extensibility/debugger/reference/idebugreference2-setvalueasreference.md)|从另一个引用设置此引用的值。|
|[EnumChildren](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md)|枚举此引用的子对象。|
|[GetParent](../../../extensibility/debugger/reference/idebugreference2-getparent.md)|获取此引用的父级。|
|[GetDerivedMostReference](../../../extensibility/debugger/reference/idebugreference2-getderivedmostreference.md)|获取此引用的最派生引用。|
|[GetMemoryBytes](../../../extensibility/debugger/reference/idebugreference2-getmemorybytes.md)|获取此引用引用的内存字节数。|
|[GetMemoryContext](../../../extensibility/debugger/reference/idebugreference2-getmemorycontext.md)|获取此引用的内存上下文。|
|[GetSize](../../../extensibility/debugger/reference/idebugreference2-getsize.md)|获取此引用的大小（以字节为单位）。|
|[SetReferenceType](../../../extensibility/debugger/reference/idebugreference2-setreferencetype.md)|设置此引用类型。|
|[比较](../../../extensibility/debugger/reference/idebugreference2-compare.md)|将此引用与另一个引用进行比较。|

## <a name="remarks"></a>备注

> [!NOTE]
> 尽管 可以表示此类实体，但不应将"property"的这种使用与表示类的成员变量 `IDebugReference2` 混淆。

- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) 表示属性，而 表示对属性的引用，通常是对正在调试的程序 `IDebugReference2` 中的对象的引用。

 属性和引用之间的主要区别在于属性引用对象的命名实例，而引用则引用未命名的实例。 例如，属性可能通过 引用程序堆中的对象 `"a.b"` 。 另一个属性可以引用与 相同的对象 `"c.d"` 。 引用此属性的方式要求 或 `"a.b"` `"c.d"` 在范围内。 对此同一对象的引用是无名称的;只要该对象的内存有效，就可以引用 该对象。

 `IDebugProperty2`可以将接口视为具有名称、类型和地址的值。 另 `IDebugReference2` 一方面，可以将 视为类型和地址。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [GetReference](../../../extensibility/debugger/reference/idebugproperty2-getreference.md)

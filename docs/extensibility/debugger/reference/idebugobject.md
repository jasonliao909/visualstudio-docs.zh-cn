---
description: 此接口表示联编程序创建的对象，用于封装符号和表达式的值。
title: IDebugObject |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject
helpviewer_keywords:
- IDebugObject interface
ms.assetid: 05cd8bf4-c9ee-4b49-b782-2263c33067d6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 1232cd198e9f6db0317eb25d6acc2e0b36eece57e5dce0e0c6906ca88e418c65
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121451778"
---
# <a name="idebugobject"></a>IDebugObject
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式计算器的方法已弃用。 有关实现 CLR 表达式计算器的信息，请参阅 [Clr 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 此接口表示联编程序创建的对象，用于封装符号和表达式的值。

## <a name="syntax"></a>语法

```
IDebugObject : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 表达式计算器实现此接口来表示对象。

## <a name="notes-for-callers"></a>调用方说明
 此接口是表达式计算器在分析的表达式中使用的所有对象的基类。 它通过调用 [Bind](../../../extensibility/debugger/reference/idebugbinder-bind.md) 方法返回。 [QueryInterface](/cpp/atl/queryinterface) 从此接口获取更专用的接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法 `IDebugObject` 。

|方法|说明|
|------------|-----------------|
|[GetSize](../../../extensibility/debugger/reference/idebugobject-getsize.md)|获取对象的大小。|
|[GetValue](../../../extensibility/debugger/reference/idebugobject-getvalue.md)|获取作为连续字节序列的对象的值。|
|[SetValue](../../../extensibility/debugger/reference/idebugobject-setvalue.md)|从连续的字节序列中设置对象的值。|
|[SetReferenceValue](../../../extensibility/debugger/reference/idebugobject-setreferencevalue.md)|设置此对象的引用值。|
|[GetMemoryContext](../../../extensibility/debugger/reference/idebugobject-getmemorycontext.md)|获取表示对象的值地址的内存上下文。|
|[GetManagedDebugObject](../../../extensibility/debugger/reference/idebugobject-getmanageddebugobject.md)|在调试引擎的地址空间中创建托管对象的副本。|
|[IsNullReference](../../../extensibility/debugger/reference/idebugobject-isnullreference.md)|测试此对象是否为空引用。|
|[IsEqual](../../../extensibility/debugger/reference/idebugobject-isequal.md)|将一个对象与此对象进行比较。|
|[IsReadOnly](../../../extensibility/debugger/reference/idebugobject-isreadonly.md)|确定此对象是否为只读。|
|[IsProxy](../../../extensibility/debugger/reference/idebugobject-isproxy.md)|确定对象是否为透明代理。|

## <a name="remarks"></a>备注
 表达式计算器使用此接口作为基类来表示分析树中的对象。

## <a name="requirements"></a>要求
 标头： ee。h

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [表达式计算接口](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [GetElement](../../../extensibility/debugger/reference/idebugarrayobject-getelement.md)
- [绑定](../../../extensibility/debugger/reference/idebugbinder-bind.md)

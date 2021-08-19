---
description: 此接口表示联编程序为封装符号和表达式的值而创建的对象。
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
ms.openlocfilehash: 8d7fdb6e4cbb3a5491a34f404bc7c903de85a147
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122133102"
---
# <a name="idebugobject"></a>IDebugObject
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式计算器的方法已弃用。 有关实现 CLR 表达式评估器的信息，请参阅 [CLR 表达式评估器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式评估器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 此接口表示联编程序为封装符号和表达式的值而创建的对象。

## <a name="syntax"></a>语法

```
IDebugObject : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 表达式计算程序实现此接口来表示 对象。

## <a name="notes-for-callers"></a>调用方说明
 此接口是表达式计算程序在分析表达式中使用的所有对象的基类。 它通过调用 Bind 方法 [返回](../../../extensibility/debugger/reference/idebugbinder-bind.md) 。 [QueryInterface](/cpp/atl/queryinterface) 从此接口获取更专用的接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法 `IDebugObject` 。

|方法|说明|
|------------|-----------------|
|[GetSize](../../../extensibility/debugger/reference/idebugobject-getsize.md)|获取 对象的大小。|
|[GetValue](../../../extensibility/debugger/reference/idebugobject-getvalue.md)|获取 对象的值作为连续的字节序列。|
|[SetValue](../../../extensibility/debugger/reference/idebugobject-setvalue.md)|从连续的字节序列设置 对象的值。|
|[SetReferenceValue](../../../extensibility/debugger/reference/idebugobject-setreferencevalue.md)|设置此 对象的引用值。|
|[GetMemoryContext](../../../extensibility/debugger/reference/idebugobject-getmemorycontext.md)|获取表示 对象的值的地址的内存上下文。|
|[GetManagedDebugObject](../../../extensibility/debugger/reference/idebugobject-getmanageddebugobject.md)|在调试引擎的地址空间中创建托管对象的副本。|
|[IsNullReference](../../../extensibility/debugger/reference/idebugobject-isnullreference.md)|测试此对象是否是空引用。|
|[IsEqual](../../../extensibility/debugger/reference/idebugobject-isequal.md)|将对象与此对象进行比较。|
|[IsReadOnly](../../../extensibility/debugger/reference/idebugobject-isreadonly.md)|确定此对象是否为只读。|
|[IsProxy](../../../extensibility/debugger/reference/idebugobject-isproxy.md)|确定对象是否透明代理。|

## <a name="remarks"></a>备注
 表达式计算程序使用此接口作为基类来表示分析树中的对象。

## <a name="requirements"></a>要求
 标头：ee.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [表达式计算接口](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [GetElement](../../../extensibility/debugger/reference/idebugarrayobject-getelement.md)
- [绑定](../../../extensibility/debugger/reference/idebugbinder-bind.md)

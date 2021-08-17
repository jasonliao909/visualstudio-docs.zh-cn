---
description: 此接口表示内存的字节数。
title: IDebugMemoryBytes2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMemoryBytes2
helpviewer_keywords:
- IDebugMemoryBytes2 interface
ms.assetid: d7647575-0e06-4190-88f5-ca40b82209a4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: add2f353b432d5a7a935a7206ece2113382182ca06aa0755c084fe8123fd7298
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121417088"
---
# <a name="idebugmemorybytes2"></a>IDebugMemoryBytes2
此接口表示内存的字节数。

## <a name="syntax"></a>语法

```
IDebugMemoryBytes2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 调试引擎 (DE) 实现此接口，以表示内存中的字节数。

## <a name="notes-for-callers"></a>调用方说明
- [GetMemoryBytes](../../../extensibility/debugger/reference/idebugprogram2-getmemorybytes.md) 返回此接口以提供对系统内存的访问。 [GetMemoryBytes](../../../extensibility/debugger/reference/idebugproperty2-getmemorybytes.md) 和 [GetMemoryBytes](../../../extensibility/debugger/reference/idebugreference2-getmemorybytes.md) 返回此接口以提供对对象的字节的访问。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法 `IDebugMemoryBytes2` 。

|方法|说明|
|------------|-----------------|
|[ReadAt](../../../extensibility/debugger/reference/idebugmemorybytes2-readat.md)|读取从给定位置开始的字节序列。|
|[WriteAt](../../../extensibility/debugger/reference/idebugmemorybytes2-writeat.md)|写入 `dwCount` 字节，从开始 `pStartContext` 。|
|[GetSize](../../../extensibility/debugger/reference/idebugmemorybytes2-getsize.md)|获取此接口所表示的内存的大小（以字节为单位）。|

## <a name="remarks"></a>备注
 对于属性，表示数组的 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) 接口提供 `IDebugMemoryBytes2` 用于访问该数组中的值的接口。

 Visual Studio 的 **内存视图** 调用 [GetMemoryBytes](../../../extensibility/debugger/reference/idebugprogram2-getmemorybytes.md)来检索 `IDebugMemoryBytes2` 用于访问系统内存的接口。 要访问的地址是通过将作为地址输入到内存视图的表达式进行分析来获取的，然后使用 [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) 来计算分析的表达式以获取 `IDebugProperty2` 接口。 对 [GetMemoryContext](../../../extensibility/debugger/reference/idebugproperty2-getmemorycontext.md) 的调用将返回描述内存地址的 [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) 。 然后，将此内存上下文传递给 [ReadAt](../../../extensibility/debugger/reference/idebugmemorybytes2-readat.md) 和 [WriteAt](../../../extensibility/debugger/reference/idebugmemorybytes2-writeat.md)。

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetMemoryBytes](../../../extensibility/debugger/reference/idebugprogram2-getmemorybytes.md)
- [GetMemoryBytes](../../../extensibility/debugger/reference/idebugproperty2-getmemorybytes.md)
- [GetMemoryBytes](../../../extensibility/debugger/reference/idebugreference2-getmemorybytes.md)
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)

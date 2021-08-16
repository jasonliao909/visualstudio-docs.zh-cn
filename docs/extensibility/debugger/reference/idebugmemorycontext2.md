---
description: 此接口表示运行正在调试的程序计算机的地址空间中的位置。
title: IDebugMemoryContext2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMemoryContext2
helpviewer_keywords:
- IDebugMemoryContext2 interface
ms.assetid: 3a544c8b-11dc-46bb-8549-261e4ac5bbc4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: e004939d27cbf579143716b1cc49968c1f520e7176492608706a5c0f283e6ded
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121433757"
---
# <a name="idebugmemorycontext2"></a>IDebugMemoryContext2
此接口表示运行正在调试的程序计算机的地址空间中的位置。

## <a name="syntax"></a>语法

```
IDebugMemoryContext2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 调试引擎 (DE) 实现此接口来表示内存中的地址。

## <a name="notes-for-callers"></a>调用方说明
 调用 [GetMemoryContext](../../../extensibility/debugger/reference/idebugproperty2-getmemorycontext.md) 或 [GetMemoryContext](../../../extensibility/debugger/reference/idebugreference2-getmemorycontext.md) 将返回此接口。 此外，对 [Add](../../../extensibility/debugger/reference/idebugmemorycontext2-add.md) 和 Subtract 的 [调用](../../../extensibility/debugger/reference/idebugmemorycontext2-subtract.md) 在应用适当的算术运算后返回此接口的新副本。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法 `IDebugMemoryContext2` 。

|方法|说明|
|------------|-----------------|
|[GetName](../../../extensibility/debugger/reference/idebugmemorycontext2-getname.md)|获取此上下文的用户可显示名称。|
|[GetInfo](../../../extensibility/debugger/reference/idebugmemorycontext2-getinfo.md)|获取描述此上下文的信息。|
|[添加](../../../extensibility/debugger/reference/idebugmemorycontext2-add.md)|将指定的值添加到当前上下文的地址以创建新上下文。|
|[减](../../../extensibility/debugger/reference/idebugmemorycontext2-subtract.md)|从当前上下文的地址中减去指定值以创建新上下文。|
|[比较](../../../extensibility/debugger/reference/idebugmemorycontext2-compare.md)|按比较标志指示的方式比较两个上下文。|

## <a name="remarks"></a>备注
 Visual Studio **的"** 内存"窗口调用 [GetMemoryContext](../../../extensibility/debugger/reference/idebugproperty2-getmemorycontext.md)以获取接口，该接口包含用于内存 `IDebugMemoryContext2` 地址的已计算表达式。 然后将此上下文传递给 [ReadAt](../../../extensibility/debugger/reference/idebugmemorybytes2-readat.md) 和 [WriteAt，](../../../extensibility/debugger/reference/idebugmemorybytes2-writeat.md) 以指定要读取或写入的地址。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetMemoryContext](../../../extensibility/debugger/reference/idebugproperty2-getmemorycontext.md)
- [GetMemoryContext](../../../extensibility/debugger/reference/idebugreference2-getmemorycontext.md)
- [ReadAt](../../../extensibility/debugger/reference/idebugmemorybytes2-readat.md)
- [WriteAt](../../../extensibility/debugger/reference/idebugmemorybytes2-writeat.md)

---
description: 此接口表示指令流。
title: IDebugDisassemblyStream2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDisassemblyStream2
helpviewer_keywords:
- IDebugDisassemblyStream2 interface
ms.assetid: b03cab0c-3f0b-4cc6-88dc-acb3b48c567a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: e42d8019c854ca800dd35028fe82a158bc3a428e
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122119511"
---
# <a name="idebugdisassemblystream2"></a>IDebugDisassemblyStream2
此接口表示指令流。

## <a name="syntax"></a>语法

```
IDebugDisassemblyStream2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 调试引擎实现此接口以支持程序代码的反汇编。

## <a name="notes-for-callers"></a>调用方说明
 对 [GetDisassemblyStream](../../../extensibility/debugger/reference/idebugprogram2-getdisassemblystream.md) 方法的调用将返回此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法 `IDebugDisassemblyStream2` 。

|方法|说明|
|------------|-----------------|
|[读取](../../../extensibility/debugger/reference/idebugdisassemblystream2-read.md)|读取从反汇编流中的当前位置开始的说明。|
|[Seek](../../../extensibility/debugger/reference/idebugdisassemblystream2-seek.md)|将反汇编流中的读取指针相对于指定位置移动给定数量的指令。|
|[GetCodeLocationId](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodelocationid.md)|返回特定代码上下文的代码位置标识符。|
|[GetCodeContext](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodecontext.md)|返回对应于指定代码位置标识符的代码上下文对象。|
|[GetCurrentLocation](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcurrentlocation.md)|返回表示当前代码位置的代码位置标识符。|
|[GetDocument](../../../extensibility/debugger/reference/idebugdisassemblystream2-getdocument.md)|获取与此反汇编流关联的源文档。|
|[GetScope](../../../extensibility/debugger/reference/idebugdisassemblystream2-getscope.md)|获取此反汇编流的作用域。|
|[GetSize](../../../extensibility/debugger/reference/idebugdisassemblystream2-getsize.md)|获取此反汇编流的大小。|

## <a name="remarks"></a>备注
 可创建反汇编流来表示整个地址空间，或只表示空间中的函数或模块。 每个指令都由对 Read 方法的调用返回的 [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md) [结构](../../../extensibility/debugger/reference/idebugdisassemblystream2-read.md) 表示。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetDisassemblyStream](../../../extensibility/debugger/reference/idebugprogram2-getdisassemblystream.md)
- [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)

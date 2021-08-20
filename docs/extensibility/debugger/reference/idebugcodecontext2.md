---
description: 此接口表示代码指令的起始位置。
title: IDebugCodeContext2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCodeContext2
helpviewer_keywords:
- IDebugCodeContext2 interface
ms.assetid: 3670439e-2171-405d-9d77-dedb0f1cba93
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: da3fdc1c8f3c9c836519ba45d39df0aeca326d05
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122104126"
---
# <a name="idebugcodecontext2"></a>IDebugCodeContext2
此接口表示代码指令的起始位置。 对于目前大多数运行时体系结构，可以将代码上下文视为程序执行流中的地址。

## <a name="syntax"></a>语法

```
IDebugCodeContext2 : IDebugMemoryContext2
```

## <a name="notes-for-implementers"></a>实现者说明
 调试引擎实现此接口，以将代码指令的位置与文档位置关联。

## <a name="notes-for-callers"></a>调用方说明
 许多接口上的方法返回此接口，通常是 [GetCodeContext](../../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md)。 它还广泛用于 [IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md) 接口以及断点解析信息。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了 [IDebugMemoryContext2 接口](../../../extensibility/debugger/reference/idebugmemorycontext2.md) 上的方法外，此接口还实现以下方法：

|方法|说明|
|------------|-----------------|
|[GetDocumentContext](../../../extensibility/debugger/reference/idebugcodecontext2-getdocumentcontext.md)|获取与活动代码上下文对应的文档上下文。|
|[GetLanguageInfo](../../../extensibility/debugger/reference/idebugcodecontext2-getlanguageinfo.md)|获取此代码上下文的语言信息。|

## <a name="remarks"></a>备注
 接口和 `IDebugCodeContext2` [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) 接口之间的主要区别在于 始终与指令 `IDebugCodeContext2` 对齐。 这意味着 始终指向指令的开头，而 可能指向运行时体系结构中的任何 `IDebugCodeContext2` `IDebugMemoryContext2` 内存字节。 `IDebugCodeContext2` 按指令递增，而不是按基本存储大小递增 (字节) 。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [GetDisassemblyStream](../../../extensibility/debugger/reference/idebugprogram2-getdisassemblystream.md)
- [CanSetNextStatement](../../../extensibility/debugger/reference/idebugthread2-cansetnextstatement.md)
- [SetNextStatement](../../../extensibility/debugger/reference/idebugthread2-setnextstatement.md)
- [GetCodeContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getcodecontext.md)
- [GetCodeContext](../../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md)
- [下一页](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-next.md)
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)

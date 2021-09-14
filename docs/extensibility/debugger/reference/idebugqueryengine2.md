---
description: 此接口使会话调试管理器 (SDM) 检索表示调试引擎 (DE) 的接口。
title: IDebugQueryEngine2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugQueryEngine2
helpviewer_keywords:
- IDebugQueryEngine2 interface
ms.assetid: 8f0e1838-a818-4459-9138-a3dceb7408de
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: bf399a8ccf018e8e18c18ba0af2b54a0e5b948c9
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664470"
---
# <a name="idebugqueryengine2"></a>IDebugQueryEngine2
此接口使会话调试管理器 (SDM) 检索表示调试引擎 (DE) 的接口。

## <a name="syntax"></a>语法

```
IDebugQueryEngine2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 DE 在实现最常见的 DE 接口 (（如 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)、 [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)和 [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)) ）的对象上实现了此接口，以允许访问 DE 自身的 [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md) 接口。

## <a name="notes-for-callers"></a>调用方说明
 在典型的 DE 接口上调用 [QueryInterface](/cpp/atl/queryinterface) 以获取此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法 `IDebugQueryEngine2` 。

|方法|说明|
|------------|-----------------|
|[GetEngineInterface](../../../extensibility/debugger/reference/idebugqueryengine2-getengineinterface.md)|获取 (DE) 接口的自定义调试引擎。|

## <a name="remarks"></a>备注
 在实现 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) 接口的对象中，通常会实现此接口，以便支持因果关系单步执行函数;也就是说，当调试器跳出某个函数时，要执行的下一个函数可能不是堆栈上的上一个函数，而是另一个线程中的函数。 有关 "因果关系" 的定义，请参阅[Visual Studio 调试器术语表](../../../extensibility/debugger/reference/visual-studio-debugger-glossary.md)。

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)

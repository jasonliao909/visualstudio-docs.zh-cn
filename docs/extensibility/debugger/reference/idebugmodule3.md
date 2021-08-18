---
description: 此接口表示支持符号和 JustMyCode 状态备用位置的模块。
title: IDebugModule3 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugModule3
helpviewer_keywords:
- IDebugModule3 interface
ms.assetid: 44f8e96e-9c59-4ffc-9a08-9c908a0e4de7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 11b6db77e947ae8cb2ace6353b3f55aa8db48664
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122078838"
---
# <a name="idebugmodule3"></a>IDebugModule3
此接口表示支持符号和 JustMyCode 状态备用位置的模块。

## <a name="syntax"></a>语法

```
IDebugModule3 : IDebugModule2
```

## <a name="notes-for-implementers"></a>实现者说明
 调试引擎 (DE) 实现此接口以支持符号的备用位置，并处理 JustMyCode 状态 (请参阅[Visual Studio 调试](../../../extensibility/debugger/reference/visual-studio-debugger-glossary.md)器词汇表，了解"JustMyCode") 的定义。

## <a name="notes-for-callers"></a>调用方说明
 调用 [GetSymbolSearchInfo 将](../../../extensibility/debugger/reference/idebugsymbolsearchevent2-getsymbolsearchinfo.md) 返回此接口。 DE 使用 Event 方法将 [IDebugSymbolSearchEvent2](../../../extensibility/debugger/reference/idebugsymbolsearchevent2.md) (SDM) 会话调试 [管理器](../../../extensibility/debugger/reference/idebugeventcallback2-event.md) 。 此外，对[IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)接口上的[QueryInterface](/cpp/atl/queryinterface)的调用将返回此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了 [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md) 接口上的方法外，此接口还实现以下方法：

|方法|说明|
|------------|-----------------|
|[GetSymbolInfo](../../../extensibility/debugger/reference/idebugmodule3-getsymbolinfo.md)|返回搜索符号的路径列表以及搜索每个路径的结果。|
|[LoadSymbols](../../../extensibility/debugger/reference/idebugmodule3-loadsymbols.md)|加载并初始化当前模块的符号。|
|[IsUserCode](../../../extensibility/debugger/reference/idebugmodule3-isusercode.md)|返回指定模块是否表示用户代码的标志。|
|[SetJustMyCodeState](../../../extensibility/debugger/reference/idebugmodule3-setjustmycodestate.md)|指定是否应当将模块视为用户代码。|

## <a name="remarks"></a>备注
 Visual Studio是此接口的典型使用者。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)
- [IDebugSymbolSearchEvent2](../../../extensibility/debugger/reference/idebugsymbolsearchevent2.md)
- [GetSymbolSearchInfo](../../../extensibility/debugger/reference/idebugsymbolsearchevent2-getsymbolsearchinfo.md)

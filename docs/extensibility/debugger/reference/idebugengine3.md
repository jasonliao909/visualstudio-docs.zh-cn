---
description: 表示一个调试引擎 (DE) 控制一个或多个模块的调试。
title: IDebugEngine3 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine3
helpviewer_keywords:
- IDebugEngine3 interface
ms.assetid: 8bdf4bb7-3b5d-4991-8981-772d4f6bb656
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: f997a177164c66ac116db407db6e3edfcc571b0a
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664829"
---
# <a name="idebugengine3"></a>IDebugEngine3
表示一个调试引擎 (DE) 控制一个或多个模块的调试。

## <a name="syntax"></a>语法

```
IDebugEngine3 : IDebugEngine2
```

## <a name="notes-for-implementers"></a>实现者说明
 此接口由自定义 DE (如果支持符号) 启用 JustMyCode 状态。 如果 DE 支持符号和 JustMyCode，则必须实现此接口。

## <a name="notes-for-callers"></a>调用方说明
 此接口由会话调试管理器 (SDM) ，以传递用于加载符号的位置的用户选项。 在实例化引擎时，也会调用它来设置引擎的 GUID (此 GUID 基于从引擎注册到) 。 SDM 还调用此接口来设置 JustMyCode 状态，以及将调试器已知的所有异常设置为指定状态。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了从 [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)继承的方法之外， `IDebugEngine3` 接口还公开了以下方法。

|方法|说明|
|------------|-----------------|
|[SetSymbolPath](../../../extensibility/debugger/reference/idebugengine3-setsymbolpath.md)|设置 DE 用于搜索调试符号的路径。|
|[LoadSymbols](../../../extensibility/debugger/reference/idebugengine3-loadsymbols.md)|加载尚未加载其符号的所有模块的符号。|
|[SetJustMyCodeState](../../../extensibility/debugger/reference/idebugengine3-setjustmycodestate.md)|告知 DE JustMyCode 信息。|
|[SetEngineGuid](../../../extensibility/debugger/reference/idebugengine3-setengineguid.md)|从指标设置 DE GUID。|
|[SetAllExceptions](../../../extensibility/debugger/reference/idebugengine3-setallexceptions.md)|将当前未完成的所有异常设置为指定状态。|

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)

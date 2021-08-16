---
description: 此接口表示一个模块，即程序的可执行单元（如 DLL）。
title: IDebugModule2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugModule2
helpviewer_keywords:
- IDebugModule2 interface
ms.assetid: 24c2a126-f4ab-4891-8509-8ef99b994c08
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: d6829db5b10ef69a67891847ef763b80b8f710c0e6dfef78d09ace714839c129
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121451817"
---
# <a name="idebugmodule2"></a>IDebugModule2
此接口表示一个模块，即程序的可执行单元（如 DLL）。

## <a name="syntax"></a>语法

```
IDebugModule2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 调试引擎 (DE) 实现此接口来表示模块并提供对该模块的信息的访问。

## <a name="notes-for-callers"></a>调用方说明
 对 [GetModule](../../../extensibility/debugger/reference/idebugmoduleloadevent2-getmodule.md) 的调用返回此接口。 DE 使用[事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)方法将[IDebugModuleLoadEvent2](../../../extensibility/debugger/reference/idebugmoduleloadevent2.md)接口发送到会话调试管理器 (SDM) 。

 此接口还可以在 [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md) 结构中返回， (通过调用 [EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)) 返回。

- [接下来](../../../extensibility/debugger/reference/ienumdebugmodules2-next.md) ，还返回此接口 ([EnumModules](../../../extensibility/debugger/reference/idebugprogram2-enummodules.md) 返回 [IEnumDebugModules2](../../../extensibility/debugger/reference/ienumdebugmodules2.md) 接口) 。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法 `IDebugModule2` 。

|方法|说明|
|------------|-----------------|
|[GetInfo](../../../extensibility/debugger/reference/idebugmodule2-getinfo.md)|获取描述此模块的 [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md) 。|
|[ReloadSymbols_Deprecated](../../../extensibility/debugger/reference/idebugmodule2-reloadsymbols-deprecated.md)|已过时。 请勿使用。 重新加载此模块的符号。|

## <a name="remarks"></a>备注
 模块信息可以显示在 IDE 的 " **模块** " 窗口中。

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)
- [GetModule](../../../extensibility/debugger/reference/idebugmoduleloadevent2-getmodule.md)
- [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)
- [IEnumDebugModules2](../../../extensibility/debugger/reference/ienumdebugmodules2.md)

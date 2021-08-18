---
description: 此接口由调试引擎 DE (DE) 在加载或卸载模块时 (SDM) 发送到会话调试管理器。
title: IDebugModuleLoadEvent2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugModuleLoadEvent2
helpviewer_keywords:
- IDebugModuleLoadEvent2 interface
ms.assetid: 7d26fb23-5d49-4ba7-b7c5-3aed4d7be81e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: e147515a761bca80eaae06f367bf798aa63fe8cd
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122035028"
---
# <a name="idebugmoduleloadevent2"></a>IDebugModuleLoadEvent2
此接口由调试引擎 DE (DE) 在加载或卸载模块时 (SDM) 发送到会话调试管理器。

## <a name="syntax"></a>语法

```
IDebugModuleLoadEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 DE 实现此接口以报告模块已加载或卸载。 必须在与此接口相同的对象上实现 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) 接口。 SDM 使用 [QueryInterface](/cpp/atl/queryinterface) 访问 `IDebugEvent2` 接口。

## <a name="notes-for-callers"></a>调用方说明
 DE 创建并发送此事件对象，以报告模块已加载或卸载。 事件是通过使用 SDM 在附加到正在调试的程序时提供的 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) 回调函数发送的。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的 方法 `IDebugModuleLoadEvent2` 。

|方法|说明|
|------------|-----------------|
|[GetModule](../../../extensibility/debugger/reference/idebugmoduleloadevent2-getmodule.md)|获取正在加载或卸载的模块。|

## <a name="remarks"></a>备注
 Visual Studio此事件使"模块 **"** 窗口保持最新。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)

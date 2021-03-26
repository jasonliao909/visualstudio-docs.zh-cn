---
description: 当加载或卸载模块时，调试引擎会将此接口 (DE) 发送到会话调试管理器 (SDM) 。
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
ms.workload:
- vssdk
ms.openlocfilehash: f6030e5962c0544a63b7b9658622447324a15792
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105065354"
---
# <a name="idebugmoduleloadevent2"></a>IDebugModuleLoadEvent2
当加载或卸载模块时，调试引擎会将此接口 (DE) 发送到会话调试管理器 (SDM) 。

## <a name="syntax"></a>语法

```
IDebugModuleLoadEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 DE 实现此接口，报告已加载或卸载模块。 必须在与此接口相同的对象上实现 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) 接口。 SDM 使用 [QueryInterface](/cpp/atl/queryinterface) 访问 `IDebugEvent2` 接口。

## <a name="notes-for-callers"></a>调用方说明
 DE 创建此事件对象并将其发送给报告已加载或卸载的模块。 此事件在附加到正在调试的程序时，使用 SDM 提供的 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) 回调函数发送。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法 `IDebugModuleLoadEvent2` 。

|方法|说明|
|------------|-----------------|
|[GetModule](../../../extensibility/debugger/reference/idebugmoduleloadevent2-getmodule.md)|获取正在加载或卸载的模块。|

## <a name="remarks"></a>备注
 Visual Studio 使用此事件将 " **模块** " 窗口保持为最新状态。

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)

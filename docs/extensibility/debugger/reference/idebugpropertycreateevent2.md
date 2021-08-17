---
description: 当调试引擎创建与特定文档关联的属性时，此接口由调试引擎 (DE) 发送到会话调试管理器 (SDM) 。
title: IDebugPropertyCreateEvent2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPropertyCreateEvent2
helpviewer_keywords:
- IDebugPropertyCreateEvent2 interface
ms.assetid: 33b3082b-a42e-488a-a1e4-dadf506f922c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: edd4b94de54221108962ce6b948fb4a782d57f4cc8a08922c20051a29ed370fd
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121402345"
---
# <a name="idebugpropertycreateevent2"></a>IDebugPropertyCreateEvent2
当调试引擎创建与特定文档关联的属性时，此接口由调试引擎 (DE) 发送到会话调试管理器 (SDM) 。

## <a name="syntax"></a>语法

```
IDebugPropertyCreateEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 DE 实现此接口，报告已创建属性。 必须在与此接口相同的对象上实现 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) 接口。 SDM 使用 [QueryInterface](/cpp/atl/queryinterface) 访问 `IDebugEvent2` 接口。 如果 DE 创建了与已加载或创建的脚本关联的属性，并且该脚本需要在 IDE 中显示，则实现此接口。

## <a name="notes-for-callers"></a>调用方说明
 DE 创建此事件对象并将其发送给报告已创建的属性。 此事件在附加到正在调试的程序时，使用 SDM 提供的 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) 回调函数发送。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了接口的方法 `IDebugPropertyCreateEvent2` 。

|方法|说明|
|------------|-----------------|
|[GetDebugProperty](../../../extensibility/debugger/reference/idebugpropertycreateevent2-getdebugproperty.md)|获取新属性。|

## <a name="remarks"></a>备注
 如果某个属性具有与之关联的特定文档或脚本，则 DE 可以将此事件发送到 SDM，以便使用文档名称更新 " **脚本文档** " 窗口。 SDM 将使用参数调用 [GetExtendedInfo](../../../extensibility/debugger/reference/idebugproperty2-getextendedinfo.md) `guidDocument` ，以检索 `VARIANT` 包含 [IUnknown](/cpp/atl/iunknown) 指针的。 SDM 将对此指针调用 [QueryInterface](/cpp/atl/queryinterface) ，以检索用于更新 **脚本文档** 窗口的 [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)接口。

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)

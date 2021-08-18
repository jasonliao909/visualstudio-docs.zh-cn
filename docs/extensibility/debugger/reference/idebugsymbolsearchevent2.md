---
description: 此接口由调试引擎 (DE) ，以指示已加载正在调试的模块的调试符号。
title: IDebugSymbolSearchEvent2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugSymbolSearchEvent2
helpviewer_keywords:
- IDebugSymbolSearchEvent2
ms.assetid: 9b946d55-ff85-44eb-b40a-efbf8282eafd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: d61bcc7c77295b59bc6cc66cd1cf9aac3486e6c6
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122103645"
---
# <a name="idebugsymbolsearchevent2"></a>IDebugSymbolSearchEvent2
此接口由调试引擎 (DE) ，以指示已加载正在调试的模块的调试符号。

## <a name="syntax"></a>语法

```
IDebugSymbolSearchEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 DE 实现此接口以报告模块的符号已加载。 必须在与此接口相同的对象上实现 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) 接口。 SDM 使用 [QueryInterface](/cpp/atl/queryinterface) 访问 `IDebugEvent2` 接口。

## <a name="notes-for-callers"></a>调用方说明
 DE 创建并发送此事件对象，以报告模块的符号已加载。 事件是通过使用 SDM 在附加到正在调试的程序时提供的 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) 回调函数发送的。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 `IDebugSymbolSearchEvent2`接口公开以下方法。

|方法|说明|
|------------|-----------------|
|[GetSymbolSearchInfo](../../../extensibility/debugger/reference/idebugsymbolsearchevent2-getsymbolsearchinfo.md)|检索有关符号搜索结果的信息。|

## <a name="remarks"></a>备注
 即使无法加载符号，也会发送此事件。 调用 `IDebugSymbolSearchEvent2::GetSymbolSearchInfo` 允许此事件的处理程序确定模块是否实际具有任何符号。

 Visual Studio此事件在"模块"窗口中更新已加载 **符号的状态。**

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)

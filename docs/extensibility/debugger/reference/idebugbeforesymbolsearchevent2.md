---
description: 调试引擎 (DE) 将此接口发送到会话调试管理器 (SDM) ，以便在符号加载过程中设置状态栏消息。
title: IDebugBeforeSymbolSearchEvent2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugBeforeSymbolSearchEvent2 interface
ms.assetid: 679fd7b1-765a-41a8-a046-63240c09a499
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: fdf292a309e514f5b437b129bbfc6ee125df8269
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102167732"
---
# <a name="idebugbeforesymbolsearchevent2"></a>IDebugBeforeSymbolSearchEvent2
调试引擎 (DE) 将此接口发送到会话调试管理器 (SDM) ，以便在符号加载过程中设置状态栏消息。

## <a name="syntax"></a>语法

```
IDebugBeforeSymbolSearchEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 当在符号加载过程中必须设置状态栏消息时，将实现此接口。 此接口仅由使用或是脚本解释器一部分的调试引擎实现。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)接口必须在与此接口相同的对象上实现 (SDM 使用 **QueryInterface** 访问 **IDebugEvent2** 接口) 。

## <a name="notes-for-callers"></a>调用方说明
 如果在符号加载过程中必须设置状态栏消息，则 DE 将创建并发送此事件对象。 使用 SDM 在附加到正在调试的程序时提供的 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) 回调函数发送事件。

## <a name="methods"></a>方法
 下表显示的方法 `IDebugBeforeSymbolSearchEvent2` 。

|方法|说明|
|------------|-----------------|
|[GetModuleName](../../../extensibility/debugger/reference/idebugbeforesymbolsearchevent2-getmodulename.md)|检索当前正在调试的模块的名称。|

## <a name="requirements"></a>要求
 标头： Msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

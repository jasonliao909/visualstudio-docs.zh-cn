---
description: 调试引擎 (DE) 使用此接口请求加载文档。
title: IDebugActivateDocumentEvent2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugActivateDocumentEvent2
helpviewer_keywords:
- IDebugActivateDocumentEvent2 interface
ms.assetid: 6f37edd7-a48c-4b41-b160-dff9be63a284
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 2e2e1e516774f1acfe4041c58b97e4892aefd242
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122104477"
---
# <a name="idebugactivatedocumentevent2"></a>IDebugActivateDocumentEvent2
调试引擎 (DE) 使用此接口请求加载文档。

## <a name="syntax"></a>语法

```
IDebugActivateDocumentEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 DE 在需要打开源文件时实现此接口。 此接口仅由使用或属于脚本解释器一部分的调试引擎实现。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)接口必须在与此接口相同的对象上实现 (SDM 使用[QueryInterface](/cpp/atl/queryinterface)访问接口 `IDebugEvent2`) 。

## <a name="notes-for-callers"></a>调用方说明
 DE 在需要打开源文件时创建并发送此事件对象。 事件是通过使用 SDM 在附加到正在调试的程序时提供的 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) 回调函数发送的。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法 `IDebugActivateDocumentEvent2` 。

|方法|说明|
|-------------|-----------------|
|[GetDocument](../../../extensibility/debugger/reference/idebugactivatedocumentevent2-getdocument.md)|获取要激活的文档。|
|[GetDocumentContext](../../../extensibility/debugger/reference/idebugactivatedocumentevent2-getdocumentcontext.md)|获取描述文档内位置的文档上下文。|

## <a name="remarks"></a>备注
 使用此接口的典型方案是，如果 HTML 页上的脚本代码中出现分析错误，则脚本 DE 会向 SDM 发送此接口，以便可以显示具有分析错误的文档。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)

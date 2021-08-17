---
description: 此接口枚举当前调试会话中运行的线程。
title: IEnumDebugThreads2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugThreads2
helpviewer_keywords:
- IEnumDebugThreads2
ms.assetid: 1854f078-3b49-42c2-b65b-33e3b506fd63
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: e2f291d02a9420b465681a0e75278d022e14b3cf
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122034781"
---
# <a name="ienumdebugthreads2"></a>IEnumDebugThreads2
此接口枚举当前调试会话中运行的线程。

## <a name="syntax"></a>语法

```
IEnumDebugThreads2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 DE 脚本 (DE) 实现此接口来表示程序中的线程列表。

## <a name="notes-for-callers"></a>调用方说明
 调用 [EnumThreads](../../../extensibility/debugger/reference/idebugprocess2-enumthreads.md) 以获取此接口，该接口表示进程中运行的所有程序中所有线程的列表。 调用 [EnumThreads](../../../extensibility/debugger/reference/idebugprogram2-enumthreads.md) 以获取此接口，该接口表示在程序中运行的线程列表。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法 `IEnumDebugThreads2` 。

|方法|说明|
|------------|-----------------|
|[下一页](../../../extensibility/debugger/reference/ienumdebugthreads2-next.md)|检索枚举序列中的指定线程数。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugthreads2-skip.md)|跳过枚举序列中的指定线程数。|
|[重置](../../../extensibility/debugger/reference/ienumdebugthreads2-reset.md)|将枚举序列重置为开头。|
|[克隆](../../../extensibility/debugger/reference/ienumdebugthreads2-clone.md)|创建一个枚举器，其中包含与当前枚举状态相同的枚举状态。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugthreads2-getcount.md)|获取枚举器中的线程数。|

## <a name="remarks"></a>备注
 Visual Studio获取此接口以更新"线程"窗口，以及获取列表的第一个线程，以便调用"执行[](../../../extensibility/debugger/reference/idebugprocess3-execute.md)["、"继续](../../../extensibility/debugger/reference/idebugprocess3-continue.md)"和"[步骤"。](../../../extensibility/debugger/reference/idebugprocess3-step.md)

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumThreads](../../../extensibility/debugger/reference/idebugprocess2-enumthreads.md)
- [EnumThreads](../../../extensibility/debugger/reference/idebugprogram2-enumthreads.md)
- [步骤](../../../extensibility/debugger/reference/idebugprocess3-step.md)
- [继续](../../../extensibility/debugger/reference/idebugprocess3-continue.md)
- [执行](../../../extensibility/debugger/reference/idebugprocess3-execute.md)

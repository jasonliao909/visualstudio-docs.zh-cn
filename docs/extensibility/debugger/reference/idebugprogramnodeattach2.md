---
description: 允许程序节点通知附加到关联程序的尝试。
title: IDebugProgramNodeAttach2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNodeAttach2
helpviewer_keywords:
- IDebugProgramNodeAttach2 interface
ms.assetid: 46b37ac9-a026-4ad3-997b-f19e2f8deb73
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: e28ca64629d0bdb000a39d5cd4ab040b732730fb
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122096097"
---
# <a name="idebugprogramnodeattach2"></a>IDebugProgramNodeAttach2
允许程序节点通知附加到关联程序的尝试。

## <a name="syntax"></a>语法

```
IDebugProgramNodeAttach2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 在实现 [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) 接口的同一类上实现此接口，以便接收附加操作的通知并提供取消附加操作的机会。

## <a name="notes-for-callers"></a>调用方说明
 通过 `QueryInterface` 在 [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) 对象中调用方法获取此接口。 必须先调用 [OnAttach](../../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md) 方法，然后才能通过 [attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) 方法为程序节点指定停止附加过程的机会。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 此接口实现以下方法：

|方法|说明|
|------------|-----------------|
|[OnAttach](../../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)|附加到关联程序或将附加进程推迟到 [attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) 方法。|

## <a name="remarks"></a>备注
 此接口是不推荐使用的 [Attach_V7](../../../extensibility/debugger/reference/idebugprogramnode2-attach-v7.md) 方法的首选替代项。 所有调试引擎始终都与函数一起加载 `CoCreateInstance` ，也就是说，它们在要调试的程序的地址空间之外进行实例化。

 如果以前实现的 `IDebugProgramNode2::Attach_V7` 方法只是设置 `GUID` 正在调试的程序的，则只需实现 [OnAttach](../../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md) 方法。

 如果以前的 `IDebugProgramNode2::Attach_V7` 方法实现使用了提供的回调接口，则需要将该功能移到 [附加](../../../extensibility/debugger/reference/idebugengine2-attach.md) 方法的实现中，并且 `IDebugProgramNodeAttach2` 无需实现此接口。

## <a name="requirements"></a>要求
 标头： Msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
- [附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)
- [Attach_V7](../../../extensibility/debugger/reference/idebugprogramnode2-attach-v7.md)

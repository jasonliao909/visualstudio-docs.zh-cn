---
description: 此接口允许会话调试管理器 (SDM) 附加到程序并获取与程序关联的程序节点。
title: IDebugProgramEx2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramEx2
helpviewer_keywords:
- IDebugProgramEx2 interface
ms.assetid: 663359ed-635a-4539-addb-0cc52f19d1bd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 1c1cff5e18dfca2838595848c2ae4f18c076441ec51ed78e93e467bdbbca9f8b
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121276394"
---
# <a name="idebugprogramex2"></a>IDebugProgramEx2
此接口允许会话调试管理器 (SDM) 附加到程序并获取与程序关联的程序节点。

## <a name="syntax"></a>语法

```
IDebugProgramEx2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 自定义端口供应商在 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) 接口的同一对象上实现此接口，以便 SDM 附加到程序，同时允许端口供应商跟踪附加到程序的所有会话。 自定义端口供应商可以选择实现此接口。

## <a name="notes-for-callers"></a>调用方说明
 SDM 在接口上调用 [QueryInterface](/cpp/atl/queryinterface) 以获取此接口，以 `IDebugProgram2` 跟踪已附加到程序上的会话。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法 `IDebugProgramEx2` 。

|方法|说明|
|------------|-----------------|
|[附加](../../../extensibility/debugger/reference/idebugprogramex2-attach.md)|将程序附加到会话。|
|[GetProgramNode](../../../extensibility/debugger/reference/idebugprogramex2-getprogramnode.md)|获取与程序关联的程序节点。|

## <a name="remarks"></a>备注
 此接口在 SDM 与程序之间是私有的。

## <a name="requirements"></a>要求
 标头：Portpriv.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)

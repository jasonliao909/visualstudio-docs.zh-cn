---
description: 此接口表示可调试的程序。
title: IDebugProgramNode2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNode2
helpviewer_keywords:
- IDebugProgramNode2 interface
ms.assetid: 80e511d8-9b40-4a85-aa5d-952fa5ee6ae7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 7237d03907a961135a767a246c4f9d291ef17d293b0d04f8020915b8ab0e31e7
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121389561"
---
# <a name="idebugprogramnode2"></a>IDebugProgramNode2
此接口表示可调试的程序。

## <a name="syntax"></a>语法

```
IDebugProgramNode2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 调试引擎 (DE) 或自定义端口供应商实现此接口来表示可调试的程序。 此接口通常在实现 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) 接口的同一对象上实现。 此接口通过调用 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] [PublishProgramNode 注册到](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogramnode.md)。

## <a name="notes-for-callers"></a>调用方说明
 调用 [GetProviderProgramNode](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprogramnode.md) 以返回此接口。 自定义端口供应商通过调用 [AddProgramNode 接收此接口](../../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)。 DE 通过调用 Attach 接收此 [接口](../../../extensibility/debugger/reference/idebugengine2-attach.md)。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法 `IDebugProgramNode2` 。

|方法|说明|
|------------|-----------------|
|[GetProgramName](../../../extensibility/debugger/reference/idebugprogramnode2-getprogramname.md)|获取程序的名称。|
|[GetHostName](../../../extensibility/debugger/reference/idebugprogramnode2-gethostname.md)|获取托管程序的进程的名称。|
|[GetHostPid](../../../extensibility/debugger/reference/idebugprogramnode2-gethostpid.md)|获取托管程序的进程的系统进程标识符。|
|[GetHostMachineName_V7](../../../extensibility/debugger/reference/idebugprogramnode2-gethostmachinename-v7.md)|废弃。 请勿使用。|
|[Attach_V7](../../../extensibility/debugger/reference/idebugprogramnode2-attach-v7.md)|废弃。 请勿使用。 有关替代方法 [，请参阅 IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md) 接口。|
|[GetEngineInfo](../../../extensibility/debugger/reference/idebugprogramnode2-getengineinfo.md)|获取运行此程序的 DE 的名称和标识符。|
|[DetachDebugger_V7](../../../extensibility/debugger/reference/idebugprogramnode2-detachdebugger-v7.md)|废弃。 请勿使用。|

## <a name="remarks"></a>备注
 会话调试管理器 (SDM) 调用 [GetProviderProgramNode](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprogramnode.md) 来获取此接口。

## <a name="requirements"></a>要求
 标头：Msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md)
- [AddProgramNode](../../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)
- [RemoveProgramNode](../../../extensibility/debugger/reference/idebugportnotify2-removeprogramnode.md)
- [附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)
- [GetProviderProgramNode](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprogramnode.md)
- [PublishProgramNode](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogramnode.md)

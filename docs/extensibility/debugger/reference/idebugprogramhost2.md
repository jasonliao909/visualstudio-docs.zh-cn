---
description: 此接口提供主机 (进程) 有关程序的信息。
title: IDebugProgramHost2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramHost2
helpviewer_keywords:
- IDebugProgramHost2 interface
ms.assetid: 2c37b3aa-97a9-4665-8709-edd917f18cb1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 235c36be2fd6ec4ee98b2efc97ee37a0d5077425aaa4f7f2ad62d767e0eb6a67
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121402696"
---
# <a name="idebugprogramhost2"></a>IDebugProgramHost2
此接口提供主机 (进程) 有关程序的信息。

## <a name="syntax"></a>语法

```
IDebugProgramHost2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 调试引擎在 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) 接口的同一对象上实现此接口，以提供有关托管进程的信息。 这是一个可选接口。

## <a name="notes-for-callers"></a>调用方说明
 在 [接口上调用 QueryInterface](/cpp/atl/queryinterface) `IDebugProgram2` 以获取此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法 `IDebugProgramHost2` 。

|方法|说明|
|------------|-----------------|
|[GetHostName](../../../extensibility/debugger/reference/idebugprogramhost2-gethostname.md)|获取此程序的托管进程的标题、友好名称或文件名。|
|[GetHostId](../../../extensibility/debugger/reference/idebugprogramhost2-gethostid.md)|获取此程序的承载进程的进程标识符。|
|[GetHostMachineName](../../../extensibility/debugger/reference/idebugprogramhost2-gethostmachinename.md)|获取运行此程序的托管进程所运行计算机的名称。|

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)

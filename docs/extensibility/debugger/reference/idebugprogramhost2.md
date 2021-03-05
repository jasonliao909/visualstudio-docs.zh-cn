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
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 109cca0cc3d12d8bf14da848774042fe346f0f1e
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102168109"
---
# <a name="idebugprogramhost2"></a>IDebugProgramHost2
此接口提供主机 (进程) 有关程序的信息。

## <a name="syntax"></a>语法

```
IDebugProgramHost2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 调试引擎在与 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) 接口相同的对象上实现此接口，以提供有关宿主进程的信息。 这是一个可选接口。

## <a name="notes-for-callers"></a>调用方说明
 在接口上调用 [QueryInterface](/cpp/atl/queryinterface) `IDebugProgram2` 以获取此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法 `IDebugProgramHost2` 。

|方法|说明|
|------------|-----------------|
|[GetHostName](../../../extensibility/debugger/reference/idebugprogramhost2-gethostname.md)|获取此程序的宿主进程的标题、友好名称或文件名。|
|[GetHostId](../../../extensibility/debugger/reference/idebugprogramhost2-gethostid.md)|获取此程序的宿主进程的进程标识符。|
|[GetHostMachineName](../../../extensibility/debugger/reference/idebugprogramhost2-gethostmachinename.md)|获取运行此程序的承载进程的计算机的名称。|

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)

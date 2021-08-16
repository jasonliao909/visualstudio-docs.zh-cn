---
description: IDebugProcessSecurity 由端口供应商实现，以警告用户附加到进程不安全。
title: IDebugProcessSecurity |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProcessSecurity interface
ms.assetid: 8a52ddca-bd99-49c0-9778-469dce7abd44
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: e97d498abbd7cbc650a0438a96570c172e5cf1d48031c92f8bef7b09de8f1860
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121338886"
---
# <a name="idebugprocesssecurity"></a>IDebugProcessSecurity
`IDebugProcessSecurity` 由端口供应商实现，以警告用户附加到进程不安全。

## <a name="syntax"></a>语法

```
IDebugProcessSecurity : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法 `IDebugProcessSecurity` 。

|方法|说明|
|------------|-----------------|
|[GetUserName](../../../extensibility/debugger/reference/idebugprocesssecurity-getusername.md)|从端口供应商获取用户名。|
|[QueryCanSafelyAttach](../../../extensibility/debugger/reference/idebugprocesssecurity-querycansafelyattach.md)|警告用户附加到调试进程不安全。|

## <a name="remarks"></a>备注
 实现此接口以显示警告，并允许用户在要附加到的进程被视为不安全时取消。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [端口](../../../extensibility/debugger/ports.md)
- [端口提供程序](../../../extensibility/debugger/port-suppliers.md)
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)

---
description: 使调试引擎能够在结束调试会话时Visual Studio UI 的默认行为。
title: IDebugProgramDestroyEventFlags2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProgramDestroyEventFlags2 interface
ms.assetid: d384ff71-dc71-40b9-a871-801f8b6a3418
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 17c9cf3f910a1d94bf8a2972bb0615dd6f2e3b5762e99ae2eebff53c7a94611f
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121338743"
---
# <a name="idebugprogramdestroyeventflags2"></a>IDebugProgramDestroyEventFlags2
使调试引擎能够在结束调试会话时重写 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] UI 的默认行为。

## <a name="syntax"></a>语法

```
IDebugProgramDestroyEventFlags2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 此接口由调试引擎实现。 它适用于可能在进程生存期内创建和销毁多个程序主机。

## <a name="methods"></a>方法
 下表显示了 的方法 `IDebugProgramDestroyEventFlags2` 。

|方法|说明|
|------------|-----------------|
|[GetFlags](../../../extensibility/debugger/reference/idebugprogramdestroyeventflags2-getflags.md)|检索程序销毁标志。|

## <a name="remarks"></a>备注
 UI 的默认行为是在所有程序发送程序销毁事件后返回到 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] 设计模式。 此接口使调试引擎可以更改该行为。

## <a name="requirements"></a>要求
 标头：Msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

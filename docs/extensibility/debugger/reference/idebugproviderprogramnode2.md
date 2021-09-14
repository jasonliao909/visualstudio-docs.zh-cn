---
description: 此接口跨进程边界封送与程序相关的接口。
title: IDebugProviderProgramNode2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProviderProgramNode2
helpviewer_keywords:
- IDebugProviderProgramNode2
ms.assetid: f0bca1cc-afbe-44cf-b5aa-d078aa685d24
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 43a66e927d2a1d2e1afc84688bb3a36451fffecc
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664472"
---
# <a name="idebugproviderprogramnode2"></a>IDebugProviderProgramNode2
此接口跨进程边界封送与程序相关的接口。

## <a name="syntax"></a>语法

```
IDebugProviderProgramNode2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 调试引擎 (DE) 实现 [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) 的同一对象上实现此接口，以支持跨进程边界封送接口。

## <a name="notes-for-callers"></a>调用方说明
 在 [接口上调用 QueryInterface](/cpp/atl/queryinterface) `IDebugProgramNode2` 以获取此接口。 如果无法获取此接口，DE 不支持接口的封送处理。

## <a name="methods-in-vtable-order"></a>Vtable 顺序的方法
 此接口实现以下方法：

|方法|说明|
|------------|-----------------|
|[UnmarshalDebuggeeInterface](../../../extensibility/debugger/reference/idebugproviderprogramnode2-unmarshaldebuggeeinterface.md)|获取跨进程边界的指定接口。|

## <a name="remarks"></a>备注
 当 DE 在独立于正在调试的程序的进程空间中运行时实现此接口：例如，当 DE 在 Visual Studio 进程空间中运行，而不是在正在调试的程序的进程空间中运行时。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)

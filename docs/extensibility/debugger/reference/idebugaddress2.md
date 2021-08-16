---
description: 此接口提供对拥有其地址由此接口表示的对象的进程的 ID 的访问。
title: IDebugAddress2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugAddress2
helpviewer_keywords:
- IDebugAddress2 interface
ms.assetid: b150e0ed-4ac0-4f8c-9732-4b3e54b9d243
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: be12b088771484f1202fbb4cc806ae041d6d23778aa2e7efcb2ceee2cf1d1dd0
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121403177"
---
# <a name="idebugaddress2"></a>IDebugAddress2
此接口提供对拥有其地址由此接口表示的对象的进程的 ID 的访问。

## <a name="syntax"></a>语法

```
IDebugAddress2 : IDebugAddress
```

## <a name="notes-for-implementers"></a>实现者说明
 符号提供程序在实现 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) 接口的同一对象上实现此接口。 此接口提供对拥有与此地址相关的对象的进程的 ID 的访问。

## <a name="notes-for-callers"></a>调用方说明
 使用 [QueryInterface](/cpp/atl/queryinterface) 从 [IDebugAddress 接口获取此](../../../extensibility/debugger/reference/idebugaddress.md) 接口。

## <a name="methods-in-vtable-order"></a>vtable 顺序中的方法
 除了从 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) 接口继承的方法之外，此接口还实现以下方法：

|方法|说明|
|------------|-----------------|
|[GetProcessID](../../../extensibility/debugger/reference/idebugaddress2-getprocessid.md)|检索拥有此接口表示的对象的进程的 ID。|

## <a name="requirements"></a>要求
 标头：sh.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)

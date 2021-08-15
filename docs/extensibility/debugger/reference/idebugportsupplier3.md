---
description: 此接口允许调用方确定端口供应商是否可以通过在 (之间将端口写入磁盘) 来保留这些端口，然后获取这些保留端口的列表。
title: IDebugPortSupplier3 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortSupplier3
helpviewer_keywords:
- IDebugPortSupplier3 interface
ms.assetid: e458cd02-2370-4435-8953-17d7a60ce152
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 84dc23cf1c750d539d043b1993490a523c70ebaaacf04cc44c8702d8383278ad
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121416750"
---
# <a name="idebugportsupplier3"></a>IDebugPortSupplier3
此接口允许调用方确定端口供应商是否可以通过在 (之间将端口写入磁盘) 来保留这些端口，然后获取这些保留端口的列表。

## <a name="syntax"></a>语法

```
IDebugPortSupplier3 : IDebugPortSupplier2
```

## <a name="notes-for-implementers"></a>实现者说明
 自定义端口供应商实现此接口以支持将端口信息保留或保存到磁盘。 必须在与 [IDebugPortSupplier2 接口相同的对象上实现此](../../../extensibility/debugger/reference/idebugportsupplier2.md) 接口。

## <a name="notes-for-callers"></a>调用方说明
 在 [接口上调用 QueryInterface](/cpp/atl/queryinterface) `IDebugPortSupplier2` 以获取此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序的方法
 除了从 [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md) 接口继承的方法外，此接口还支持以下各项：

|方法|说明|
|------------|-----------------|
|[CanPersistPorts](../../../extensibility/debugger/reference/idebugportsupplier3-canpersistports.md)|返回端口供应商是否可以通过在 (之间将端口写入磁盘) 来持久保存端口。|
|[EnumPersistedPorts](../../../extensibility/debugger/reference/idebugportsupplier3-enumpersistedports.md)|返回一个对象，该对象可用于枚举此端口供应商写入磁盘的所有端口。|

## <a name="remarks"></a>备注
 如果端口供应商可以跨调用保留端口，则它应实现此接口。 在实例化端口供应商时，应加载端口，在销毁端口供应商时写入磁盘。

 调试引擎通常不与端口供应商交互，并且不会用于此接口。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)

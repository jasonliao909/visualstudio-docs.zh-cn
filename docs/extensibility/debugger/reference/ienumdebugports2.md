---
description: 此接口枚举计算机或端口供应商的端口。
title: IEnumDebugPorts2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugPorts2
helpviewer_keywords:
- IEnumDebugPorts2
ms.assetid: 1754eef3-cf62-42e0-b218-1911acba77d4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 243fcf1476f2f278ebed550805fcdfc9cf82d03300a1df70ad2c1c833ac3cdc8
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121291683"
---
# <a name="ienumdebugports2"></a>IEnumDebugPorts2
此接口枚举计算机或端口供应商的端口。

## <a name="syntax"></a>语法

```
IEnumDebugPorts2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 自定义端口供应商实现此接口来表示供应商创建的端口列表。 Visual Studio实现此接口以支持自己的端口供应商。

## <a name="notes-for-callers"></a>调用方说明
 调用 [EnumPorts](../../../extensibility/debugger/reference/idebugportsupplier2-enumports.md) 以获取此接口，该接口表示端口供应商创建的端口列表。 调用 [EnumPersistedPorts](../../../extensibility/debugger/reference/idebugportsupplier3-enumpersistedports.md) 以获取此接口，该接口表示保存到磁盘的端口列表。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法 `IEnumDebugPorts2` 。

|方法|说明|
|------------|-----------------|
|[下一页](../../../extensibility/debugger/reference/ienumdebugports2-next.md)|检索枚举序列中指定数量的端口。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugports2-skip.md)|跳过枚举序列中的指定数量的端口。|
|[重置](../../../extensibility/debugger/reference/ienumdebugports2-reset.md)|将枚举序列重置为开头。|
|[克隆](../../../extensibility/debugger/reference/ienumdebugports2-clone.md)|创建一个枚举器，其中包含与当前枚举器相同的枚举状态。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugports2-getcount.md)|获取枚举器中的端口数。|

## <a name="remarks"></a>备注
 Visual Studio使用此接口来帮助填充用于附加到进程端口的列表。

 调试引擎通常不使用此接口。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumPorts](../../../extensibility/debugger/reference/idebugcoreserver2-enumports.md)
- [EnumPorts](../../../extensibility/debugger/reference/idebugportsupplier2-enumports.md)

---
description: 此接口提供允许获取和设置属性的函数。
title: IDebugPropertyField |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPropertyField
helpviewer_keywords:
- IDebugPropertyField interface
ms.assetid: b50edb2c-fb8d-4def-993d-17d23d2027c1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: d4e0780f43953bdf7afb10e2d038ce46b794d3dd
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664474"
---
# <a name="idebugpropertyfield"></a>IDebugPropertyField
此接口提供允许获取和设置属性的函数。

## <a name="syntax"></a>语法

```
IDebugPropertyField : IDebugContainerField
```

## <a name="notes-for-implementers"></a>实现者说明
 符号提供程序在实现 [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)的同一对象上实现此接口。 此接口是支持类的属性概念的专用化。

## <a name="notes-for-callers"></a>调用方说明
 如果[GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)方法返回 ，则使用[QueryInterface](/cpp/atl/queryinterface)从[IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)接口获取此接口 `FIELD_KIND_PROP` 。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 和 [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md) 接口上的方法外，此接口还实现以下方法：

|方法|说明|
|------------|-----------------|
|[GetPropertyGetter](../../../extensibility/debugger/reference/idebugpropertyfield-getpropertygetter.md)|获取获取 属性的方法。|
|[GetPropertySetter](../../../extensibility/debugger/reference/idebugpropertyfield-getpropertysetter.md)|获取设置 属性的方法。|

## <a name="remarks"></a>备注
 属性是托管代码概念，表示被视为变量的方法。 非托管 C++ 中不存在属性。

## <a name="requirements"></a>要求
 标头：sh.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)

---
description: 此接口描述方法。
title: IDebugMethodField |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMethodField
helpviewer_keywords:
- IDebugMethodField interface
ms.assetid: a7dc9030-fc98-4cf1-b943-37a4003300b6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: c47be1364b9503bffeabc4eafeedde850a7cf96b58f262c289fc74db977310b4
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121433653"
---
# <a name="idebugmethodfield"></a>IDebugMethodField
此接口描述方法。

## <a name="syntax"></a>语法

```
IDebugMethodField : IDebugContainerField
```

## <a name="notes-for-implementers"></a>实现者说明
 符号提供程序在实现 [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md) 接口的同一对象上实现此接口。 此接口是一种提供方法的专用化。

## <a name="notes-for-callers"></a>调用方说明
 如果 GetKind 返回 ，则使用 [QueryInterface](/cpp/atl/queryinterface) 从 [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md) 接口 [获取此](../../../extensibility/debugger/reference/idebugfield-getkind.md) 接口 `FIELD_TYPE_METHOD` 。 此外，方法[GetPropertyGetter、GetPropertySetter](../../../extensibility/debugger/reference/idebugpropertyfield-getpropertygetter.md)和[EnumConstructors](../../../extensibility/debugger/reference/idebugclassfield-enumconstructors.md)均返回[](../../../extensibility/debugger/reference/idebugpropertyfield-getpropertysetter.md) `IDebugMethodField` 接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 和 [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md) 接口上的方法外，此接口还实现以下方法：

|方法|说明|
|------------|-----------------|
|[EnumParameters](../../../extensibility/debugger/reference/idebugmethodfield-enumparameters.md)|为 方法的参数创建枚举器。|
|[GetThis](../../../extensibility/debugger/reference/idebugmethodfield-getthis.md)|获取包含 方法的对象的"this"指针。|
|[EnumAllLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumalllocals.md)|为 方法的所有局部变量创建枚举器。|
|[EnumLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md)|为方法的选定局部变量创建枚举器。|
|[IsCustomAttributeDefined](../../../extensibility/debugger/reference/idebugmethodfield-iscustomattributedefined.md)|确定是否定义了特定的自定义属性。|
|[EnumStaticLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumstaticlocals.md)|为 方法的静态局部变量创建枚举器。|
|[GetGlobalContainer](../../../extensibility/debugger/reference/idebugmethodfield-getglobalcontainer.md)|获取 方法的全局容器。|
|[EnumArguments](../../../extensibility/debugger/reference/idebugmethodfield-enumarguments.md)|为调用 方法所需的每个参数的类型创建枚举器。|

## <a name="remarks"></a>备注
 方法可以包含参数和局部变量。

## <a name="requirements"></a>要求
 标头：sh.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)

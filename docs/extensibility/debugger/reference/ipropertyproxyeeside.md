---
description: 此接口提供查看关联对象上数据的方法。
title: IPropertyProxyEESide |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IPropertyProxyEESide
helpviewer_keywords:
- IPropertyProxyEESide interface
ms.assetid: cf227cf8-39d9-4758-8f7e-a697aebb1926
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 0295e4d0b23e2f474571490d44303aecebbb1f75
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664403"
---
# <a name="ipropertyproxyeeside"></a>IPropertyProxyEESide
此接口提供查看关联对象上数据的方法。 此接口是类型可视化工具支持的一部分。

## <a name="syntax"></a>语法

```
IPropertyProxyEESide : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 表达式计算程序实现此接口以支持类型可视化工具。

## <a name="notes-for-callers"></a>调用方说明
 调用 [GetPropertyProxy](../../../extensibility/debugger/reference/ipropertyproxyprovider-getpropertyproxy.md) 获取此接口。 在[IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)接口上调用[QueryInterface](/cpp/atl/queryinterface)以获取[IPropertyProxyProvider](../../../extensibility/debugger/reference/ipropertyproxyprovider.md)接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序的方法
 以下方法通过此接口实现：

|方法|说明|
|------------|-----------------|
|[InitSourceDataProvider](../../../extensibility/debugger/reference/ipropertyproxyeeside-initsourcedataprovider.md)|初始化数据源提供程序，以便可以访问对象的数据。|
|[GetManagedViewerCreationData](../../../extensibility/debugger/reference/ipropertyproxyeeside-getmanagedviewercreationdata.md)|检索有关对象的程序集的信息。|
|[GetInitialData](../../../extensibility/debugger/reference/ipropertyproxyeeside-getinitialdata.md)|获取 对象的初始数据。|
|[CreateReplacementObject](../../../extensibility/debugger/reference/ipropertyproxyeeside-createreplacementobject.md)|创建现有数据存储的副本。|
|[InPlaceUpdateObject](../../../extensibility/debugger/reference/ipropertyproxyeeside-inplaceupdateobject.md)|创建对现有数据存储的引用。|
|[ResolveAssemblyRef](../../../extensibility/debugger/reference/ipropertyproxyeeside-resolveassemblyref.md)|在包含此 对象的程序集的上下文中检索有关特定程序集的信息。|

## <a name="remarks"></a>备注
 类型可视化工具使用此接口访问与此接口属于的对象关联的值。 数据通过 [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md) 接口访问，该接口提供数据的只读视图。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [类型可视化工具和自定义查看器](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
- [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)

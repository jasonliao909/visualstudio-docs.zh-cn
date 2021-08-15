---
description: 此接口提供一个代理接口，用于查看和更改对象的数据。
title: IPropertyProxyProvider |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IPropertyProxyProvider
helpviewer_keywords:
- IPropertyProxyProvider interface
ms.assetid: 52e9f7fc-6fe0-4d23-890b-5673dca8c3cb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: ae6a242914e3071c7341b4268af28fd88a8be9a50df43573ccd757efc1c74207
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121433107"
---
# <a name="ipropertyproxyprovider"></a>IPropertyProxyProvider
此接口提供一个代理接口，用于查看和更改对象的数据。

## <a name="syntax"></a>语法

```
IPropertyProxyProvider : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 表达式计算 (企业版) 在实现[IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)接口的同一对象上实现此接口，作为 企业版 类型可视化工具支持的一部分。

## <a name="notes-for-callers"></a>调用方说明
 在 [接口上调用 QueryInterface](/cpp/atl/queryinterface) `IDebugProperty3` 以获取此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序的方法
 `IPropertyProxyProvider`接口实现以下方法：

|方法|说明|
|------------|-----------------|
|[GetPropertyProxy](../../../extensibility/debugger/reference/ipropertyproxyprovider-getpropertyproxy.md)|检索属性代理接口以查看对象上的数据。|

## <a name="remarks"></a>备注
 尽管企业版实现此接口，[但 GetPropertyProxy](../../../extensibility/debugger/reference/ipropertyproxyprovider-getpropertyproxy.md)的实现通常由[GetPropertyProxy 处理](../../../extensibility/debugger/reference/ieevisualizerservice-getpropertyproxy.md)。 有关 [获取](../../../extensibility/debugger/visualizing-and-viewing-data.md) IEEVisualizerService 接口的详细信息，请参阅可视化和查看数据。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetPropertyProxy](../../../extensibility/debugger/reference/ieevisualizerservice-getpropertyproxy.md)
- [类型可视化工具和自定义查看器](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
- [可视化和查看数据](../../../extensibility/debugger/visualizing-and-viewing-data.md)

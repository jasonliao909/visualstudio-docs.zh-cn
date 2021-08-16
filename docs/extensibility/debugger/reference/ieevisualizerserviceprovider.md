---
description: 此接口允许访问可创建可视化工具服务的方法，该服务用于处理 IDE 的类型可视化工具任务。
title: IEEVisualizerServiceProvider |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEVisualizerServiceProvider
helpviewer_keywords:
- IEEVisualizerServiceProvider interface
ms.assetid: 859d1a51-1c65-4c8b-ae74-3b74b181ebcd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: bbc67be1904c785f10ea1e3ee3144d2d40380730749247f58be639bbd0cbb8f4
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121389405"
---
# <a name="ieevisualizerserviceprovider"></a>IEEVisualizerServiceProvider
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式计算器的方法已弃用。 有关实现 CLR 表达式计算器的信息，请参阅 [Clr 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 此接口允许访问可创建可视化工具服务的方法，该服务用于处理 IDE 的类型可视化工具任务。

## <a name="syntax"></a>语法

```
IEEVisualizerServiceProvider : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 Visual Studio 实现此接口来创建可视化工具服务对象，而该对象又用于向 `CLSID` Visual Studio IDE 提供可视化工具类型 (s) 的类 id。

## <a name="notes-for-callers"></a>调用方说明
 表达式计算器 (企业版) 调用[GetEEService](../../../extensibility/debugger/reference/idebugbinder3-geteeservice.md)来获取此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序的方法

|方法|说明|
|------------|-----------------|
|[CreateVisualizerService](../../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md)|创建可视化工具服务|

## <a name="remarks"></a>备注
 `IEEVisualizerServiceProvider`接口是在实现[EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)的过程中获取的。 此接口创建的可视化工具服务用于将功能提供给企业版负责实现的[IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)接口。 企业版还负责实现允许类型可视化工具查看和修改属性值的[IEEVisualizerDataProvider](../../../extensibility/debugger/reference/ieevisualizerdataprovider.md)接口。

 有关这些接口如何交互的详细信息，请参阅 [可视化和查看数据](../../../extensibility/debugger/visualizing-and-viewing-data.md) 。

## <a name="requirements"></a>要求
 标头： ee。h

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [表达式计算接口](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)
- [IEEVisualizerDataProvider](../../../extensibility/debugger/reference/ieevisualizerdataprovider.md)
- [GetEEService](../../../extensibility/debugger/reference/idebugbinder3-geteeservice.md)
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [可视化和查看数据](../../../extensibility/debugger/visualizing-and-viewing-data.md)

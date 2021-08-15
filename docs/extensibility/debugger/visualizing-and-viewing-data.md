---
title: 可视化和查看数据 |Microsoft Docs
description: 了解类型可视化工具和自定义查看器如何向开发人员提供数据。 表达式计算器支持第三方类型可视化工具。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], viewing data
- debugging [Debugging SDK], visualizing data
ms.assetid: 699dd0f5-7569-40b3-ade6-d0fe53e832bc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 85cc7d58eccae8a76f13f7d5be1a9a0530b8045ffe5209f57d3e97feef3fc99c
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121448450"
---
# <a name="visualizing-and-viewing-data"></a>可视化和查看数据
类型可视化工具和自定义查看器以快速向开发人员提供意义的方式显示数据。 表达式计算器 (企业版) 可支持第三方类型可视化工具，并提供自己的自定义查看器。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 通过调用 [GetCustomViewerCount](../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md) 方法，确定多少类型可视化工具和自定义查看器与对象的类型相关联。 如果至少有一个可用的类型可视化工具或自定义查看器，Visual Studio 将调用[GetCustomViewerList](../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)方法来检索这些可视化工具和查看器的列表 (实际上是实现可视化工具和查看器) 并向用户显示的列表。

## <a name="supporting-type-visualizers"></a>支持类型可视化工具
 为了支持类型可视化工具，企业版必须实现多个接口。 这些接口可以分为两大类：列出可视化工具的类型和访问属性数据的接口。

### <a name="listing-type-visualizers"></a>列出类型可视化工具
 企业版支持在和的实现中列出可视化工具的 `IDebugProperty3::GetCustomViewerCount` 类型 `IDebugProperty3::GetCustomViewerList` 。 这些方法将对相应方法的调用传递给 [GetCustomViewerCount](../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewercount.md) 和 [GetCustomViewerList](../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md)。

 [IEEVisualizerService](../../extensibility/debugger/reference/ieevisualizerservice.md)是通过调用[CreateVisualizerService](../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md)获取的。 此方法需要[IDebugBinder3](../../extensibility/debugger/reference/idebugbinder3.md)接口，该接口是从传递给[EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)的[IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)接口获取的。 `IEEVisualizerServiceProvider::CreateVisualizerService` 还需要传递到的 [IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md) 和 [IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md) 接口 `IDebugParsedExpression::EvaluateSync` 。 创建接口所需的最终接口 `IEEVisualizerService` 是企业版实现的[IEEVisualizerDataProvider](../../extensibility/debugger/reference/ieevisualizerdataprovider.md)接口。 此接口允许对正在可视化的属性进行更改。 所有属性数据都封装在[IDebugObject](../../extensibility/debugger/reference/idebugobject.md)接口中，该接口也由企业版实现。

### <a name="accessing-property-data"></a>访问属性数据
 访问属性数据是通过 [IPropertyProxyEESide](../../extensibility/debugger/reference/ipropertyproxyeeside.md) 接口实现的。 若要获取此接口，Visual Studio 调用属性对象上的[QueryInterface](/cpp/atl/queryinterface) ，以获取在实现[IDebugProperty3](../../extensibility/debugger/reference/idebugproperty3.md)) 接口的同一对象上实现的[IPropertyProxyProvider](../../extensibility/debugger/reference/ipropertyproxyprovider.md)接口 (，然后调用[GetPropertyProxy](../../extensibility/debugger/reference/ipropertyproxyprovider-getpropertyproxy.md)方法来获取 `IPropertyProxyEESide` 接口。

 传入和传出接口的所有数据 `IPropertyProxyEESide` 封装在 [IEEDataStorage](../../extensibility/debugger/reference/ieedatastorage.md) 接口中。 此接口表示一个字节数组，并由 Visual Studio 和企业版实现。 如果要更改某个属性的数据，Visual Studio 会创建一个 `IEEDataStorage` 包含新数据的对象，并使用该数据对象调用[CreateReplacementObject](../../extensibility/debugger/reference/ipropertyproxyeeside-createreplacementobject.md) ，以获取一个新的对象，然后 `IEEDataStorage` 将该对象传递给[InPlaceUpdateObject](../../extensibility/debugger/reference/ipropertyproxyeeside-inplaceupdateobject.md)以更新该属性的数据。 `IPropertyProxyEESide::CreateReplacementObject`允许企业版实例化其自己的实现接口的类 `IEEDataStorage` 。

## <a name="supporting-custom-viewers"></a>支持自定义查看器
 在 `DBG_ATTRIB_VALUE_CUSTOM_VIEWER` DEBUG_PROPERTY_INFO 结构的字段中设置标志， `dwAttrib` (通过调用[GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)) 返回，以指示该对象具有与之关联的自定义查看器。 [](../../extensibility/debugger/reference/debug-property-info.md) 设置此标志后，Visual Studio 使用[QueryInterface](/cpp/atl/queryinterface)从[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)接口获取[IDebugProperty3](../../extensibility/debugger/reference/idebugproperty3.md)接口。

 如果用户选择自定义查看器，Visual Studio 使用由方法提供的查看器来实例化自定义查看器 `CLSID` `IDebugProperty3::GetCustomViewerList` 。 然后 Visual Studio 调用[DisplayValue](../../extensibility/debugger/reference/idebugcustomviewer-displayvalue.md)来向用户显示值。

 通常， `IDebugCustomViewer::DisplayValue` 显示数据的只读视图。 若要允许对数据进行更改，企业版必须实现一个自定义接口，该接口支持更改属性对象上的数据。 `IDebugCustomViewer::DisplayValue`方法使用此自定义接口来支持更改数据。 方法查找作为参数传入的接口上的自定义接口 `IDebugProperty2` `pDebugProperty` 。

## <a name="supporting-both-type-visualizers-and-custom-viewers"></a>支持类型可视化工具和自定义查看器
 企业版可以同时支持[GetCustomViewerCount](../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md)和[GetCustomViewerList](../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)方法中的类型可视化工具和自定义查看器。 首先，企业版会将其提供给[GetCustomViewerCount](../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewercount.md)方法返回的值的自定义查看器数添加到其中。 其次，企业版将自己的 `CLSID` 自定义查看器的[GetCustomViewerList](../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md)追加到由方法返回的列表。

## <a name="see-also"></a>另请参阅
- [调试任务](../../extensibility/debugger/debugging-tasks.md)
- [类型可视化工具和自定义查看器](../../extensibility/debugger/type-visualizer-and-custom-viewer.md)

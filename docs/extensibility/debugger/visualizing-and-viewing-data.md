---
title: 可视化和查看|Microsoft Docs
description: 了解类型可视化工具与自定义查看器如何向开发人员呈现数据。 表达式计算程序支持第三方类型可视化工具。
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
ms.openlocfilehash: bd0fa59cec59e27949bf9d8d209bc66221d3505d
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600795"
---
# <a name="visualizing-and-viewing-data"></a>可视化和查看数据
类型可视化工具和自定义查看器以对开发人员快速有意义的方式呈现数据。 表达式评估 (企业版) 可以支持第三方类型可视化工具，以及提供其自己的自定义查看器。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 通过调用 [GetCustomViewerCount](../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md) 方法，确定与对象的类型关联的类型可视化工具与自定义查看器数量。 如果至少有一个类型可视化工具或自定义查看器可用，Visual Studio 将调用[GetCustomViewerList](../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)方法来检索这些可视化工具与查看器的列表 (实际上，这是一个实现可视化工具与查看器的 列表) 并呈现给用户。

## <a name="supporting-type-visualizers"></a>支持类型可视化工具
 用户必须实现许多接口企业版支持类型可视化工具。 这些接口可以分为两大类：列出类型可视化工具的接口和访问属性数据的接口。

### <a name="listing-type-visualizers"></a>列出类型可视化工具
 该企业版支持在其 和 的实现中列出类型可视化 `IDebugProperty3::GetCustomViewerCount` 工具 `IDebugProperty3::GetCustomViewerList` 。 这些方法将调用传递给相应的 [方法 GetCustomViewerCount](../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewercount.md) 和 [GetCustomViewerList](../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md)。

 [IEEVisualizerService](../../extensibility/debugger/reference/ieevisualizerservice.md)通过调用[CreateVisualizerService 获取](../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md)。 此方法需要[IDebugBinder3](../../extensibility/debugger/reference/idebugbinder3.md)接口，该接口从传递给[EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)的[IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)接口获取。 `IEEVisualizerServiceProvider::CreateVisualizerService` 还需要传递到 的 [IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md) 和 [IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md) 接口 `IDebugParsedExpression::EvaluateSync` 。 创建接口所需的最终接口是 `IEEVisualizerService` [IEEVisualizerDataProvider](../../extensibility/debugger/reference/ieevisualizerdataprovider.md)接口，企业版实现。 此接口允许对要可视化的属性进行更改。 所有属性数据都封装在[IDebugObject](../../extensibility/debugger/reference/idebugobject.md)接口中，该接口也由 企业版。

### <a name="accessing-property-data"></a>访问属性数据
 通过 [IPropertyProxyEESide](../../extensibility/debugger/reference/ipropertyproxyeeside.md) 接口访问属性数据。 若要获取此接口，Visual Studio 对属性对象调用[QueryInterface](/cpp/atl/queryinterface)以获取[IPropertyProxyProvider](../../extensibility/debugger/reference/ipropertyproxyprovider.md)接口 (该接口在实现[IDebugProperty3](../../extensibility/debugger/reference/idebugproperty3.md)接口) 的同一对象上实现，然后调用[GetPropertyProxy](../../extensibility/debugger/reference/ipropertyproxyprovider-getpropertyproxy.md)方法来获取接口。 `IPropertyProxyEESide`

 传入和退出接口的所有 `IPropertyProxyEESide` 数据都封装在 [IEEDataStorage](../../extensibility/debugger/reference/ieedatastorage.md) 接口中。 此接口表示字节数组，由 Visual Studio 和 企业版。 当要更改属性的数据时，Visual Studio 将创建一个包含新数据的对象，并调用具有该数据对象的 `IEEDataStorage` [CreateReplacementObject，](../../extensibility/debugger/reference/ipropertyproxyeeside-createreplacementobject.md)以获取一个新的 对象，而该对象又传递到 `IEEDataStorage` [InPlaceUpdateObject](../../extensibility/debugger/reference/ipropertyproxyeeside-inplaceupdateobject.md)以更新属性的数据。 `IPropertyProxyEESide::CreateReplacementObject`允许企业版实例化实现 接口的自己的 `IEEDataStorage` 类。

## <a name="supporting-custom-viewers"></a>支持自定义查看器
 标志在调用 `DBG_ATTRIB_VALUE_CUSTOM_VIEWER` `dwAttrib` [GetPropertyIn) fo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) [](../../extensibility/debugger/reference/debug-property-info.md) (返回的 DEBUG_PROPERTY_INFO 结构字段中设置，以指示对象具有与之关联的自定义查看器。 设置此标志后，Visual Studio [QueryInterface](/cpp/atl/queryinterface)从[IDebugProperty2 接口获取 IDebugProperty3](../../extensibility/debugger/reference/idebugproperty2.md)接口。 [](../../extensibility/debugger/reference/idebugproperty3.md)

 如果用户选择自定义查看器，Visual Studio方法提供的查看器实例化 `CLSID` 自定义 `IDebugProperty3::GetCustomViewerList` 查看器。 Visual Studio调用[DisplayValue](../../extensibility/debugger/reference/idebugcustomviewer-displayvalue.md)向用户显示值。

 通常， `IDebugCustomViewer::DisplayValue` 提供数据的只读视图。 若要允许更改数据，企业版必须实现一个自定义接口，该接口支持更改属性对象上的数据。 `IDebugCustomViewer::DisplayValue`方法使用此自定义接口来支持更改数据。 方法在作为参数传入的 `IDebugProperty2` 接口上查找自定义 `pDebugProperty` 接口。

## <a name="supporting-both-type-visualizers-and-custom-viewers"></a>支持类型可视化工具与自定义查看器
 一企业版[GetCustomViewerCount](../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md)和[GetCustomViewerList](../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)方法中的类型可视化工具和自定义查看器。 首先，企业版向[GetCustomViewerCount](../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewercount.md)方法返回的值添加它所提供自定义查看器的数量。 其次，企业版将自己的自定义查看器的 追加 `CLSID` 到[GetCustomViewerList](../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md)方法返回的列表中。

## <a name="see-also"></a>另请参阅
- [调试任务](../../extensibility/debugger/debugging-tasks.md)
- [类型可视化工具与自定义查看器](../../extensibility/debugger/type-visualizer-and-custom-viewer.md)

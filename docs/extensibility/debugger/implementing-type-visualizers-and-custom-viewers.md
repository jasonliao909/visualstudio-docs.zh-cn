---
title: 实现类型可视化工具以及自定义查看器|Microsoft Docs
description: 了解如何实现类型可视化工具和自定义查看器，使用户可以以比数字转储更有意义的方式查看数据。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], custom viewer
- debugging [Debugging SDK], type visualizer
ms.assetid: abef18c0-8272-4451-b82a-b4624edaba7d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: b42afdc165540360d8d8c1c458e1c044dbcbcddd
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122138752"
---
# <a name="implement-type-visualizers-and-custom-viewers"></a>实现类型可视化工具与自定义查看器
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式计算器的方法已弃用。 有关实现 CLR 表达式计算器的信息，请参阅 [CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 类型可视化工具和自定义查看器允许用户以比简单的十六进制数字转储更有意义的方式查看特定类型的数据。 表达式评估器 (企业版) 自定义查看器与特定类型的数据或变量关联。 这些自定义查看器由 企业版。 该企业版还可以支持外部类型可视化工具，这些可视化工具可能来自其他第三方供应商，甚至是最终用户。

## <a name="discussion"></a>讨论 (Discussion)

### <a name="type-visualizers"></a>类型可视化工具
 Visual Studio要求在监视窗口中显示每个对象的类型可视化工具列表和自定义查看器。 表达式评估 (企业版) 为想要支持类型可视化工具及自定义查看器的每种类型提供此类列表。 调用 [GetCustomViewerCount](../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md) 和 [GetCustomViewerList](../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md) 将启动访问类型可视化工具和自定义查看器的整个过程 (请参阅 [可视化](../../extensibility/debugger/visualizing-and-viewing-data.md) 和查看数据，了解有关调用序列) 。

### <a name="custom-viewers"></a>自定义查看器
 自定义查看器在企业版数据类型的数据集中实现，由[IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md)接口表示。 自定义查看器没有类型可视化工具那么灵活，因为它仅在实现该特定自定义查看器企业版时可用。 实现自定义查看器比实现对类型可视化工具的支持更简单。 但是，支持类型可视化工具为最终用户提供了最大的灵活性来可视化其数据。 此讨论的其余部分仅涉及类型可视化工具。

## <a name="interfaces"></a>界面
 该企业版实现以下接口以支持类型可视化工具，供 Visual Studio：

- [IEEVisualizerDataProvider](../../extensibility/debugger/reference/ieevisualizerdataprovider.md)

- [IPropertyProxyEESide](../../extensibility/debugger/reference/ipropertyproxyeeside.md)

- [IPropertyProxyProvider](../../extensibility/debugger/reference/ipropertyproxyprovider.md)

- [IEEDataStorage](../../extensibility/debugger/reference/ieedatastorage.md)

- [IDebugProperty3](../../extensibility/debugger/reference/idebugproperty3.md)

- [IDebugObject](../../extensibility/debugger/reference/idebugobject.md)

  该企业版使用以下接口来支持类型可视化工具：

- [IEEVisualizerService](../../extensibility/debugger/reference/ieevisualizerservice.md)

- [IEEVisualizerServiceProvider](../../extensibility/debugger/reference/ieevisualizerserviceprovider.md)

- [IDebugBinder3](../../extensibility/debugger/reference/idebugbinder3.md)

## <a name="see-also"></a>请参阅
- [编写 CLR 表达式计算程序](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
- [可视化和查看数据](../../extensibility/debugger/visualizing-and-viewing-data.md)
- [IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md)

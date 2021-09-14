---
title: 类型可视化工具和自定义查看器 |Microsoft Docs
description: 了解类型可视化工具和自定义查看器，它以特定的格式显示数据和它们之间的差异。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], custom viewer
- debugging [Debugging SDK], type visualizer
ms.assetid: fd3691e6-9c78-4767-846f-43f85ada4375
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: a27606abf4b33acfb812d55cad83a801f05d3f2f
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600798"
---
# <a name="type-visualizer-and-custom-viewer"></a>类型可视化工具和自定义查看器
类型可视化工具是以特定格式显示一段数据的组件。 格式完全取决于实现可视化工具的用户，是最终用户或可视化工具的第三方供应商。

 自定义查看器是自定义表达式计算器的一部分，它以特定的格式显示一段数据。 此格式完全取决于自定义查看器的实施者，这意味着该格式由表达式计算器的实施者决定 (企业版) 。

## <a name="support-for-type-visualizers-in-an-expression-evaluator"></a>对表达式计算器中的类型可视化工具的支持
 通过支持可视化工具可访问的一组接口（如[IEEVisualizerService](../../extensibility/debugger/reference/ieevisualizerservice.md)和[IEEVisualizerDataProvider](../../extensibility/debugger/reference/ieevisualizerdataprovider.md)），企业版支持类型可视化工具。 但企业版不负责实现类型可视化工具本身：企业版只允许外部可视化工具访问其类型信息。 此类可视化工具可能随企业版一起提供，并安装在 Visual Studio 中的适当位置，由其他第三方供应商提供，甚至由最终用户提供。

## <a name="support-for-custom-viewers-in-an-expression-evaluator"></a>表达式计算器中的自定义查看器支持
 企业版还可以支持自定义查看器，在该查看器中，企业版本身提供用于查看数据类型的代码。 自定义查看器实现了 [IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md) 接口，该接口可处理以任意格式显示数据的所有职责;查看器可以完全控制显示，甚至可以让数据被修改。 企业版提供的任何自定义查看器均随附产品时的企业版。

## <a name="see-also"></a>另请参阅
- [调试器组件](../../extensibility/debugger/debugger-components.md)
- [表达式计算器](../../extensibility/debugger/expression-evaluator.md)
- [调试引擎](../../extensibility/debugger/debug-engine.md)
- [IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md)
- [IEEVisualizerService](../../extensibility/debugger/reference/ieevisualizerservice.md)
- [IEEVisualizerDataProvider](../../extensibility/debugger/reference/ieevisualizerdataprovider.md)

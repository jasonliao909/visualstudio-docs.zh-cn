---
title: 类型可视化工具与自定义查看器|Microsoft Docs
description: 了解类型可视化工具组件和自定义查看器，它们以特定格式显示数据，以及它们之间的差异。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122042603"
---
# <a name="type-visualizer-and-custom-viewer"></a>类型可视化工具与自定义查看器
类型可视化工具是一个组件，它以特定格式显示一段数据。 格式完全由实现可视化工具的用户决定，而可视化工具是最终用户还是第三方供应商。

 自定义查看器是自定义表达式计算程序（以特定格式显示一段数据）的一部分。 此格式完全由自定义查看器的实现者决定，这意味着该格式取决于表达式计算程序 (企业版) 。

## <a name="support-for-type-visualizers-in-an-expression-evaluator"></a>支持表达式评估器中的类型可视化工具
 一企业版支持一组可供可视化工具访问的接口来支持类型可视化工具[：IEEVisualizerService](../../extensibility/debugger/reference/ieevisualizerservice.md)和[IEEVisualizerDataProvider](../../extensibility/debugger/reference/ieevisualizerdataprovider.md)等接口。 但是，企业版不负责实现类型可视化工具本身：企业版仅允许外部可视化工具访问其类型信息。 此类可视化工具可以随 企业版一起随附，并安装在 Visual Studio 的适当位置，由另一个第三方供应商甚至最终用户提供。

## <a name="support-for-custom-viewers-in-an-expression-evaluator"></a>支持表达式评估器中的自定义查看器
 一企业版还可以支持自定义查看器，其中企业版本身提供用于查看数据类型的代码。 自定义查看器实现 [IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md) 接口，该接口处理以任何所需格式显示数据的所有职责;查看器可以完全控制显示，甚至可以允许修改数据。 产品发货时，企业版提供企业版自定义查看器。

## <a name="see-also"></a>请参阅
- [调试器组件](../../extensibility/debugger/debugger-components.md)
- [表达式计算程序](../../extensibility/debugger/expression-evaluator.md)
- [调试引擎](../../extensibility/debugger/debug-engine.md)
- [IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md)
- [IEEVisualizerService](../../extensibility/debugger/reference/ieevisualizerservice.md)
- [IEEVisualizerDataProvider](../../extensibility/debugger/reference/ieevisualizerdataprovider.md)

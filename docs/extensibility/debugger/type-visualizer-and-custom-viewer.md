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
ms.workload:
- vssdk
ms.openlocfilehash: c18bb49c740362d42a4a54bf52f6998629acb0c0
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904417"
---
# <a name="type-visualizer-and-custom-viewer"></a>类型可视化工具与自定义查看器
类型可视化工具是一个组件，它以特定格式显示一段数据。 格式完全由实现可视化工具的用户决定，而可视化工具是最终用户还是第三方供应商。

 自定义查看器是自定义表达式计算程序（以特定格式显示一段数据）的一部分。 此格式完全由自定义查看器的实现者决定，这意味着该格式取决于 EE (表达式) 。

## <a name="support-for-type-visualizers-in-an-expression-evaluator"></a>支持表达式评估器中的类型可视化工具
 EE 通过支持可视化工具可访问的一组接口来支持类型可视化工具 [：IEEVisualizerService](../../extensibility/debugger/reference/ieevisualizerservice.md) 和 [IEEVisualizerDataProvider](../../extensibility/debugger/reference/ieevisualizerdataprovider.md)等接口。 但是，EE 不负责实现类型可视化工具本身：EE 仅允许外部可视化工具访问其类型信息。 此类可视化工具可以随 EE 一起随附，并安装在 Visual Studio 的适当位置，由另一个第三方供应商甚至最终用户提供。

## <a name="support-for-custom-viewers-in-an-expression-evaluator"></a>支持表达式评估器中的自定义查看器
 EE 还可以支持自定义查看器，其中 EE 本身提供用于查看数据类型的代码。 自定义查看器实现 [IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md) 接口，该接口处理以任何所需格式显示数据的所有职责;查看器可以完全控制显示，甚至可以允许修改数据。 产品发货时，EE 提供的任何自定义查看器都附带 EE。

## <a name="see-also"></a>另请参阅
- [调试器组件](../../extensibility/debugger/debugger-components.md)
- [表达式计算器](../../extensibility/debugger/expression-evaluator.md)
- [调试引擎](../../extensibility/debugger/debug-engine.md)
- [IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md)
- [IEEVisualizerService](../../extensibility/debugger/reference/ieevisualizerservice.md)
- [IEEVisualizerDataProvider](../../extensibility/debugger/reference/ieevisualizerdataprovider.md)

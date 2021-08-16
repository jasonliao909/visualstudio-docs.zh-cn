---
description: 下面是用于调试 SDK 的表达式Visual Studio接口。
title: 表达式计算接口|Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- expression evaluation, interfaces
ms.assetid: 2d259f60-2cd7-460e-b02d-24a8fb202850
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 22110ea35cbac5bc2fbfca06448e7ece2e0fc7cf82b2a62e6f1d0ee835d38eae
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121434316"
---
# <a name="expression-evaluation-interfaces"></a>表达式计算接口
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式计算器的方法已弃用。 有关实现 CLR 表达式评估器的信息，请参阅 [CLR 表达式评估器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式评估器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 以下是调试 SDK 的表达式 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] 计算接口。

## <a name="discussion"></a>讨论区
 这些接口用于在中断模式期间计算调用堆栈中的表达式。 它们仅针对公共语言运行时表达式评估程序 (企业版) 。

 表中的每个接口都显示了可以从以下列表实现它的组件：

- 调试引擎 (DE) 

- 表达式计算 (企业版) 

- Visual Studio (VS) 

|接口|实现者|说明|
|---------------|--------------------|-----------------|
|[IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)|EE|表示变量的数值别名。|
|[IDebugAlias2](../../../extensibility/debugger/reference/idebugalias2.md)|EE|表示变量的数值别名，使表达式 (企业版) 获取别名的应用程序域。|
|[IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md)|EE|表示一个数组对象。|
|[IDebugArrayObject2](../../../extensibility/debugger/reference/idebugarrayobject2.md)|EE|表示托管数组对象，并允许表达式 (企业版) 确定数组 (下限) 基索引。|
|[IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)|DE|表示将调试符号绑定到内存中的实际地址的联编程序。|
|[IDebugBinder3](../../../extensibility/debugger/reference/idebugbinder3.md)|DE|与 [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md) 接口相同，但提供对类型、别名和自定义可视化工具的访问。|
|[IDebugExpressionEvaluator](../../../extensibility/debugger/reference/idebugexpressionevaluator.md)|EE|表示表达式计算器。|
|[IDebugExpressionEvaluator2](../../../extensibility/debugger/reference/idebugexpressionevaluator2.md)|EE|表示表达式计算程序表达式的增强 (企业版) 。|
|[IDebugExpressionEvaluator3](../../../extensibility/debugger/reference/idebugexpressionevaluator3.md)|EE|表示具有增强 (企业版) 树的表达式计算程序。|
|[IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)|EE|表示函数。|
|[IDebugFunctionObject2](../../../extensibility/debugger/reference/idebugfunctionobject2.md)|EE|表示函数并增强 [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md) 接口。|
|[IDebugIDECallback](../../../extensibility/debugger/reference/idebugidecallback.md)|DE|允许表达式计算 (企业版) 在调试器的输出窗口中显示消息。|
|[IDebugManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject.md)|EE|表示托管代码对象。|
|[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)|EE|表示绑定到内存地址的任何符号的基接口。|
|[IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md)|EE|与 [IDebugObject 接口](../../../extensibility/debugger/reference/idebugobject.md) 相同，但提供对附加信息的访问。|
|[IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md)|EE|表示已准备好计算已分析的表达式。|
|[IDebugPointerObject](../../../extensibility/debugger/reference/idebugpointerobject.md)|EE|表示指针。|
|[IDebugPointerObject3](../../../extensibility/debugger/reference/idebugpointerobject3.md)|EE|表示分析树中的指针，并扩展 **IDebugPointerObject** 接口。|
|[IEEVisualizerDataProvider](../../../extensibility/debugger/reference/ieevisualizerdataprovider.md)|EE|提供通过类型可视化工具修改类型值的能力。|
|[IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md)|VS|提供对自定义查看器和类型可视化工具的访问。|
|[IEEVisualizerServiceProvider](../../../extensibility/debugger/reference/ieevisualizerserviceprovider.md)|VS|提供创建 [IEEVisualizerService 对象](../../../extensibility/debugger/reference/ieevisualizerservice.md) 的能力。|
|[IEnumDebugObjects](../../../extensibility/debugger/reference/ienumdebugobjects.md)|EE|表示 [IDebugObject 对象](../../../extensibility/debugger/reference/idebugobject.md) 的集合。|

## <a name="see-also"></a>另请参阅
- [API 参考](../../../extensibility/debugger/reference/api-reference-visual-studio-debugging.md)
- [编写 CLR 表达式计算器](../../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
- [类型可视化工具和自定义查看器](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)

---
description: 此接口表示可以进行计算的已分析表达式。
title: IDebugParsedExpression |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugParsedExpression
helpviewer_keywords:
- IDebugParsedExpression interface
ms.assetid: be6486ed-b070-4898-95b1-58581bcb4447
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 00daeac20d621657d61aa802d79a46a3ee0e7aa7
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084579"
---
# <a name="idebugparsedexpression"></a>IDebugParsedExpression
> [!IMPORTANT]
> 在 Visual Studio 2015 中，不推荐使用这种实现表达式计算器的方式。 有关实现 CLR 表达式计算器的信息，请参阅 [Clr 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 此接口表示可以进行计算的已分析表达式。

## <a name="syntax"></a>语法

```
IDebugParsedExpression : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 表达式计算器实现此接口，以表示可进行计算的已分析表达式。

## <a name="notes-for-callers"></a>调用方说明
 对 [Parse](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md) 的调用将返回此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法 `IDebugParsedExpression` 。

|方法|说明|
|------------|-----------------|
|[EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)|计算分析的表达式。|

## <a name="remarks"></a>备注
 当调用方准备好对表达式进行求值时，它会调用 [EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) 以返回一个包含计算结果的 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) 。 这是一种用于计算、分析然后计算的两部分方法，它使分析后的表达式可以多次计算，绕过分析表达式的耗时过程。

## <a name="requirements"></a>要求
 标头： ee。h

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [Parse](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)
- [EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)

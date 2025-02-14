---
title: 更改本地值|Microsoft Docs
description: 了解在"局部值"窗口的值字段中键入新值时更改局部值的过程。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation, changing values programmatically
ms.assetid: 8407d3df-d38a-4328-82d1-98084bef43ec
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: ba6ea460d16491d651c52e9dec1ca430c33fefd6
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664616"
---
# <a name="change-the-value-of-a-local"></a>更改本地的值
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式计算器的方法已弃用。 有关实现 CLR 表达式评估器的信息，请参阅 [CLR 表达式评估器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式评估器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 在"局部值"窗口的值字段中键入新值时，调试包会将字符串按类型传递给表达式 (企业版) 。 该企业版计算此字符串，该字符串可以包含简单值或表达式，并且将生成的值存储在关联的本地中。

 这是对更改本地值的过程的概述：

1. 用户输入新值后，Visual Studio与本地[关联的 IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)对象上调用[SetValueAsString。](../../extensibility/debugger/reference/idebugproperty2-setvalueasstring.md)

2. `IDebugProperty2::SetValueAsString` 执行下列任务：

   1. 计算字符串以生成值。

   2. 绑定关联的 [IDebugField](../../extensibility/debugger/reference/idebugfield.md) 对象以获取 [IDebugObject](../../extensibility/debugger/reference/idebugobject.md) 对象。

   3. 将值转换为一系列字节。

   4. 调用 [SetValue](../../extensibility/debugger/reference/idebugobject-setvalue.md) 将值的字节放入内存中，以便正在调试的程序可以访问它们。

3. Visual Studio刷新"局部区域 **"显示 (** 请参阅显示局部区域 [设置](../../extensibility/debugger/displaying-locals.md)，了解) 。

   此过程还用于在"监视"窗口中更改变量的值，只不过它是与所使用的局部变量的值关联的对象，而不是与本地本身 `IDebugProperty2` `IDebugProperty2` 关联的对象。

## <a name="in-this-section"></a>本节内容
 [更改值的示例实现](../../extensibility/debugger/sample-implementation-of-changing-values.md) 使用 MyCEE 示例逐步完成更改值的过程。

## <a name="see-also"></a>另请参阅
- [编写 CLR 表达式计算程序](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
- [显示局部变量](../../extensibility/debugger/displaying-locals.md)

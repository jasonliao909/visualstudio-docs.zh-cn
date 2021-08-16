---
title: 编写公共语言运行时表达式计算器 |Microsoft Docs
description: 了解如何为公共语言运行时编写表达式计算器，该计算器计算正在调试的代码语言中的表达式。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- expression evaluators, tutorial
- expression evaluation, samples
- debugging [Debugging SDK], expression evaluators tutorial
ms.assetid: bd79d57f-8e0a-4e14-a417-0b1de28fa1b2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: bfc32d79ac0e1d38792890f5b997895b1f009def556c73c87ee2e53690c3da17
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121388911"
---
# <a name="writing-a-common-language-runtime-expression-evaluator"></a>编写公共语言运行时表达式计算器
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式计算器的方法已弃用。 有关实现 CLR 表达式计算器的信息，请参阅 [CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 表达式计算器 (企业版) 是调试引擎 (DE) 的一部分，用于处理生成正在调试的代码的编程语言的语法和语义。 必须在编程语言的上下文中对表达式进行求值。 例如，在某些语言中，表达式 "A + B" 表示 "A 和 B 的总和"。 在其他语言中，同一表达式可能表示 "A" 或 "B"。 因此，必须为每种编程语言编写一个单独的企业版，以在 Visual Studio IDE 中生成要调试的对象代码。

 Visual Studio 调试包的某些方面必须解释编程语言上下文中的代码。 例如，当执行在断点处暂停时，必须计算并显示用户在 " **监视** " 窗口中键入的任何表达式。 用户可以通过在 " **监视** " 窗口或 " **即时** " 窗口中键入表达式来更改本地变量的值。

## <a name="in-this-section"></a>本节内容
 [公共语言运行时和表达式计算](../../extensibility/debugger/common-language-runtime-and-expression-evaluation.md)说明在将专有编程语言集成到 Visual Studio IDE 中时，编写能够在专有语言的上下文中计算表达式的企业版允许您编译为 Microsoft 中间语言 (MSIL) ，无需编写调试引擎。

 [表达式计算器体系结构](../../extensibility/debugger/expression-evaluator-architecture.md)讨论如何实现所需的企业版接口，并调用公共语言运行时符号提供程序 (SP) 和联编程序接口。

 [注册表达式计算器](../../extensibility/debugger/registering-an-expression-evaluator.md)请注意，企业版必须使用公共语言运行时和 Visual Studio 运行时环境将自身注册为类工厂。

 [实现表达式计算器](../../extensibility/debugger/implementing-an-expression-evaluator.md)描述计算表达式的过程如何包含调试引擎 (DE) 、符号提供程序 (SP) 、联编程序对象和表达式计算器 (企业版) 。

 [显示局部变量](../../extensibility/debugger/displaying-locals.md) 描述如何在执行暂停时，调试包调用 DE 以获取局部变量和参数的列表。

 [计算监视窗口表达式](../../extensibility/debugger/evaluating-a-watch-window-expression.md)记录 Visual Studio 调试包如何调用 DE 来确定其监视列表中每个表达式的当前值。

 [更改本地的值](../../extensibility/debugger/changing-the-value-of-a-local.md) 说明在更改本地的值时，"局部变量" 窗口中的每一行都有一个关联的对象，该对象提供本地的名称、类型和当前值。

 [实现类型可视化工具和自定义查看](../../extensibility/debugger/implementing-type-visualizers-and-custom-viewers.md) 器说明需要由哪个组件实现哪个接口才能支持类型可视化工具和自定义查看器。

## <a name="see-also"></a>另请参阅
 [Visual Studio 调试器扩展性](../../extensibility/debugger/visual-studio-debugger-extensibility.md)

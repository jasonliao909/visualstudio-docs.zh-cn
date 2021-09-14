---
title: 公共语言运行时和表达式计算 |Microsoft Docs
description: 了解公共语言运行时如何与调试引擎交互，以及如何将专有编程语言集成到 Visual Studio IDE 中。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation, and common language runtime
ms.assetid: b36c1eb5-1aaf-48a6-b287-ee7a273d2b1c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 2c3c0566acf6a0216e5301cefceca061aae9d974
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600977"
---
# <a name="common-language-runtime-and-expression-evaluation"></a>公共语言运行时和表达式计算
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式计算器的方法已弃用。 有关实现 CLR 表达式计算器的信息，请参阅 [clr 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 编译器（如 Visual Basic 和 c # (以 c 升) 为目标，其目标为公共语言运行时 (CLR) ，生成 Microsoft 中间语言 (MSIL) ，后者稍后将编译为本机代码。 CLR 提供调试引擎 (DE) 调试生成的代码。 如果您计划将您的专有编程语言集成到 Visual Studio IDE 中，则可以选择编译为 MSIL，因此无需编写您自己的 DE。 但是，您必须将表达式计算器 (企业版) ，以便能够在您的编程语言的上下文中对表达式进行计算。

## <a name="discussion"></a>讨论 (Discussion)
 通常分析计算机语言表达式以生成一组数据对象和一组用于操作这些对象的运算符。 例如，可以对表达式 "A + B" 进行分析，以将加法运算符 (+) 应用于数据对象 "A" 和 "B"，可能导致其他数据对象。 数据对象、运算符及其关联的总集通常在程序中表示为一个树，其中的运算符位于树的节点和分支处的数据对象。 已分解为树形窗体的表达式通常称为已分析树。

 分析表达式后，将调用符号提供程序 (SP) 来计算每个数据对象。 例如，如果在多个方法中都定义了 "A"，则 "这是什么？" 问题 必须先进行应答，才能已确定的值。 SP 返回的答案类似于 "第三个堆栈帧上的第三项" 或 "在分配给此方法的静态内存开头以外的50字节"。

 除了为程序自身生成 MSIL 外，CLR 编译器还可以生成非常描述性的调试信息，将其写入 *到 (的* 程序数据库) 文件中。 只要专有语言编译器生成的调试信息的格式与 CLR 编译器的格式相同，CLR 的 SP 就可以识别该语言的命名数据对象。 标识了命名数据对象后，企业版使用联编程序对象将数据对象 (或绑定) 到包含该对象的值的内存区域。 然后，可以获取或设置数据对象的新值。

 专用编译器可以通过调用在 `ISymbolWriter` 命名空间) 的 .NET Framework 中定义的接口 (来提供 CLR 调试信息 `System.Diagnostics.SymbolStore` 。 通过编译为 MSIL 并通过这些接口编写调试信息，专用编译器可以使用 CLR DE 和 SP。 这极大地简化了将专用语言集成到 Visual Studio IDE 中的情况。

 当 CLR 取消调用专用企业版来计算表达式时，将向 SP 提供接口，并向其提供一个联编程序对象的企业版。 因此，编写基于 CLR 的调试引擎意味着只需实现适当的表达式计算器接口，CLR 负责处理绑定和符号处理。

## <a name="see-also"></a>另请参阅
- [编写 CLR 表达式计算器](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)

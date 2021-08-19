---
title: 公共语言运行时和表达式计算|Microsoft Docs
description: 了解公共语言运行时如何与调试引擎交互，以及如何将专有编程语言集成到 Visual Studio IDE。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122043617"
---
# <a name="common-language-runtime-and-expression-evaluation"></a>公共语言运行时和表达式计算
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式计算器的方法已弃用。 有关实现 CLR 表达式评估器的信息，请参阅 [CLR 表达式评估器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式评估器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 面向公共语言运行时 (CLR) 的编译器（如 Visual Basic 和 C# (发音为 C-sharp) ）生成 Microsoft 中间语言 (MSIL) ，该语言稍后将编译为本机代码。 CLR 提供调试引擎 (DE) 调试生成的代码。 如果计划将专有编程语言集成到 Visual Studio IDE 中，可以选择编译为 MSIL，因此无需编写自己的 DE。 但是，必须编写一个表达式 (企业版) ，该函数能够计算编程语言上下文中的表达式。

## <a name="discussion"></a>讨论 (Discussion)
 计算机语言表达式通常进行分析，以生成一组数据对象和一组用于操作这些数据对象的运算符。 例如，可以分析表达式"A+B"，以将加法运算符 (+) 应用于数据对象"A"和"B"，从而可能导致另一个数据对象。 数据对象、运算符及其关联的总集通常以树表示在程序中，其中运算符位于树的节点上，数据对象在分支处。 已分解为树形式的表达式通常称为分析树。

 分析表达式后，将调用 SP (提供程序) 以计算每个数据对象。 例如，如果"A"同时在多个方法中定义，则问题"哪个 A？" 必须先回答 ，然后才能确定 A 的值。 SP 返回的答案类似"第五个堆栈帧上的第三项"或"A，超出分配给此方法的静态内存的起始位置 50 字节。"

 除了为程序本身生成 MSIL 外，CLR 编译器还可以生成非常描述性的调试信息，这些信息将写入 .pdb (*Program DataBase*) 文件中。 只要专有语言编译器以与 CLR 编译器相同的格式生成调试信息，CLR 的 SP 就能识别该语言的命名数据对象。 标识命名数据对象后，企业版使用联编程序对象将 (或) 绑定到保存该对象值的内存区域。 然后，DE 可以获取或设置数据对象的新值。

 专有编译器可以通过调用接口接口来提供 CLR 调试信息， (命名空间中.NET Framework中定义的 `ISymbolWriter` `System.Diagnostics.SymbolStore` 接口) 。 通过编译为 MSIL 并通过这些接口写入调试信息，专有编译器可以使用 CLR DE 和 SP。 这大大简化了将专有语言集成到 Visual Studio IDE。

 当 CLR DE 调用专有企业版计算表达式时，DE 会企业版 SP 和联编程序对象的接口。 因此，编写基于 CLR 的调试引擎意味着只需实现适当的表达式计算程序接口;CLR 负责处理绑定和符号处理。

## <a name="see-also"></a>请参阅
- [编写 CLR 表达式计算程序](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)

---
title: 扩展调试器代码的|Microsoft Docs
description: Visual Studio调试文档包括示例、参考和演示自定义调试器的典型方法的几个方案。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], roadmap
- Debugging SDK, roadmap
ms.assetid: 1f4096a8-f7aa-4dfa-84e1-6d59263e70bb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 00da6cede11993e0b498978bc9a18ec0e21781b4
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602363"
---
# <a name="roadmap-for-extending-the-debugger"></a>扩展调试器路线图
本文档提供有关使用 扩展 [!INCLUDE[vs_current_short](../../code-quality/includes/vs_current_short_md.md)] 调试器的指导和参考信息 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] 。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 调试文档包括示例、一个全面的参考和几个演示自定义调试器的典型方法的代表性方案。

 编译器及其输出决定了在产品中设置调试所需的内容。 如果编译器：

- 面向Windows操作系统并写入 *。PDB* 文件，可以使用集成到 的 DE (DE) 本机代码调试引擎来调试程序 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 无需实现 DE 或表达式计算程序。 表达式计算程序是针对 C++ 编程语言的语法编写的。

- 生成 Microsoft 中间语言 (MSIL) 输出，可以使用托管代码调试引擎 DE 调试程序，该引擎也集成到 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 中。 因此，只需实现表达式计算程序。 提供了一个示例表达式计算程序。 有关详细信息，请参阅以下主题：

   [表达式计算](../../extensibility/debugger/expression-evaluation-visual-studio-debugging-sdk.md)

   [计算表达式](../../extensibility/debugger/evaluating-expressions.md)

   [表达式计算上下文](../../extensibility/debugger/expression-evaluation-context.md)

   [中断模式下的表达式计算](../../extensibility/debugger/expression-evaluation-in-break-mode.md)

   [编写公共语言运行时表达式计算程序](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)

- 面向专有操作系统或其他一些运行时环境，需要编写自己的 DE。 提供了使用 ATL COM 创建简单 DE 的教程。 有关详细信息，请参阅以下主题：

   [创建自定义调试引擎](../../extensibility/debugger/creating-a-custom-debug-engine.md)

   [教程：使用 ATL COM 生成调试引擎](/previous-versions/bb147024(v=vs.90))

   [实现端口供应商](../../extensibility/debugger/implementing-a-port-supplier.md)

   [示例](../../extensibility/debugger/visual-studio-debugging-samples.md)

## <a name="see-also"></a>另请参阅
- [入门](../../extensibility/debugger/getting-started-with-debugger-extensibility.md)
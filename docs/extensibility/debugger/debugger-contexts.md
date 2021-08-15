---
title: 调试器上下文 |Microsoft Docs
description: 了解 Visual Studio 调试引擎如何在不同的上下文中运行：代码上下文、文档上下文、位置和表达式计算上下文。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], contexts
ms.assetid: 79808036-b680-4e4c-9c61-4ed43aa11323
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 2d4df19ac3287788010a9db54cd1f237aaf13089b16e418068cbcd334dfc2cb3
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121343274"
---
# <a name="debugger-contexts"></a>调试器上下文
在 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 调试中，调试引擎 (DE) 在多个不同的上下文中同时运行，如下所示：

- 代码上下文，描述程序的执行流中的当前位置。

- 文档上下文或位置，描述源文档中的当前位置。

- 表达式计算上下文，描述将在其中发生表达式求值的上下文。

## <a name="in-this-section"></a>本节内容
 [代码上下文](../../extensibility/debugger/code-context.md) 在当今的运行时体系结构与 nontraditional 的语言中，将代码上下文讨论为程序指令流中的一个地址，其中，代码可能不由说明表示，而是其他一些方法。

 [文档位置](../../extensibility/debugger/document-position.md)在 Visual Studio 调试中定义文档位置，方法是通过将源文件中的位置抽象到 IDE 已知的方式进行调试。

 [文档上下文](../../extensibility/debugger/document-context.md)讨论相对于源文件 Visual Studio 调试中所代表的文档上下文。 还讨论了符号处理程序如何将代码上下文映射到文档上下文。

 [表达式计算上下文](../../extensibility/debugger/expression-evaluation-context.md)提供有关 Visual Studio 中的表达式计算上下文的信息。 例如，与堆栈帧关联的表达式计算上下文提供用于计算局部变量、方法参数和类成员的上下文。

## <a name="related-sections"></a>相关章节
 [调试概念](../../extensibility/debugger/debugger-concepts.md) 介绍主要调试体系结构概念。

 [调试组件](../../extensibility/debugger/debugger-components.md)概述 Visual Studio 调试组件，其中包括 (DE) 、表达式计算器 (企业版) 和符号处理程序 (SH) 的调试引擎。

 [调试任务](../../extensibility/debugger/debugging-tasks.md) 包含指向各种调试任务的链接，如启动程序和计算表达式。

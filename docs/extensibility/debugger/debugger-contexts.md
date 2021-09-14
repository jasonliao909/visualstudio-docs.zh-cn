---
title: 调试器上下文|Microsoft Docs
description: 了解Visual Studio引擎如何运行不同的上下文：代码上下文、文档上下文或位置以及表达式计算上下文。
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
ms.openlocfilehash: d7c06855b7ec216ec90d77fc0c0b9968d8da1be1
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664869"
---
# <a name="debugger-contexts"></a>调试器上下文
在 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 调试中，调试引擎 (DE) 在几个不同的上下文中同时运行，如下所示：

- 描述程序执行流中的当前位置的代码上下文。

- 文档上下文或位置，描述源文档中的当前位置。

- 表达式计算上下文，描述将在其中进行表达式计算的上下文。

## <a name="in-this-section"></a>本节内容
 [代码上下文](../../extensibility/debugger/code-context.md) 将代码上下文作为当前运行时体系结构中的程序指令流中的地址与非传统语言讨论，其中代码可能不会由指令表示，而是由其他一些方法表示。

 [文档位置](../../extensibility/debugger/document-position.md)通过使用 IDE 已知的Visual Studio在源文件中的位置抽象，定义文档在调试过程中的位置。

 [文档上下文](../../extensibility/debugger/document-context.md)讨论文档上下文在Visual Studio与源文件相关的调试中表示的内容。 还讨论符号处理程序如何将代码上下文映射到文档上下文。

 [表达式计算上下文](../../extensibility/debugger/expression-evaluation-context.md)提供有关表达式中表达式计算上下文Visual Studio。 例如，与堆栈帧关联的表达式计算上下文提供用于计算局部变量、方法参数和类成员的上下文。

## <a name="related-sections"></a>相关章节
 [调试概念](../../extensibility/debugger/debugger-concepts.md) 介绍主要调试体系结构概念。

 [调试组件](../../extensibility/debugger/debugger-components.md)概述 Visual Studio 调试组件，其中包括调试引擎 (DE) 、表达式 (企业版) 和符号处理程序 (SH) 。

 [调试任务](../../extensibility/debugger/debugging-tasks.md) 包含指向各种调试任务（如启动程序和评估表达式）的链接。

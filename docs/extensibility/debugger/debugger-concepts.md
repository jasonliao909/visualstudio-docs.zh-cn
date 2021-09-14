---
title: 调试器概念|Microsoft Docs
description: 了解设计调试包时所使用的Visual Studio概念，以帮助你基于该包进行生成。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK]
ms.assetid: 2d371d38-f1a0-4a9a-8ea3-100e8c0149b7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 2d407418d158adbd06dd64f998a1c6831b9f7cd1
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664870"
---
# <a name="debugger-concepts"></a>调试器概念
若要基于Visual Studio包进行构建，需要熟悉设计包时所使用的体系结构概念。

## <a name="in-this-section"></a>本节内容
 [调试会话](../../extensibility/debugger/debug-session.md) 说明会话在调试体系结构中的角色。

 [服务器](../../extensibility/debugger/servers-visual-studio-sdk.md) 以抽象和物理术语定义服务器在调试体系结构方面的概念。

 [端口供应商](../../extensibility/debugger/port-suppliers.md) 定义端口供应商在调试体系结构方面是什么。

 [端口](../../extensibility/debugger/ports.md) 定义端口在调试体系结构方面是什么。

 [进程](../../extensibility/debugger/processes.md) 定义进程在调试体系结构方面是什么。

 [程序节点](../../extensibility/debugger/program-nodes.md) 根据调试体系结构定义程序节点，包括它如何标识自身及其运行的进程。

 [程序](../../extensibility/debugger/programs.md) 根据调试体系结构定义程序。

 [线程数](../../extensibility/debugger/threads.md) 定义线程在调试体系结构方面的特征。

 [堆栈帧](../../extensibility/debugger/stack-frames.md) 根据调试体系结构定义堆栈帧。 堆栈帧是提供线程执行上下文的堆栈的抽象。

 [模块](../../extensibility/debugger/modules.md) 在调试体系结构方面，将模块定义为代码的物理容器，例如可执行文件或 DLL。

 [断点](../../extensibility/debugger/breakpoints-visual-studio-sdk.md) 根据调试体系结构定义三种类型的断点-挂起、绑定和错误。

## <a name="related-sections"></a>相关章节
 [调试器上下文](../../extensibility/debugger/debugger-contexts.md) 说明调试引擎如何 (DE) 代码、文档和表达式计算上下文中同时运行。 介绍这三个上下文的位置或相关评估。

 [调试器组件](../../extensibility/debugger/debugger-components.md)概述 Visual Studio 调试组件，其中包括调试引擎 (DE) 、表达式 (企业版) 和 SH (符号) 。

 [调试任务](../../extensibility/debugger/debugging-tasks.md) 包含指向各种调试任务（如启动程序和评估表达式）的链接。

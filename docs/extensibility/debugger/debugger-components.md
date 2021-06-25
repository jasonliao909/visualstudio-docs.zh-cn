---
title: 调试器组件|Microsoft Docs
description: 了解组成调试会话的元素，该会话由 Visual Studio器管理，作为 VSPackage 实现。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Visual Studio], components
- components [Visual Studio SDK], debugging
- debugging [Debugging SDK], components
ms.assetid: 8b8ab77f-a134-495c-be42-3bc51aa62dfb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8c246bc00ee4f6fcead8404b3174da39f7b5ca2d
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112903978"
---
# <a name="debugger-components"></a>调试器组件
调试 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 器作为 VSPackage 实现，并管理整个调试会话。 调试会话包含以下元素：

- **调试包：**[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]无论正在调试什么内容，调试器都提供相同的用户界面。

- **会话调试管理器 (SDM) ：** 为调试器提供一致的编程 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 接口，用于管理各种调试引擎。 它由 实现 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

- **处理 PDM (调试) ：** 管理所有正在运行的 实例的列表，该列表包含可调试或 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 正在调试的所有程序。 它由 实现 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

- **调试引擎 (DE) ：** 负责监视正在调试的程序，将正在运行的程序的状态与 SDM 和 PDM 通信，并与表达式评估器与符号提供程序交互，以提供程序内存和变量的状态实时分析。 它是通过 (语言实现的，) 希望支持自己的运行时的提供商和第三方 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 供应商。

- **EE (表达式) ：** 支持在程序停止于特定点时动态计算用户提供的变量和表达式。 它由 (支持的语言实现) 希望支持自己的语言的第三方 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 供应商。

- **符号提供程序 (SP) ：** 也称为符号处理程序，将程序的调试符号映射到正在运行的程序实例，以便提供有意义的信息 (如源代码级调试和表达式计算) 。 它由 (针对公共语言运行时 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] [CLR] 符号和 Program DataBase [PDB] 符号文件格式) 以及由具有自己的专用方法来存储调试信息的第三方供应商实现。

  下图显示了调试器中这些元素Visual Studio关系。

  ![调试组件概述](../../extensibility/debugger/media/dbugcompovrview.gif "DBugCompOvrview")

## <a name="in-this-section"></a>在本节中
 [调试包](../../extensibility/debugger/debug-package.md) 讨论调试包，该包在 shell 中 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 运行并处理所有 UI。

 [进程调试管理器](../../extensibility/debugger/process-debug-manager.md) 概述 PDM 的功能，它是可调试的进程的管理器。

 [会话调试管理器](../../extensibility/debugger/session-debug-manager.md) 定义 SDM，它为 IDE 提供调试会话的统一视图。 SDM 管理 DE。

 [调试引擎](../../extensibility/debugger/debug-engine.md) 记录 DE 提供的调试服务。

 [操作模式](../../extensibility/debugger/operational-modes.md) 概述 IDE 可操作的三种模式：设计模式、运行模式和中断模式。 还讨论了转换机制。

 [表达式计算程序](../../extensibility/debugger/expression-evaluator.md) 说明 EE 运行时的用途。

 [符号提供程序](../../extensibility/debugger/symbol-provider.md) 讨论实现时符号提供程序如何计算变量和表达式。

 [类型可视化工具与自定义查看器](../../extensibility/debugger/type-visualizer-and-custom-viewer.md) 讨论类型可视化工具与自定义查看器是什么，以及表达式计算程序在支持这两者方面所扮演的角色。

## <a name="related-sections"></a>相关章节
 [调试器概念](../../extensibility/debugger/debugger-concepts.md) 介绍主要的调试体系结构概念。

 [调试器上下文](../../extensibility/debugger/debugger-contexts.md) 说明 DE 如何在代码、文档和表达式评估上下文中同时运行。 介绍这三个上下文的位置或相关评估。

 [调试任务](../../extensibility/debugger/debugging-tasks.md) 包含指向各种调试任务（如启动程序和评估表达式）的链接。

## <a name="see-also"></a>另请参阅
- [入门](../../extensibility/debugger/getting-started-with-debugger-extensibility.md)

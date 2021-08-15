---
title: 调试器组件 |Microsoft Docs
description: 了解组成调试会话的元素，该会话由 Visual Studio 调试程序管理，以 VSPackage 的形式实现。
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
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: d2ebe084538388174d1c205ab101ade465c694f955c3f481598edb0b1da60827
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121324140"
---
# <a name="debugger-components"></a>调试器组件
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]调试器以 VSPackage 的形式实现并管理整个调试会话。 调试会话包含以下元素：

- **调试包：** 无论 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 正在调试什么内容，调试器都提供相同的用户界面。

- **会话调试管理器 (SDM) ：** 为调试器提供一致的编程接口， [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 用于管理各种调试引擎。 它由实现 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

- **进程调试管理器 (PDM) ：** 管理所有正在运行的实例的 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ，其中列出了所有可以或正在调试的程序。 它由实现 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

- **调试引擎 (DE) ：** 负责监视正在调试的程序，将正在运行的程序的状态传达给 SDM 和 PDM，并与表达式计算器和符号提供程序交互，以便实时分析程序的内存和变量的状态。 它是由 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 它所支持的语言的 (实现的，) 以及想要支持其自己的运行时间的第三方供应商。

- **表达式计算器 (企业版) ：** 为在特定点停止程序时，动态计算用户提供的变量和表达式提供支持。 它是由 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 它所支持的语言的 (实现的，) 以及要支持其自己语言的第三方供应商。

- **符号提供程序 (SP) ：** 也称为符号处理程序，将程序的调试符号映射到程序的正在运行的实例，以便可以 (提供有意义的信息，如源代码级调试和表达式计算) 。 它是由 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 公共语言运行时 [CLR] 符号和程序数据库 [PDB] 符号文件) 格式 (实现的，而第三方供应商拥有自己的存储调试信息的专有方法。

  下图显示了 Visual Studio 调试器的这些元素之间的关系。

  ![调试组件概述](../../extensibility/debugger/media/dbugcompovrview.gif "DBugCompOvrview")

## <a name="in-this-section"></a>本节内容
 [调试包](../../extensibility/debugger/debug-package.md) 讨论在 shell 中运行 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 并处理所有 UI 的调试包。

 [进程调试管理器](../../extensibility/debugger/process-debug-manager.md) 概述 PDM 的功能，这是可以调试的进程的管理器。

 [会话调试管理器](../../extensibility/debugger/session-debug-manager.md) 定义 SDM，后者向 IDE 提供调试会话的统一视图。 SDM 管理 DE。

 [调试引擎](../../extensibility/debugger/debug-engine.md) 记录 DE 提供的调试服务。

 [操作模式](../../extensibility/debugger/operational-modes.md) 概述 IDE 可以操作的三种模式：设计模式、运行模式和中断模式。 还介绍了转换机制。

 [表达式计算器](../../extensibility/debugger/expression-evaluator.md)说明企业版在运行时的用途。

 [符号提供程序](../../extensibility/debugger/symbol-provider.md) 讨论在实现时，符号提供程序如何计算变量和表达式。

 [类型可视化工具和自定义查看器](../../extensibility/debugger/type-visualizer-and-custom-viewer.md) 讨论什么是类型可视化工具和自定义查看器，以及表达式计算器在支持两者时所扮演的角色。

## <a name="related-sections"></a>相关章节
 [调试器概念](../../extensibility/debugger/debugger-concepts.md) 介绍主要的调试体系结构概念。

 [调试器上下文](../../extensibility/debugger/debugger-contexts.md) 说明 DE 如何在代码、文档和表达式评估上下文中同时运行。 介绍这三个上下文的位置或相关评估。

 [调试任务](../../extensibility/debugger/debugging-tasks.md) 包含指向各种调试任务的链接，如启动程序和计算表达式。

## <a name="see-also"></a>另请参阅
- [入门](../../extensibility/debugger/getting-started-with-debugger-extensibility.md)

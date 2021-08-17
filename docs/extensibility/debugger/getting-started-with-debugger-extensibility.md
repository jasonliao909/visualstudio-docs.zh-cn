---
title: 入门调试器扩展性|Microsoft Docs
description: 开始创建和自定义调试器组件，这些调试器组件用于在Visual Studio程序。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- getting started, Debugging SDK
- debugging [Debugging SDK], getting started
- Debugging SDK, getting started
ms.assetid: d6ce6f43-1409-4bf7-93cd-f3464ca23504
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 87f6ff3bb423a32af3e5bf6fb1a25a016d367556
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122043552"
---
# <a name="get-started-with-debugger-extensibility"></a>调试器扩展性入门
提供创建和自定义调试器组件（用于从环境中调试程序 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] ） [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 所需的信息。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 调试添加了从在以前的调试器上执行的广泛可用性测试 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 派生的改进。 可以使用调试单步执行多语言应用程序，或者可以在调试应用程序和多语言解决方案时实现变量 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 的"即点即用"编辑。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 调试在进程外执行，程序正在调试，因此在应用程序的进程空间中侵入性较低。 因此，可以更轻松地编写与调试器交互的组件，而不会影响调试程序。

 若要充分利用 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] ，应熟悉以下各项：

- [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]集成开发环境 (IDE) 

- C++ 编程语言

- ATL COM

## <a name="in-this-section"></a>本节内容
 [扩展调试器路线图](../../extensibility/debugger/roadmap-for-extending-the-debugger.md) 概述在产品中实现调试的过程，具体取决于编译器及其输出。

 [调试器组件](../../extensibility/debugger/debugger-components.md)概述调试组件，其中包括调试引擎 (DE) 、表达式 (企业版) 以及 SH ([!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 符号) 。

 [调试器概念](../../extensibility/debugger/debugger-concepts.md) 介绍主要的调试体系结构概念。

 [调试器上下文](../../extensibility/debugger/debugger-contexts.md) 说明调试引擎如何 (DE) 代码、文档和表达式计算上下文中同时运行。 介绍这三个上下文的位置或相关评估。

 [调试任务](../../extensibility/debugger/debugging-tasks.md) 包含指向各种调试任务（如启动程序和评估表达式）的链接。

---
title: Visual Studio调试器扩展性|Microsoft Docs
description: 本文介绍Visual Studio扩展性，并提供指向有关调试Visual Studio的链接。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Visual Studio], Debugging SDK
- Debugging SDK
ms.assetid: c088b6a2-c3ad-446b-830d-9c6f41b2934b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 3949777d22f6cb47469e035a84dbbc484ab210a663420f31bd4a67c4a21cd487
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121306031"
---
# <a name="visual-studio-debugger-extensibility"></a>Visual Studio调试器扩展性
Visual Studio包含一个完全交互式的源代码调试器，提供一个功能强大且易于使用的工具，用于跟踪程序中的 bug。 调试器完全支持 Visual Basic、C#、C/C++ 和 JavaScript。 但是，借助 Microsoft 下载中心提供的 ，调试器中可以使用相同丰富功能支持 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] 其他编程语言。 [](https://www.microsoft.com/download/details.aspx?id=21835)

 调试器是常见的前端 (，即用户界面) 调试组件，而调试组件又特定于要调试 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 的语言。 对于新语言，调试器支持所需的全部操作就是创建必要的后端组件，例如 DE ([!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 调试) 。 这一点是 进入 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] 的地方。

 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]包括对创建新 DE 所需的所有 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 元素的完整引用。 此外，还有可帮助你入门的示例和教程。

 有关支持调试的语言项目系统的完整示例，请参阅 [IronPython 示例](https://www.microsoft.com/download/details.aspx?id=55984)。

 以下部分介绍如何使用 扩展调试器 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] 。

## <a name="in-this-section"></a>本节内容
 [入门](../../extensibility/debugger/getting-started-with-debugger-extensibility.md) 介绍 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 调试提供哪些功能以及如何安装 SDK。

 [创建自定义调试引擎](../../extensibility/debugger/creating-a-custom-debug-engine.md) 记录自定义 DE 过程，从为 DE 准备程序到分离 DE。

 [编写 CLR 表达式计算程序](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md) 说明是否必须编写表达式计算程序。

 [选择调试引擎实现策略](../../extensibility/debugger/choosing-a-debug-engine-implementation-strategy.md) 讨论如何实现 DE。

 [参考](../../extensibility/debugger/reference/reference-visual-studio-debugging-apis.md) 记录 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 调试 API。

 [示例](../../extensibility/debugger/visual-studio-debugging-samples.md) 包含指向公共语言运行时表达式评估程序示例和调试引擎示例的链接。

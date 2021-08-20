---
title: 选择调试引擎实现策略|Microsoft Docs
description: 了解运行时体系结构如何帮助你从调试引擎实现的几个策略中选择。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, implementation strategies
ms.assetid: 90458fdd-2d34-4f10-82dc-6d8f31b66d8b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 22077acd9e669f82d274a11a2b983c01afd1f746
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122111783"
---
# <a name="choose-a-debug-engine-implementation-strategy"></a>选择调试引擎实现策略
使用运行时体系结构来确定调试引擎 (DE) 实现策略。 可以在正在调试的程序的进程内创建调试引擎。 使用 SDM 脚本在进程内Visual Studio调试管理器 (引擎) 。 或者，在进程外为两者创建调试引擎。 以下指南应有助于在这三种策略中选择。

## <a name="guidelines"></a>指南
 虽然 DE 可能会进程外同时对 SDM 和正在调试的程序执行，但通常没有这样做的理由。 跨进程边界的调用相对较慢。

 调试引擎已针对 Win32 本机运行时环境和公共语言运行时环境提供。 如果必须替换任一环境的 DE，则应该使用 SDM 在进程内创建 DE。

 否则，在 SDM 的进程内或正在调试的程序的进程内创建 DE。 需要考虑 DE 的表达式计算程序是否需要频繁访问程序符号存储。 或者，如果符号存储可以加载到内存中以快速访问。 此外，请考虑以下方法：

- 如果表达式计算器与符号存储之间没有多个调用，或者如果符号存储可以读入 SDM 内存空间，则创建 SDM 的 DE 进程内。 当调试引擎附加到程序时，必须将调试引擎的 CLSID 返回到 SDM。 SDM 使用此 CLSID 创建 DE 的进程内实例。

- 如果 DE 必须调用程序来访问符号存储，则使用该程序创建 DE 进程内。 在这种情况下，程序将创建 DE 的实例。

## <a name="see-also"></a>请参阅
- [Visual Studio调试器扩展性](../../extensibility/debugger/visual-studio-debugger-extensibility.md)

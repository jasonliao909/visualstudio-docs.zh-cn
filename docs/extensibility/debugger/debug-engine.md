---
title: 调试引擎|Microsoft Docs
description: 了解调试引擎如何与解释器或操作系统一起提供执行控制、断点和表达式计算等服务。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debug engines
ms.assetid: 148b1efc-ca07-4d8e-bdfc-c723a760c620
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 16b82ce91fea9fe3b841b449651d42c66a82af32302332d94eded8bb6f6076bc
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121390501"
---
# <a name="debug-engine"></a>调试引擎
调试引擎 (DE) 与解释器或操作系统一起提供调试服务，例如执行控制、断点和表达式计算。 DE 负责监视正在调试的程序的状态。 为此，DE 将使用受支持的运行时中可用于它的任何方法，无论是来自 CPU 还是来自运行时提供的 API。

 例如，公共语言运行时 (CLR) 提供通过 ICorDebugXXX 接口监视正在运行的程序的机制。 支持 CLR 的 DE 使用相应的 ICorDebugXXX 接口来跟踪正在调试的托管代码程序。 然后，它将状态的任何更改传达给 SDM (的会话) 管理器，该管理器将此类信息转发到 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE。

> [!NOTE]
> 调试引擎面向特定的运行时，即正在调试的程序运行的系统。 CLR 是托管代码的运行时，Win32 运行时用于本机Windows应用程序。 如果创建的语言可以面向这两个运行时之一，则 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 已提供必要的调试引擎。 你实现的所有都是表达式计算程序。

## <a name="debug-engine-operation"></a>调试引擎操作
 监视服务通过 DE 接口实现，可能会导致调试包在不同操作模式之间转换。 有关详细信息，请参阅操作 [模式](../../extensibility/debugger/operational-modes.md)。 每个运行时环境通常只有一个 DE 实现。

> [!NOTE]
> 虽然 Transact-SQL 和 有单独的 DE 实现 [!INCLUDE[jsprjscript](../../debugger/debug-interface-access/includes/jsprjscript_md.md)] ，但 VBScript 和 [!INCLUDE[jsprjscript](../../debugger/debug-interface-access/includes/jsprjscript_md.md)] 共享单个 DE。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 调试使调试引擎能够运行以下两种方式之一：在 shell 的同一进程中，或与正在调试的目标程序 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 相同的进程中。 当正在调试的进程实际上是在解释器下运行的脚本时，通常会发生后一种形式。 调试引擎必须了解解释器才能监视脚本。 在这种情况下，解释器实际上是运行时;调试引擎适用于特定的运行时实现。 此外，可以跨进程和计算机边界拆分单个 DE 的实现 (例如远程调试) 。

 DE 公开 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 调试接口。 所有通信都通过 COM 进行。 无论 DE 是在进程内、进程外还是在另一台计算机中加载，它都不会影响组件通信。

 DE 与表达式计算器组件一起工作，使该特定运行时的 DE 能够理解表达式的语法。 DE 还使用符号处理程序组件来访问语言编译器生成的符号调试信息。 有关详细信息，请参阅表达式[计算程序和](../../extensibility/debugger/expression-evaluator.md)[符号提供程序](../../extensibility/debugger/symbol-provider.md)。

## <a name="see-also"></a>另请参阅
- [调试器组件](../../extensibility/debugger/debugger-components.md)
- [表达式计算程序](../../extensibility/debugger/expression-evaluator.md)
- [符号提供程序](../../extensibility/debugger/symbol-provider.md)

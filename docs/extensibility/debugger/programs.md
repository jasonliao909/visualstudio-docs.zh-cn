---
title: 程序|Microsoft Docs
description: 本文介绍程序在调试器体系结构中的定义和Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], programs
- programs, debugging
ms.assetid: e1f955d8-95da-493b-837e-e97741a26d7e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 0c19e92bdfb7a7f015cdf23fea12657e9f5813f155b761c6894bc9d943841b63
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121434524"
---
# <a name="programs"></a>Programs
在调试器体系结构中，程序 *：*

- 是一组线程和一组模块的容器。 程序在操作系统中没有Windows类。

     程序是一种子进程。 例如，调试网站时，可以将脚本视为程序。 虽然脚本在脚本引擎进程中运行，而与其他脚本无关，但它也有其自己的线程集。 调试引擎 (DE) 附加到程序，而不是附加到进程或线程。

- 可以标识自身及其运行的进程。 程序可以附加到、从中分离，并描述创建它的 DE（如果有）。 程序还可以执行、停止、继续和终止。

- 可以枚举其所有线程。 程序还可以提供自己的反汇编流，并可以枚举给定文档位置的所有代码上下文。

- 由 [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md) 接口表示，该接口在附加程序之前创建，或在附加过程中创建，具体取决于实现。 当端口枚举进程的程序时，根据作为参数传递给[AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)的相应[IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)接口创建每个程序。 虽然调试引擎还会创建接口来表示程序，但是这些程序不是根据程序节点 `IDebugProgram2` 创建的。 DE 创建的接口用于实际调试，而端口创建的接口仅用于发现进程中 `IDebugProgramNode2` 正在运行的程序。

## <a name="see-also"></a>另请参阅
- [进程](../../extensibility/debugger/processes.md)
- [程序节点](../../extensibility/debugger/program-nodes.md)
- [模块](../../extensibility/debugger/modules.md)
- [调试器概念](../../extensibility/debugger/debugger-concepts.md)
- [调试引擎](../../extensibility/debugger/debug-engine.md)
- [文档位置](../../extensibility/debugger/document-position.md)
- [代码上下文](../../extensibility/debugger/code-context.md)
- [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)
- [AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)

---
title: 程序 |Microsoft Docs
description: 本文介绍 Visual Studio 中调试器体系结构中的程序的定义和角色。
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
ms.openlocfilehash: 0fcbd1d6ac01d4d67ad03193c1fa2b2e75ded6d5
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122160330"
---
# <a name="programs"></a>Programs
在调试程序体系结构中， *程序*：

- 是一组线程和一组模块的容器。 在 Windows 操作系统中，程序没有任何一个类比。

     程序是一种子进程。 例如，在调试网站时，可以将脚本视为程序。 尽管脚本在脚本引擎进程中运行（与其他脚本无关），但它还具有自己的一组线程。 调试引擎 (DE) 附加到程序，而不是进程或线程。

- 可以标识自身及其正在运行的进程。 程序可以附加到，也可以从中分离出来，并说明创建它的 DE （如果有）。 程序还可以执行、停止、继续和终止。

- 可以枚举其所有线程。 程序还可以提供自己的反汇编流，还可以枚举给定文档位置的所有代码上下文。

- 由在附加程序之前创建的 [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md) 接口表示，或作为附加过程的一部分，具体取决于实现。 当端口枚举进程的程序时，将根据作为参数传递到[AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)的相应[IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)接口创建每个程序。 尽管调试引擎还 `IDebugProgram2` 会创建接口来表示程序，但不会根据程序节点创建这些程序。 `IDebugProgramNode2`由 DE 创建的接口用于实际调试，而由端口创建的接口仅用于发现进程中运行的程序。

## <a name="see-also"></a>请参阅
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

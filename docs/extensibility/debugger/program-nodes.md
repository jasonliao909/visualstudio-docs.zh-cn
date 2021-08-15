---
title: 程序节点|Microsoft Docs
description: 本文介绍中调试器体系结构中程序节点的定义和Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- program nodes, debugging context
- debugging [Debugging SDK], program nodes
- program nodes, adding
- program nodes, superceding
ms.assetid: 1c5a5c13-c14d-42c3-af11-4c63f1032c8d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: e0066f6b8ee17591620af896c753dbd9b29a5948790d024c5b505be76f34cb75
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121417764"
---
# <a name="program-nodes"></a>程序节点
在调试器体系结构中，程序 *节点：*

- 程序的轻量说明。

- 可以标识自身及其运行的进程。 程序节点可以附加到、从中分离，并描述创建 (DE) 调试引擎（如果有）。

- 由通常由 DE 或端口创建的 [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md) 接口表示。 通过调用 [AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)将程序节点添加到端口。 将程序节点添加到端口时，会添加到包含此程序节点表示的程序的进程。

  启动调试会话后的某个时间，根据调试包的实现，程序节点用于创建相应的程序。 查询进程的程序时，将枚举程序，每个程序节点一个程序节点。

  在将程序附加到之前，IDE 只需要程序的轻型说明。 可以从程序节点获取此信息。 程序附加到 后，IDE 会显示更详细的信息，例如程序中运行的所有线程的列表。 此信息从程序本身获取。

## <a name="see-also"></a>另请参阅
- Programs 
- [进程](../../extensibility/debugger/processes.md)
- [调试引擎](../../extensibility/debugger/debug-engine.md)
- [调试器概念](../../extensibility/debugger/debugger-concepts.md)
- [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)
- [AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)

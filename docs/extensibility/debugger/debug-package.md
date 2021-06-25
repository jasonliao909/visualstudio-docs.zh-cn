---
title: 调试包|Microsoft Docs
description: 了解调试包如何在 Visual Studio shell 中运行，并通过使用调试接口并与会话调试管理器通信来处理 UI。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], packages
ms.assetid: 99947fd4-fb87-4c69-b26c-65634e17d285
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8be920ae352067a6e77593ca0a922474d68851d9
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112905665"
---
# <a name="debug-package"></a>调试包
调试包在 Visual Studio shell 中运行，并处理所有 UI。 它使用Visual Studio接口，并与 SDM (会话调试管理器) 。

 通过 SDM 发送的中断事件将调试器从运行模式切换到中断模式，将焦点更改为发生中断的程序。 调试包从事件发送给堆栈帧和线程的信息中跟踪堆栈帧和线程。

 调试包没有语言或运行时环境依赖项。 不需要实现或修改调试包。

 调试包由 *vsdebug.dll。*

## <a name="see-also"></a>另请参阅
- [会话调试管理器](../../extensibility/debugger/session-debug-manager.md)
- [堆栈帧](../../extensibility/debugger/stack-frames.md)
- [线程](../../extensibility/debugger/threads.md)
- [调试器组件](../../extensibility/debugger/debugger-components.md)

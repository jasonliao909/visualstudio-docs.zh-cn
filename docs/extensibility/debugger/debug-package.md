---
title: 调试包 |Microsoft Docs
description: 了解调试包在 Visual Studio shell 中的运行方式，并通过使用调试接口并与会话调试管理器通信来处理 UI。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], packages
ms.assetid: 99947fd4-fb87-4c69-b26c-65634e17d285
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: c2692f99388fe5cba3103605480dda1f27b62ff3
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122153597"
---
# <a name="debug-package"></a>调试包
调试包在 Visual Studio shell 中运行并处理所有 UI。 它使用 Visual Studio 调试接口，并与会话调试管理器 (SDM) 通信。

 中断通过 SDM 发送的事件将调试器从运行模式切换为中断模式，并将焦点更改为发生中断的程序。 调试包跟踪事件发送到的堆栈帧和线程。

 调试包没有语言或运行时环境依赖项。 不需要实现或修改调试包。

 调试包由 *vsdebug.dll* 实现。

## <a name="see-also"></a>请参阅
- [会话调试管理器](../../extensibility/debugger/session-debug-manager.md)
- [堆栈帧](../../extensibility/debugger/stack-frames.md)
- [线程](../../extensibility/debugger/threads.md)
- [调试器组件](../../extensibility/debugger/debugger-components.md)

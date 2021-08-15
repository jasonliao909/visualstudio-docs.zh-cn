---
title: 服务器 (Visual Studio SDK) |Microsoft Docs
description: 本文介绍 Visual Studio 中调试器体系结构中服务器的定义和角色。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- servers, debugging
- debugging [Debugging SDK], servers
ms.assetid: 62236d64-7956-448c-9ac3-5528f3edac1d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 402e6df722cb0c5e3bceb88614e0b137e3ef5e488378c357b3788a441e59baa4
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121432925"
---
# <a name="servers-visual-studio-sdk"></a>服务器 (Visual Studio SDK)
在调试程序体系结构中， *服务器*：

- 是端口和端口供应商的容器，可将端口和端口供应商传达给会话调试管理器 (SDM) 和调试引擎。

- 可以按名称标识自身，并枚举其端口和端口供应商。

- 由[IDebugCoreServer2](../../extensibility/debugger/reference/idebugcoreserver2.md)接口表示，此接口仅通过 Visual Studio (运行) 的每个 Visual Studio 实例的服务器实例来实现。

## <a name="see-also"></a>另请参阅
- [端口](../../extensibility/debugger/ports.md)
- [端口供应商](../../extensibility/debugger/port-suppliers.md)
- [调试器概念](../../extensibility/debugger/debugger-concepts.md)
- [IDebugCoreServer2](../../extensibility/debugger/reference/idebugcoreserver2.md)

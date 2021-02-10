---
title: Visual Studio SDK)  (服务器 |Microsoft Docs
description: 本文介绍 Visual Studio 的调试器结构中的服务器的定义和角色。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- servers, debugging
- debugging [Debugging SDK], servers
ms.assetid: 62236d64-7956-448c-9ac3-5528f3edac1d
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d60c214fce57f5958d8b30ca231c3e8a2bc05194
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99960801"
---
# <a name="servers-visual-studio-sdk"></a>服务器 (Visual Studio SDK)
在调试程序体系结构中， *服务器*：

- 是端口和端口供应商的容器，可将端口和端口供应商传达给会话调试管理器 (SDM) 和调试引擎。

- 可以按名称标识自身，并枚举其端口和端口供应商。

- 由 [IDebugCoreServer2](../../extensibility/debugger/reference/idebugcoreserver2.md) 接口表示，此接口仅由 visual studio 为运行) 的每个 visual studio 实例 (服务器的一个实例实现。

## <a name="see-also"></a>另请参阅
- [端口](../../extensibility/debugger/ports.md)
- [端口供应商](../../extensibility/debugger/port-suppliers.md)
- [调试器概念](../../extensibility/debugger/debugger-concepts.md)
- [IDebugCoreServer2](../../extensibility/debugger/reference/idebugcoreserver2.md)

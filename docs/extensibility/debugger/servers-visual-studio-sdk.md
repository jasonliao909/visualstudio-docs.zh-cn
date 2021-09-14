---
title: 服务器 (Visual Studio SDK) |Microsoft Docs
description: 本文介绍服务器在调试器体系结构中的定义和Visual Studio。
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
ms.openlocfilehash: 06317f9249371076ddc306ac5a38e3fe764996f7
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600834"
---
# <a name="servers-visual-studio-sdk"></a>服务器 (Visual Studio SDK)
在调试器体系结构中，服务器 *：*

- 是端口和端口供应商的容器，将端口和端口供应商与会话调试管理器通信 (SDM) 引擎。

- 可以按名称标识自身，并枚举其端口和端口供应商。

- 由[IDebugCoreServer2](../../extensibility/debugger/reference/idebugcoreserver2.md)接口表示，该接口仅由运行) 的每个实例Visual Studio (一个服务器实例Visual Studio实现。

## <a name="see-also"></a>另请参阅
- [端口](../../extensibility/debugger/ports.md)
- [端口供应商](../../extensibility/debugger/port-suppliers.md)
- [调试器概念](../../extensibility/debugger/debugger-concepts.md)
- [IDebugCoreServer2](../../extensibility/debugger/reference/idebugcoreserver2.md)

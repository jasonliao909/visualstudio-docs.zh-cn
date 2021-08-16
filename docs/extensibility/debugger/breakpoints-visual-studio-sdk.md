---
title: SDK (Visual Studio断) |Microsoft Docs
description: 了解三种类型的断点：挂起、绑定和错误。 本文列出了用于实现类型的接口。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- breakpoints
ms.assetid: acfcabed-9f2f-436c-ad18-7ca2f45d631b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: c023119e621addb65b758bfbd17909d663f4e61451797c398b8123b2095ffd96
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121452506"
---
# <a name="breakpoints-visual-studio-sdk"></a>断点 (Visual Studio SDK)
有三种类型的断点：挂起、绑定和错误。

 **挂起的断点：**

- 一个抽象，包含将断点绑定到一个或多个程序中的一个或多个代码上下文所需的全部信息。 每次调试的程序导致加载代码时，调试引擎会检查所有挂起的断点，看它们是否可绑定。

   挂起的断点本身永远不会绑定到代码，而是收集并包含它生成的所有绑定断点。

- 由 [IDebugPendingBreakpoint2 接口](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md) 表示。

  **绑定断点：**

- 与单个代码上下文关联或绑定到单个代码上下文的断点的抽象。 生成每个绑定断点以响应挂起的断点。 但是，挂起的断点可以生成多个绑定断点。

   卸载代码时，绑定断点可以取消绑定并丢弃。

- 由 [IDebugBoundBreakpoint2 接口](../../extensibility/debugger/reference/idebugboundbreakpoint2.md) 表示。

  **错误断点：**

- 一个抽象，用于描述尝试将挂起断点绑定到代码上下文时的错误。 错误断点描述位置或断点表达式本身中的错误。 有关详细信息，请参阅 [绑定断点](../../extensibility/debugger/binding-breakpoints.md)。

   断点错误可以是错误或警告。

- 由 [IDebugErrorBreakpoint2 接口](../../extensibility/debugger/reference/idebugerrorbreakpoint2.md) 表示。

## <a name="see-also"></a>另请参阅
- Programs 
- [调试器概念](../../extensibility/debugger/debugger-concepts.md)
- [代码上下文](../../extensibility/debugger/code-context.md)
- [IDebugBoundBreakpoint2](../../extensibility/debugger/reference/idebugboundbreakpoint2.md)
- [IDebugPendingBreakpoint2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
- [IDebugErrorBreakpoint2](../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)

---
title: " (Visual Studio SDK) 的断点 |Microsoft Docs"
description: 了解下面三种类型的断点：挂起、绑定和错误。 本文列出了用于实现类型的接口。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- breakpoints
ms.assetid: acfcabed-9f2f-436c-ad18-7ca2f45d631b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1fce472faf95aa77f87ab02d78a3da640b6bd3bf
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901482"
---
# <a name="breakpoints-visual-studio-sdk"></a>断点 (Visual Studio SDK)
有三种类型的断点： "挂起"、"绑定" 和 "错误"。

 **挂起的断点：**

- 是一个抽象，其中包含将断点绑定到一个或多个程序中的一个或多个代码上下文所需的所有信息。 每次被调试的程序导致加载代码时，调试引擎都会检查所有挂起的断点，以确定它们是否可以绑定。

   挂起的断点本身从不绑定到代码，而是收集并被视为包含其生成的所有绑定断点。

- 由 [IDebugPendingBreakpoint2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md) 接口表示。

  **绑定断点：**

- 与关联的断点的抽象，或绑定到单个代码上下文的断点。 每个绑定断点都是为响应挂起断点而生成的。 但挂起的断点可以生成多个绑定断点。

   卸载代码时，绑定断点可以取消绑定并被丢弃。

- 由 [IDebugBoundBreakpoint2](../../extensibility/debugger/reference/idebugboundbreakpoint2.md) 接口表示。

  **错误断点：**

- 用于描述尝试将挂起断点绑定到代码上下文的错误的抽象。 错误断点描述位置或断点表达式本身中的错误。 有关详细信息，请参阅 [绑定断点](../../extensibility/debugger/binding-breakpoints.md)。

   断点错误可以是错误或警告。

- 由 [IDebugErrorBreakpoint2](../../extensibility/debugger/reference/idebugerrorbreakpoint2.md) 接口表示。

## <a name="see-also"></a>另请参阅
- Programs 
- [调试器概念](../../extensibility/debugger/debugger-concepts.md)
- [代码上下文](../../extensibility/debugger/code-context.md)
- [IDebugBoundBreakpoint2](../../extensibility/debugger/reference/idebugboundbreakpoint2.md)
- [IDebugPendingBreakpoint2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
- [IDebugErrorBreakpoint2](../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)

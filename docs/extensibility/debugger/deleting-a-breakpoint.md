---
title: 删除断点 |Microsoft Docs
description: 了解会话调试管理器如何在删除挂起断点时删除挂起的断点以及从该断点绑定的所有绑定断点。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- breakpoints, deleting
- debugging [Debugging SDK], deleting breakpoints
ms.assetid: 75a046cc-d20a-4c79-ad2d-1f18426ac5d0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: ff1d0af4ceedc8ebd4659b44e0a316919e54a92aca9a3a0341c9f9d184e439b3
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121343247"
---
# <a name="deleting-a-breakpoint"></a>删除断点
下面描述了删除挂起断点时的过程：

## <a name="deletion-process"></a>删除过程
 会话调试管理器 (SDM) 调用 [IDebugPendingBreakpoint2：:D e) ](../../extensibility/debugger/reference/idebugpendingbreakpoint2-delete.md) 方法来删除挂起的断点以及从该断点绑定的所有绑定断点。

> [!NOTE]
> 还可以通过调用 [IDebugBoundBreakpoint2：:D e) ](../../extensibility/debugger/reference/idebugboundbreakpoint2-delete.md)删除单个绑定断点。

## <a name="see-also"></a>另请参阅
- [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md)

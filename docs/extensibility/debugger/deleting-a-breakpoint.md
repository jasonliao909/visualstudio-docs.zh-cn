---
title: 删除断点|Microsoft Docs
description: 了解会话调试管理器如何在删除挂起断点时删除挂起的断点以及绑定的所有断点。
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
ms.openlocfilehash: adaa20e57670148c9c7129c5c31d5de6da915515
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122073339"
---
# <a name="deleting-a-breakpoint"></a>删除断点
下面描述了删除挂起断点的过程：

## <a name="deletion-process"></a>删除过程
 会话调试管理器 (SDM) 调用 [IDebugPendingBreakpoint2：:D elete](../../extensibility/debugger/reference/idebugpendingbreakpoint2-delete.md) 方法以删除挂起的断点和绑定的所有断点。

> [!NOTE]
> 也可通过调用 [IDebugBoundBreakpoint2：:D删除单个绑定断点](../../extensibility/debugger/reference/idebugboundbreakpoint2-delete.md)。

## <a name="see-also"></a>请参阅
- [调用调试器事件](../../extensibility/debugger/calling-debugger-events.md)

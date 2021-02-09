---
title: 代码上下文 |Microsoft Docs
description: 了解 Visual Studio 中的代码上下文调试，其中描述了程序在断点处停止时存在的代码中的位置。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], contexts
ms.assetid: 65e4d37a-086b-426e-9394-a3534967fd59
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 685650e0e97c3f9851f051fdaa78f86252597ff8
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99930715"
---
# <a name="code-context"></a>代码上下文
在 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 调试中， **代码上下文**：

- 在代码中提供对调试引擎已知的位置的抽象 (DE) 。 对于今天的大多数运行时结构，可以将代码上下文视为程序的指令流中的地址。 对于 nontraditional 语言，其中的代码不能通过说明进行表示，代码上下文可以用其他方式表示。

- 描述正在调试的程序的执行流中的当前位置。

- 仅当程序在断点处停止时才存在。

- 具有关联的文档上下文。

- 由 [IDebugCodeContext2](../../extensibility/debugger/reference/idebugcodecontext2.md) 接口实现。

## <a name="see-also"></a>另请参阅
- [文档上下文](../../extensibility/debugger/document-context.md)
- [调试器上下文](../../extensibility/debugger/debugger-contexts.md)

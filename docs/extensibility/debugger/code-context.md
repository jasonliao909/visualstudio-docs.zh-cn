---
title: 代码上下文|Microsoft Docs
description: 了解调试中的Visual Studio上下文，该上下文描述程序在断点处停止时存在于代码中的位置。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], contexts
ms.assetid: 65e4d37a-086b-426e-9394-a3534967fd59
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 774daabac461c00998048455f4e23bd2ab7bd379
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122111796"
---
# <a name="code-context"></a>代码上下文
在 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 调试中，代码 **上下文：**

- 提供调试引擎在代码中已知位置的抽象 (DE) 。 对于目前大多数运行时体系结构，可以将代码上下文视为程序指令流中的地址。 对于非传统语言（其中代码可能不能由指令表示）而言，代码上下文可能由其他某种方式表示。

- 描述正在调试的程序的执行流中的当前位置。

- 仅在程序在断点处停止时存在。

- 具有关联的文档上下文。

- 由 [IDebugCodeContext2 接口](../../extensibility/debugger/reference/idebugcodecontext2.md) 实现。

## <a name="see-also"></a>请参阅
- [文档上下文](../../extensibility/debugger/document-context.md)
- [调试器上下文](../../extensibility/debugger/debugger-contexts.md)

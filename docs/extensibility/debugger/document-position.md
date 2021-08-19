---
title: 文档位置 |Microsoft Docs
description: 了解 Visual Studio 调试中的文档位置如何在源文件中提供 IDE 已知的位置抽象。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], contexts
ms.assetid: b59d739c-7572-427f-a70d-4e5df63d02c1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 458c9f9dad2bdb3484cd9a67a643b446d129fa23
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122153571"
---
# <a name="document-position"></a>文档位置
在 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 调试中， *文档位置*：

- 在源文件中提供对 IDE 已知的位置的抽象。 目前大多数语言都可以将文档位置视为源文件中的位置。

- 描述源文档中到调试引擎的位置。

- 由 [IDebugDocumentPosition2](../../extensibility/debugger/reference/idebugdocumentposition2.md) 接口实现。

## <a name="see-also"></a>请参阅
- [代码上下文](../../extensibility/debugger/code-context.md)
- [文档上下文](../../extensibility/debugger/document-context.md)
- [符号提供程序](../../extensibility/debugger/symbol-provider.md)
- [符号提供程序接口](../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [调试器上下文](../../extensibility/debugger/debugger-contexts.md)

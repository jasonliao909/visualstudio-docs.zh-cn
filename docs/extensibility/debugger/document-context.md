---
title: 文档上下文 |Microsoft Docs
description: 了解 Visual Studio 中的文档上下文调试，它表示源文件中的位置或代码上下文的源文档中的位置。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], contexts
ms.assetid: 8e8b5702-5c16-4988-953d-69dd807d8b84
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 34c69e11c57574c07a8ecb40480842834a8ee53f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105097235"
---
# <a name="document-context"></a>文档上下文
在 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 调试中， *文档上下文*：

- 表示源文件中的位置。 对于源文件可能不存在的语言，文档上下文标识通常由运行时环境生成的文档中的位置。 例如，脚本引擎可能通过脚本生成文档。 有关详细信息，请参阅 [文档位置](../../extensibility/debugger/document-position.md)。

- 描述与代码上下文对应的源文档中的位置。 符号处理程序使用由编译器或解释器生成的信息将代码上下文映射到文档上下文。

- 由 [IDebugDocumentContext2](../../extensibility/debugger/reference/idebugdocumentcontext2.md) 接口实现。

## <a name="see-also"></a>另请参阅
- [代码上下文](../../extensibility/debugger/code-context.md)
- [符号提供程序](../../extensibility/debugger/symbol-provider.md)
- [符号提供程序接口](../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [调试器上下文](../../extensibility/debugger/debugger-contexts.md)

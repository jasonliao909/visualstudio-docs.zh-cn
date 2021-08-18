---
title: 文档上下文|Microsoft Docs
description: 了解调试中的Visual Studio上下文，它表示源文件中的位置或代码上下文的源文档中的位置。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], contexts
ms.assetid: 8e8b5702-5c16-4988-953d-69dd807d8b84
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 776e7d92d1763888700532f9e7ecac7bdfd52b5d
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122043591"
---
# <a name="document-context"></a>文档上下文
在 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 调试中，文档 *上下文：*

- 表示源文件中的位置。 对于可能不存在源文件的语言，文档上下文标识通常由运行时环境生成的文档中的位置。 例如，脚本引擎可能会从脚本生成文档。 有关详细信息，请参阅文档 [位置](../../extensibility/debugger/document-position.md)。

- 描述源文档中与代码上下文相对应的位置。 符号处理程序使用编译器或解释器生成的信息将代码上下文映射到文档上下文。

- 由 [IDebugDocumentContext2 接口](../../extensibility/debugger/reference/idebugdocumentcontext2.md) 实现。

## <a name="see-also"></a>请参阅
- [代码上下文](../../extensibility/debugger/code-context.md)
- [符号提供程序](../../extensibility/debugger/symbol-provider.md)
- [符号提供程序接口](../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [调试器上下文](../../extensibility/debugger/debugger-contexts.md)

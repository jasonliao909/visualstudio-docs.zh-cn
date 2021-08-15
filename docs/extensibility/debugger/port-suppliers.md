---
title: 端口供应商 |Microsoft Docs
description: 本文介绍了 Visual Studio 的调试器体系结构中的端口供应商的定义和角色。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- port suppliers
- debugging [Debugging SDK], port suppliers
ms.assetid: a8f3db96-1a13-4e93-9ef6-0861880369e0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 96eaaea45afc5b61334d8a1701c02768d3176bc5707cdd931dd6b94ab67337ae
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121452519"
---
# <a name="port-suppliers"></a>端口供应商
在调试程序体系结构中， *端口供应商*：

- 包含在服务器中，并提供对该服务器的请求的端口。

- 可以在包含服务器中添加和删除端口。

- 可以枚举它提供给服务器的所有端口。

- 由[IDebugPortSupplier2](../../extensibility/debugger/reference/idebugportsupplier2.md)接口表示，该接口通过注册表注册到 Visual Studio。 此接口可通过调用 [GetPortSupplier](../../extensibility/debugger/reference/idebugcoreserver2-getportsupplier.md)获取。

  [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 提供默认端口供应商和默认端口。 如果需要实现自定义端口，还需要实现自定义端口提供商以提供这些自定义端口。

## <a name="see-also"></a>另请参阅
- [服务器](../../extensibility/debugger/servers-visual-studio-sdk.md)
- [端口](../../extensibility/debugger/ports.md)
- [调试器概念](../../extensibility/debugger/debugger-concepts.md)
- [IDebugPortSupplier2](../../extensibility/debugger/reference/idebugportsupplier2.md)
- [GetPortSupplier](../../extensibility/debugger/reference/idebugcoreserver2-getportsupplier.md)

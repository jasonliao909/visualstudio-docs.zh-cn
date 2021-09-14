---
title: 截获旧版语言服务命令|Microsoft Docs
description: 了解如何在 Visual Studio命令筛选器来截获旧版语言服务命令并添加特定于语言的行为。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, intercepting language service
- language services, intercepting commands
ms.assetid: eea69f03-349c-44bb-bd4f-4925c0dc3e55
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 6f82e3cb15b39359c78f28a42e62d65665f34dba
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600729"
---
# <a name="intercepting-legacy-language-service-commands"></a>截获旧版语言服务命令
使用 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ，你可以使语言服务截获文本视图将处理的命令。 这适用于文本视图不管理的语言特定行为。 可以通过从语言服务向文本视图添加一个或多个命令筛选器来截获这些命令。

## <a name="getting-and-routing-the-command"></a>获取和路由命令
 命令筛选器是监视 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 某些字符序列或键命令的对象。 可以将多个命令筛选器与单个文本视图关联。 每个文本视图都维护一系列命令筛选器。 创建新的命令筛选器后，将筛选器添加到相应文本视图的链中。

 在 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> 上调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 方法，将命令筛选器添加到链中。 调用 时 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> ，将返回另一个命令筛选器，你可以将命令筛选器未处理的命令 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 传递给该筛选器。

 可以使用以下命令处理选项：

- 处理 命令，然后将命令传递给链中的下一个命令筛选器。

- 处理命令，不要将命令传递给下一个命令筛选器。

- 不要处理命令，而是将命令传递给下一个命令筛选器。

- 忽略 命令。 请不要在当前筛选器中处理它，并且不要将它传递给下一个筛选器。

  有关语言服务应处理哪些命令的信息，请参阅语言 [服务筛选器的重要命令](../../extensibility/internals/important-commands-for-language-service-filters.md)。

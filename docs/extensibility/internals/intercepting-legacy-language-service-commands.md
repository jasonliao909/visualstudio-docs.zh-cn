---
title: 截获旧版语言服务命令 |Microsoft Docs
description: 了解如何使用 Visual Studio 中的命令筛选器来截获旧版语言服务命令并添加特定于语言的行为。
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
ms.openlocfilehash: cc17db226176bf806a594778d6a483a713b97b606c1fa662f1c65d3cf01ee3d2
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121375918"
---
# <a name="intercepting-legacy-language-service-commands"></a>截获旧版语言服务命令
使用 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ，你可以让语言服务截获文本视图要处理的命令。 这对于文本视图不管理的特定于语言的行为很有用。 可以通过将一个或多个命令筛选器添加到语言服务中的文本视图来截获这些命令。

## <a name="getting-and-routing-the-command"></a>获取并路由命令
 命令筛选器是 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 监视某些字符序列或键命令的对象。 可以将多个命令筛选器与一个文本视图关联。 每个文本视图维护一系列命令筛选器。 创建新的命令筛选器后，将筛选器添加到相应文本视图的链。

 调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> 上的方法 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> ，将命令筛选器添加到链。 调用时 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> ，将 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 返回另一个命令筛选器，你可以将命令筛选器不处理的命令传递给该筛选器。

 你有以下命令处理选项：

- 处理该命令，然后将命令传递到链中的下一个命令筛选器。

- 处理该命令，并不要将命令传递到下一个命令筛选器。

- 不要处理此命令，但将命令传递到下一个命令筛选器。

- 忽略命令。 请勿在当前筛选器中对其进行处理，并且不要将其传递到下一个筛选器。

  有关语言服务应处理哪些命令的信息，请参阅 [语言服务筛选器的重要命令](../../extensibility/internals/important-commands-for-language-service-filters.md)。

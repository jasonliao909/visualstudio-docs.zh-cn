---
title: 使用和提供服务 |Microsoft Docs
description: 了解 Visual Studio IDE 为 vspackage 提供的、提供和使用的服务。 这些文章介绍了如何获取和提供服务。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- examples [Visual Studio SDK], services
- Visual Studio, services
- services
ms.assetid: c0b415ba-b825-4da0-9faf-8a60a663e302
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: c230e0e573c19fe5f53e70d6c7a4ec1f6814d6d6
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122109950"
---
# <a name="using-and-providing-services"></a>使用并提供服务
服务是两个 Vspackage 之间的协定。 一个 VSPackage 为其他要使用的 VSPackage 提供一组特定的接口。 例如， [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] <xref:Microsoft.VisualStudio.Shell.Interop.SVsActivityLog> 为它加载的任何 VSPackage 提供服务。 此服务提供 <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog> 接口，该接口可用于写入活动日志。 有关详细信息，请参阅 [如何：使用活动日志](../extensibility/how-to-use-the-activity-log.md)。

 Vspackage 可以使用接口来提供自己的服务 <xref:Microsoft.VisualStudio.Shell.Interop.IProfferService> 。

 Visual Studio 提供重要的服务，如下所示：

|IDE 服务|说明|
|-----------------|-----------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsShell>|提供对处理基本功能、Vspackage 和注册表的 IDE 服务的访问。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>|提供 IDE 中与窗口和 UI 相关的基本功能，如创建工具和文档窗口的功能。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>|提供与解决方案相关的基本功能，例如枚举项目、创建新项目和监视项目更改的能力。|

## <a name="in-this-section"></a>本节内容
- [服务基础](../extensibility/internals/service-essentials.md)显示 Visual Studio 服务的重要元素。

- [如何：获取服务](../extensibility/how-to-get-a-service.md) 讨论如何请求) 服务 (使用。

- [如何：提供服务](../extensibility/how-to-provide-a-service.md) 讨论如何提供服务。

- [如何：提供异步 Visual Studio 服务](../extensibility/how-to-provide-an-asynchronous-visual-studio-service.md)讨论如何提供异步服务。

- [如何：排除服务故障](../extensibility/how-to-troubleshoot-services.md) 讨论了常见问题并向其提供了解决方案。

## <a name="related-sections"></a>相关章节
- [Visual Studio SDK](../extensibility/visual-studio-sdk.md)

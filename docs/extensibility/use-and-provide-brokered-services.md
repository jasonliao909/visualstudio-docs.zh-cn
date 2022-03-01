---
title: 使用和提供中转服务
description: 了解 IDE 和扩展Visual Studio提供的中转服务。 这些文章介绍如何获取和提供中转服务。
monikerRange: '>= vs-2019'
ms.custom: SEO-VS-2020
ms.date: 01/06/2022
ms.topic: conceptual
helpviewer_keywords:
- examples [Visual Studio SDK], brokered services
- Visual Studio, brokered services
- brokered services
ms.assetid: d2b743f2-a06b-4f82-aaef-f207046a299e
author: aarnott
ms.author: andarno
manager: ansonh
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 3ab73aaa97771573f59fd879da9915f73a76ca64
ms.sourcegitcommit: 169b7b66d13b7e3c86097b42206dd33389cd9166
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2022
ms.locfileid: "138153484"
---
# <a name="using-and-providing-brokered-services"></a>使用和提供中转服务

中转服务<xref:Microsoft.ServiceHub.Framework.IServiceBroker>是通过 获取的服务，作为与 RPC 兼容的接口公开，使服务及其客户端能够存在于不同的 AppDomain、进程甚至跨计算机 (（如果为 Live Share) ）。

VS 包可以使用 接口提供自己的 <xref:Microsoft.VisualStudio.Shell.ServiceBroker.IBrokeredServiceContainer> 服务。

[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 提供重要的中转服务，例如：

|中转服务|说明|
|-----------------|-----------------|
|<xref:Microsoft.VisualStudio.RpcContracts.OutputChannel.IOutputChannelStore>|允许将文本流式处理到输出窗口。
|<xref:Microsoft.VisualStudio.RpcContracts.OpenDocument.IOpenDocumentService>|允许打开文档。
|<xref:Microsoft.VisualStudio.RpcContracts.FileSystem.IFileSystem>|允许访问本地或远程文件系统。

## <a name="in-this-section"></a>在本节中
- [中转服务 Essentials](internals/brokered-service-essentials.md)呈现中转服务Visual Studio的重要元素，以及它们与其他服务的区别[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]。

- [发现可用的中转服务](internals/discover-available-brokered-services.md) 介绍如何发现可用的中转服务集。

- [如何：获取中转服务](how-to-consume-brokered-service.md) 讨论如何请求使用 (服务) 服务。

- [如何：提供中转服务](how-to-provide-brokered-service.md) 讨论如何提供中转服务。

## <a name="related-sections"></a>相关章节
- [Visual Studio SDK](visual-studio-sdk.md)

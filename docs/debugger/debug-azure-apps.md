---
title: 调试 Azure 服务 | Microsoft Docs
description: 可以使用 Visual Studio 调试 Azure 服务。 使用本文中的链接可了解执行此操作的各种方式。
ms.custom: SEO-VS-2020
ms.date: 09/14/2018
ms.topic: how-to
helpviewer_keywords:
- debugger
ms.assetid: 3d434de3-ee5f-419d-9a94-ac4ac02d635b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- azure
ms.openlocfilehash: d28bf31d5a7f7fe6a2bd095a0f96c76cccc35152
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122031341"
---
# <a name="debug-azure-services-in-visual-studio"></a>使用 Visual Studio 调试 Azure 服务

可以使用 Visual Studio 在不同的场景中调试 Azure 服务：

若要调试托管的生产应用：

- 使用 Visual Studio Enterprise 调试 Azure 应用服务中托管的生产应用，请参阅[使用 Snapshot Debugger 调试实时 ASP.NET 应用](../debugger/debug-live-azure-applications.md)。

- 使用 Application Insights 调试 Azure 应用服务或 Service Fabric 中托管的生产应用，请参阅 [.NET 应用中发生异常时的调试快照](/azure/application-insights/app-insights-snapshot-debugger)。

- 调试 Azure 虚拟机或 Azure 虚拟机规模集中托管的生产应用，请参阅[使用 Snapshot Debugger 调试实时 ASP.NET Azure 虚拟机和 Azure 虚拟机规模集](../debugger/debug-live-azure-virtual-machines.md)。

- 调试 Azure Kubernetes 服务中托管的生产应用，请参阅[使用 Snapshot Debugger 调试实时 ASP.NET Azure Kubernetes 服务](../debugger/debug-live-azure-kubernetes.md)。

若要远程调试：

- IIS（Azure 应用服务或 Azure VM）上的 ASP.NET，请参阅[远程调试 Azure 上的 ASP.NET](remote-debugging-azure.md)。

- Azure Service Fabric 上的 ASP.NET，请参阅[调试远程 Service Fabric 应用程序](/azure/service-fabric/service-fabric-debugging-your-application#debug-a-remote-service-fabric-application)

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中进行调试](../debugger/index.yml)

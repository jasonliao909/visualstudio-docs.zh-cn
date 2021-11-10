---
title: Azure 集成
description: 了解如何在 Visual Studio 中开发 Azure 应用程序和服务，并将它们部署到云。
author: ghogen
manager: jmartens
ms.technology: vs-azure
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: overview
ms.date: 10/19/2021
ms.author: ghogen
monikerRange: '>=vs-2019'
ms.openlocfilehash: 6d03b18236c46f4130312839e8c84bac4716a5d2
ms.sourcegitcommit: 32fa8ec0b469a7a9a87de25ff769d8d21d9f30d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2021
ms.locfileid: "131898334"
---
# <a name="overview-azure-integration"></a>概述：Azure 集成

可在 Visual Studio 中使用许多旨在简化向 Azure 的开发和部署的功能来使用 Azure。

## <a name="provision-azure-resources"></a>预配 Azure 资源

这是一个典型的 Visual Studio 对话框，可在其中浏览和搜索现有的 Azure 资源。 在现有资源列表的上方，有一个按钮，可用于预配新资源：

:::moniker range="vs-2019"
![显示如何选择 Azure 资源的屏幕截图。](./media/select-azure-resource.png)
:::moniker-end
:::moniker range=">=vs-2022"
![显示如何选择 Azure 资源的屏幕截图。](./media/vs-2022/select-azure-resource.png)
:::moniker-end

> [!NOTE]
> 此示例显示了 Azure 应用服务的实例，但 Visual Studio 支持的所有 Azure 服务都有一个类似的对话框。

## <a name="browse-and-search-existing-azure-resources"></a>浏览和搜索现有的 Azure 资源

以下屏幕截图显示了一个典型的 Visual Studio 对话框，可在其中浏览和搜索现有的 Azure 资源。

1. 可使用下拉菜单按 Azure 订阅进行筛选
2. 可按资源组或资源类型对找到的实例进行分组（这实际上为你提供了一个简单列表）
3. 可按资源名称进行搜索

:::moniker range="vs-2019"
![显示如何浏览和搜索 Azure 资源的屏幕截图](./media/browse-search-azure-resource.png)
:::moniker-end
:::moniker range=">=vs-2022"
![显示如何浏览和搜索 Azure 资源的屏幕截图](./media/vs-2022/browse-search-azure-resource.png)
:::moniker-end

> [!NOTE]
> 此示例显示了 Azure 应用服务的实例，但 Visual Studio 支持的所有 Azure 服务都有一个类似的对话框。

## <a name="deploy-an-application-to-azure-using-publish-or-github-actions"></a>使用发布向导或 GitHub Actions 将应用程序部署到 Azure

在[解决方案资源管理器](../ide/use-solution-explorer.md)中右键单击你的项目，然后从上下文菜单中选择“发布”。 发布向导将引导你完成整个体验，并且如果你的项目托管在 GitHub.com 上，你还将自动获得使用 GitHub Actions 配置 CI/CD 的机会。

## <a name="configure-azure-dependencies-to-be-emulated-locally-and-connect-to-real-services-at-deployment-time"></a>将 Azure 依赖项配置为在本地进行仿真，并在部署时连接到实际服务

使用连接的服务将应用程序连接到本地仿真器和 Azure 服务的其他本地替代项。 首先，右键单击解决方案资源管理器中的“连接的服务”节点，然后选择“管理连接的服务” 。

:::moniker range="vs-2019"
![显示本地 Azure 仿真器的屏幕截图。](./media/local-azure-emulators.png)
:::moniker-end
:::moniker range=">=vs-2022"
![显示本地 Azure 仿真器的屏幕截图。](./media/vs-2022/local-azure-emulators.png)
:::moniker-end

## <a name="debug-azure-function-projects-offline-without-cost"></a>免费脱机调试 Azure 函数项目

开始调试时，Visual Studio 将在本地无缝地仿真 Azure Functions 服务。 你甚至不必使用 Azure 订阅进行登录。

## <a name="remote-debug-azure-hosting-services-like-azure-app-service"></a>远程调试 Azure 托管服务，如 Azure 应用服务

请参阅[使用 Visual Studio 调试器附加到正在运行的进程](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md#attach-to-a-net-core-process-running-on-azure-app-service-windows)

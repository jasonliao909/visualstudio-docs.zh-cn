---
title: 发布 Azure 云服务
description: 了解如何在 Visual Studio“发布 Azure 应用程序”向导中配置各种设置
author: ghogen
manager: jmartens
ms.technology: vs-azure
ms.workload: azure-vs
ms.topic: how-to
ms.date: 03/21/2017
ms.author: ghogen
ms.openlocfilehash: 0d58f664117f28439ea6a3d98d77fd5da0ab27ea
ms.sourcegitcommit: 8fae163333e22a673fd119e1d2da8a1ebfe0e51a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2021
ms.locfileid: "129969094"
---
# <a name="using-the-visual-studio-publish-azure-application-wizard"></a>使用 Visual Studio“发布 Azure 应用程序”向导 | Microsoft Docs

在 Visual Studio 中开发 Web 应用程序后，可以使用 **发布 Azure 应用程序** 向导将该应用程序发布到 Azure 云服务。

## <a name="accessing-the-publish-azure-application-wizard"></a>访问“发布 Azure 应用程序”向导

可以通过两种方式访问“发布 Azure 应用程序”向导，具体取决于所使用的 Visual Studio 项目类型。

**如果使用的是 Azure 云服务项目：**

1. 在 Visual Studio 中创建或打开 Azure 云服务项目。

1. 在“解决方案资源管理器”中右键单击项目，并从上下文菜单中选择“发布”。

**如果使用的是未为 Azure 启用的 Web 应用程序项目：**

1. 在 Visual Studio 中创建或打开 Azure 云服务项目。

1. 在“解决方案资源管理器”中右键单击项目，并从上下文菜单中选择“转换” > “转换为 Azure 云服务项目”。

1. 在“解决方案资源管理器”中右键单击新创建的 Azure 项目，并从上下文菜单中选择“发布”。

## <a name="sign-in-page"></a>登录页

![登录页](./media/vs-azure-tools-publish-azure-application-wizard/sign-in.png)

**帐户** - 选择一个帐户，或者在帐户下拉列表中选择“添加帐户”。

**选择订阅** - 选择要用于部署的订阅。

## <a name="settings-page---common-settings-tab"></a>“设置”页 -“常用设置”选项卡

![通用设置](./media/vs-azure-tools-publish-azure-application-wizard/settings-common-settings.png)

**云服务** - 使用下拉列表选择现有的云服务，或者选择“&lt;新建>”创建一个云服务。 每个云服务的数据中心均显示在括号中。 建议云服务的数据中心位置与存储帐户的数据中心位置相同（高级设置）。

**环境** - 选择“生产”或“过渡”。 如果要在测试环境中部署应用程序，请选择过渡环境。

**生成配置** - 选择“调试”或“发布”。

**服务配置** - 选择“云”或“本地”。

**为所有角色启用远程桌面** - 如果希望能够远程连接到服务，请选中此选项。 此选项主要用于故障排除。 有关详细信息，请参阅[使用 Visual Studio 为 Azure 云服务中的角色启用远程桌面连接](/azure/cloud-services/cloud-services-role-enable-remote-desktop-visual-studio)。

**为所有 Web 角色启用 Web 部署** - 选中此选项为服务启用 Web 部署。 还必须选择“为所有角色启用远程桌面”选项才能使用此功能。 有关详细信息，请参阅[使用 Visual Studio 发布云服务](vs-azure-tools-publishing-a-cloud-service.md)。

## <a name="settings-page---advanced-settings-tab"></a>“设置”页 -“高级设置”选项卡

![高级设置](./media/vs-azure-tools-publish-azure-application-wizard/settings-advanced-settings.png)

**部署标签** - 接受默认名称，或者输入所选的名称。 要将日期附加到部署标签，请保留选中相应的复选框。

**存储帐户** - 选择要用于此部署的存储帐户，或者单击“&lt;新建>”创建一个存储帐户。 每个存储帐户的数据中心均显示在括号中。 建议存储帐户的数据中心位置与云服务的数据中心位置相同（常用设置）。

Azure 存储帐户将存储应用程序部署的包。 部署应用程序之后，将从存储帐户中删除该包。

**失败时删除部署** - 选择此选项可在发布期间遇到任何错误时会部署删除。 如果要保留云服务的不变虚拟 IP 地址，则应取消选中此项。

**部署更新** - 如果希望仅部署更新的组件，请选择此选项。 这种部署类型比完整部署更快速。 如果要保留云服务的不变虚拟 IP 地址，则应选中此项。

**部署更新 - 设置** - 此对话框用于进一步指定要更新角色的方式。 如果选择“增量更新”，则会一个接一个地更新应用程序的每个实例，以使应用程序始终可用。 如果选择“同时更新”，则会同时更新应用程序的所有实例。 同时更新速度更快，但在更新过程中服务可能不可用。

![部署设置](./media/vs-azure-tools-publish-azure-application-wizard/deployment-settings.png)

**启用 IntelliTrace** - 指定是否要启用 IntelliTrace。 通过 IntelliTrace，可以在某个角色实例在 Azure 中运行时记录该角色实例的大量调试信息。 如果需要查找问题的原因，可以从 Visual Studio 使用 IntelliTrace 日志来单步执行代码，就像它在 Azure 中运行一样。 有关使用 IntelliTrace 的详细信息，请参阅[使用 Visual Studio 和 IntelliTrace 调试已发布的 Azure 云服务](./vs-azure-tools-intellitrace-debug-published-cloud-services.md)。

**启用分析** - 指定是否要启用性能分析。 使用 Visual Studio 探查器，可以获取云服务在计算方面运行情况的深入分析。 有关使用 Visual Studio 探查器的详细信息，请参阅[测试 Azure 云服务的性能](./vs-azure-tools-performance-profiling-cloud-services.md)。

**为所有角色启用远程调试器** - 指定是否要启用远程调试。 有关使用 Visual Studio 调试云服务的详细信息，请参阅[在 Visual Studio 中调试 Azure 云服务或虚拟机](./vs-azure-tools-debug-cloud-services-virtual-machines.md)。

## <a name="diagnostics-settings-page"></a>“诊断设置”页

![诊断设置](./media/vs-azure-tools-publish-azure-application-wizard/diagnostic-settings.png)

通过诊断，可以对 Azure 云服务（或 Azure 虚拟机）进行故障排除。 有关诊断的详细信息，请参阅 [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)（为 Azure 云服务和虚拟机配置诊断）。 有关 Application Insights 的信息，请参阅[什么是 Application Insights？](/azure/application-insights/app-insights-overview)。

## <a name="summary-page"></a>“摘要”页

![“摘要”页](./media/vs-azure-tools-publish-azure-application-wizard/summary.png)

**目标配置文件** - 可以选择基于所选的设置创建发布配置文件。 例如，可以创建一个配置文件用于测试环境，并创建另一个配置文件用于生产环境。 要保存此配置文件，请选择 **“保存”** 图标。 向导将创建配置文件并将它保存在 Visual Studio 项目中。 要修改配置文件名称，请打开“目标概况”列表，并选择“&lt;管理…&gt;”。 

   > [!Note]
   > 发布配置文件将出现在 Visual Studio 的解决方案资源管理器中，配置文件设置将写入扩展名为.azurePubxml 的文件。 设置将保存为 XML 标记的属性。

## <a name="publishing-your-application"></a>发布应用程序

配置项目部署的所有设置后，请选择对话框底部的“发布”。 你可以在 Visual Studio 的 **“输出”** 窗口中监视进程状态。

## <a name="next-steps"></a>后续步骤

- [通过 Visual Studio 将 Web 应用程序迁移和发布到 Azure 云服务](./vs-azure-tools-migrate-publish-web-app-to-cloud-service.md)

- [了解如何使用 Visual Studio 发布 Azure 云服务](./vs-azure-tools-publishing-a-cloud-service.md)

- [使用 Visual Studio 和 IntelliTrace 调试已发布的 Azure 云服务](./vs-azure-tools-intellitrace-debug-published-cloud-services.md)

- [测试 Azure 云服务的性能](./vs-azure-tools-performance-profiling-cloud-services.md)

- [为 Azure 云服务和虚拟机配置诊断](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)。

- [什么是 Application Insights？](/azure/application-insights/app-insights-overview)

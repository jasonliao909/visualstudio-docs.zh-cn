---
title: 使用云资源管理器管理 Azure 资源 | Microsoft Docs
description: 了解如何使用云资源管理器来浏览和管理 Visual Studio 中的 Azure 资源。
author: ghogen
manager: jmartens
ms.technology: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 03/25/2017
ms.author: ghogen
ms.openlocfilehash: eba0fbc1dc2cb6feced3e52f3f4b6dfbce1fa1d4
ms.sourcegitcommit: 7a820b7698a8dcf076eb36e3d766fb0751f56bb1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2021
ms.locfileid: "131126527"
---
# <a name="manage-the-resources-associated-with-your-azure-accounts-in-visual-studio-cloud-explorer"></a>在 Visual Studio Cloud Explorer 中管理与 Azure 帐户关联的资源

::: moniker range=">=vs-2022"
> [!Important]
> Cloud Explorer已在 2022 年Visual Studio停用。 可以改为使用以下替代方法：
> - 使用[Microsoft Azure 存储资源管理器](/azure/vs-azure-tools-storage-manage-with-storage-explorer)是 Microsoft 提供的免费独立应用。 可以通过它在 Windows、macOS 和 Linux 上直观地使用 Azure 存储数据。
> - 若要调试 Azure 应用服务 或 Azure Function 应用，可以使用所有项目连接的服务或"发布"功能。 如果依赖于Visual Studio，则此选项在"托管"部分的其他选项下可用。 如果不使用发布功能，则你将能够从"连接服务"选项卡连接到任何 Azure 应用服务 或 Azure Function 应用，并调用各种操作，例如远程调试、远程配置文件、启动/停止站点、查看流式处理日志等。 
> - 使用 [Kudu 控制台](https://github.com/projectkudu/kudu/wiki/Kudu-console)可直接以提升的命令行访问应用服务服务器及其文件系统。 这是一个重要的调试工具，同时也支持 CLI 操作（如安装包）。
>
> 如果需要，可以使用 Azure 门户或继续使用以前版本中服务器资源管理器的 Azure Visual Studio。
>
> 有关 2022 Visual Studio，请参阅[发行说明](/visualstudio/releases/2022/release-notes-preview/)。

::: moniker-end

::: moniker range="<=vs-2019"

通过 Cloud Explorer，可在 Visual Studio 中查看 Azure 资源和资源组、检查其属性，以及执行重要的开发人员诊断操作。

与 [Azure 门户](https://portal.azure.com)一样，Cloud Explorer 基于 Azure 资源管理器堆栈。 因此，Cloud Explorer 可以识别 Azure 资源组等资源，以及逻辑应用和 API 应用等 Azure 服务，并支持[基于角色的访问控制](/azure/role-based-access-control/role-assignments-portal) (RBAC)。

## <a name="prerequisites"></a>先决条件

* Visual Studio 2017 或更高版本（请参阅[Visual Studio 下载](https://visualstudio.microsoft.com/downloads)），已选择“Azure 工作负载”。 还可以使用带有 Microsoft Azure SDK for .NET 2.9 的 Visual Studio 早期版本。
* Microsoft Azure 帐户 - 如果没有帐户，可以[注册免费试用帐户](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers/)，或者[激活 Visual Studio 订户权益](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers/)。

> [!NOTE]
> 若要查看Cloud Explorer，请按 **Ctrl** Q 激活搜索框，然后输入 + Cloud Explorer。 

## <a name="add-an-azure-account-to-cloud-explorer"></a>将 Azure 帐户添加到 Cloud Explorer

若要查看与 Azure 帐户关联的资源，必须先将该帐户添加到 **Cloud Explorer。**

1. 在 **Cloud Explorer"** 中，选择" **帐户管理"** 按钮。

   ![Cloud Explorer Azure 帐户设置图标](./media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. 选择"**管理帐户"。**

   ![Cloud Explorer 添加帐户链接](./media/vs-azure-tools-resources-managing-with-cloud-explorer/manage-accounts-link.png)

1. 登录要浏览其资源的 Azure 帐户。

1. 登录 Azure 帐户后，会显示与该帐户关联的订阅。 选中要浏览的帐户订阅的复选框，并选择“应用”。

   ![Cloud Explorer：选择要显示的 Azure 订阅](./media/vs-azure-tools-resources-managing-with-cloud-explorer/select-subscriptions.png)

1. 选择要浏览其资源的订阅后，这些订阅和资源会显示在 **Cloud Explorer。**

   ![Azure 帐户的 Cloud Explorer 资源列表](./media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-listed.png)

## <a name="remove-an-azure-account-from-cloud-explorer"></a>从 Cloud Explorer 删除 Azure 帐户

1. 在 **Cloud Explorer** 中，选择"**帐户管理"。**

   ![Azure 帐户设置](./media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. 在要删除的帐户旁，选择“管理帐户”。

   ![删除帐户](./media/vs-azure-tools-resources-managing-with-cloud-explorer/remove-account.png)

1. 选择“删除”以删除该帐户。

    ![Cloud Explorer“管理帐户”对话框](./media/vs-azure-tools-resources-managing-with-cloud-explorer/accountmanage.PNG)

## <a name="view-resource-types-or-resource-groups"></a>查看资源类型或资源组

若要查看 Azure 资源，可以选择“资源类型”或“资源组”视图。

1. 在 **Cloud Explorer** 中，选择资源视图下拉列表。

   ![Cloud Explorer 下拉列表可选择所需资源视图](./media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-view-dropdown.png)

1. 从上下文菜单中，选择所需视图：

   * “资源类型”视图 - [Azure 门户](https://portal.azure.com)中使用的常用视图，按类型来显示 Azure 资源，例如 Web 应用、存储帐户和虚拟机。
   * “资源组”视图 - 按关联的 Azure 资源组将 Azure 资源分类。 资源组是通常由特定应用程序使用的 Azure 资源组合。 若要了解有关 Azure 资源组的详细信息，请参阅 [Azure 资源管理器概述](/azure/azure-resource-manager/resource-group-overview)。

   下图比较了两个资源视图：

   ![Cloud Explorer 资源视图比较](./media/vs-azure-tools-resources-managing-with-cloud-explorer/resource-views-comparison.png)

## <a name="view-and-navigate-resources-in-cloud-explorer"></a>在 Cloud Explorer 中查看和导航资源

要在 Cloud Explorer 中导航到 Azure 资源并查看其信息，请展开项的类型或关联的资源组，并选择该资源。 当选择资源时，信息会显示在 Cloud Explorer 底部的两个选项卡（“操作”和“属性”）中。

* “操作”选项卡 - 列出了用户可以在 Cloud Explorer 针对所选资源执行的操作。 还可以通过右键单击资源来查看这些选项，以查看其上下文菜单。

* “属性”选项卡 - 显示资源的属性，例如其类型、区域设置和关联的资源组。

下图显示了关于在应用服务的每个选项卡上看到的内容的示例比较：

  ![云资源管理器的屏幕截图](./media/vs-azure-tools-resources-managing-with-cloud-explorer/actions-and-properties.png)

每个资源都有“在门户中打开”操作。 选择此操作时，云资源管理器会在 [Azure 门户](https://portal.azure.com)中显示所选的资源。 在导航到深度嵌套的资源时，**在门户中打开** 功能特别方便。

根据 Azure 资源，还可能会显示其他操作和属性值。 例如，除了“在门户中打开”以外，Web 应用和逻辑应用还提供了“在浏览器中打开”和“附加调试器”操作。 当选择存储帐户 Blob、队列或表时，会显示用于打开编辑器的操作。 Azure 应用具有“URL”和“状态”属性，而存储资源具有键和连接字符串属性。

## <a name="find-resources-in-cloud-explorer"></a>在 Cloud Explorer 中查找资源

若要在 Azure 帐户订阅中查找具有特定名称的资源，请在 azure 帐户订阅的"搜索"框中 **Cloud Explorer。**

  ![在云资源管理器中查找资源](./media/vs-azure-tools-resources-managing-with-cloud-explorer/search-for-resources.png)

在"搜索"框中 **输入字符** 时，资源树中只会显示与这些字符匹配的资源。

::: moniker-end

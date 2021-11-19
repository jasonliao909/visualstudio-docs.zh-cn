---
title: 使用连接服务添加 Azure 应用程序配置 | Microsoft Docs
description: 使用 Visual Studio 连接服务将 Azure 配置服务依赖关系添加到应用
author: ghogen
manager: ''
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: how-to
ms.date: 12/11/2020
ms.author: ghogen
monikerRange: '>=vs-2019'
ms.openlocfilehash: 250b89c983da039717982b31873a470172bde0f5
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602147"
---
# <a name="adding-azure-app-configuration-by-using-visual-studio-connected-services"></a>使用 Visual Studio 连接服务添加 Azure 应用程序配置

在本教程中，你将了解如何轻松添加开始使用 Azure 应用程序配置来管理 Visual Studio 中 Web 项目的配置和功能标志所需的所有内容。 通过在 Visual Studio 中使用连接服务功能，你可以让 Visual Studio 自动添加连接到 Azure 中的应用程序配置资源所需的所有代码、NuGet 包和配置设置。 若要使用此功能，必须使用 Visual Studio 2019 版本 16.9 或更高版本。

可以在 ASP.NET Core、.NET Core 控制台和 .NET Framework 项目中使用应用程序配置连接服务功能。

> [!NOTE]
> 本主题适用于 Visual Studio  Windows 版。 有关 Visual Studio for Mac，请参阅 [Visual Studio for Mac 中连接服务](/visualstudio/mac/connected-services)。

## <a name="prerequisites"></a>先决条件

- 安装有 Azure 工作负荷的 Visual Studio。
- 一个受支持类型的项目

## <a name="connect-to-azure-app-configuration-using-connected-services"></a>使用连接服务连接到 Azure 应用程序配置

1. 在 Visual Studio 中打开项目。

1. 在“解决方案资源管理器”中，右键单击“连接服务”节点，并在上下文菜单中选择“添加连接服务”。

    ![添加 Azure 连接服务](./media/vs-azure-tools-connected-services-storage/vs-2019/add-connected-service.png)

1. 在“连接服务”选项卡中，选择“服务依赖关系”的 + 图标。

    ![添加服务依赖关系](./media/vs-azure-tools-connected-services-storage/vs-2019/connected-services-tab.png)

1. 在“添加依赖关系”页中，选择“Azure 应用程序配置”。

    ![添加应用程序配置](./media/vs-azure-tools-connected-services-app-configuration/add-azure-app-configuration.png)

    如果你还没有登录，请登录到 Azure 帐户。 如果没有 Azure 帐户，可以注册[免费试用版](https://azure.microsoft.com/free/dotnet)。

1. 在“配置 Azure 应用程序配置”屏幕中，选择订阅和现有配置存储区。 然后，选择“下一步”。

    如果需要创建应用程序配置存储区，请转到下一步。 否则，请跳到步骤 6。

    ![将现有配置帐户添加到项目](./media/vs-azure-tools-connected-services-app-configuration/select-config-store.png)

1. 若要创建应用程序配置存储区，请执行以下操作：

   1. 选择“应用程序配置存储区”标题右侧的 + 图标。 

   1. 填写“Azure 应用程序配置: 新建”对话框，并选择“创建”。 请注意，“资源名称”字段必须是唯一的。 

       ![新建 Azure 应用程序配置存储区](./media/vs-azure-tools-connected-services-app-configuration/create-new-config-store.png)

   1. 当显示“Azure 应用程序配置”对话框时，新的配置存储区会显示在列表中。 选择这个新的存储区，然后选择“下一步”。

1. 输入连接字符串名称，然后选择是要将连接字符串存储在本地机密文件中还是存储在 [Azure Key Vault](/azure/key-vault) 中。

   ![指定连接字符串](./media/vs-azure-tools-connected-services-app-configuration/connection-string-app-config.png)

1. “更改摘要”屏幕显示了在完成该过程后将对项目进行的所有修改。 如果更改看起来正常，请选择“完成”。

   ![更改摘要](./media/vs-azure-tools-connected-services-app-configuration/summary-of-changes-app-config.png)

1. 完成“依赖关系配置过程”后，Azure 应用程序配置现在会显示在项目的“服务依赖关系”节点下。

## <a name="next-steps"></a>后续步骤

若要了解 Azure 应用程序配置，请参阅 [Azure 应用程序配置文档](/azure/azure-app-configuration/overview)。

## <a name="see-also"></a>另请参阅

- [在已连接应用程序配置的 ASP.NET Core 应用中使用动态配置的教程](/azure/azure-app-configuration/enable-dynamic-configuration-aspnet-core)
- [连接服务 (Visual Studio for Mac)](/visualstudio/mac/connected-services)
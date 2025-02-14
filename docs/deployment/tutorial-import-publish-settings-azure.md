---
title: 通过导入发布设置发布到 Azure
description: 创建并导入发布设置，以便将应用程序从 Visual Studio 部署到 Azure 应用服务
ms.date: 10/22/2021
ms.topic: tutorial
helpviewer_keywords:
- deployment, publish settings
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: 76df2e06ec5919a58aef3521c2a30d32a125bec5
ms.sourcegitcommit: 00af065ac27d41339b31d96a630705509b70b6fa
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2022
ms.locfileid: "140764097"
---
# <a name="get-publish-settings-from-azure-and-import-into-visual-studio"></a>从 Azure 获取发布设置，并将其导入 Visual Studio

可使用“发布”工具导入发布设置，然后部署应用。 本文使用 Azure 应用服务的发布设置。 这些步骤适用于 ASP.NET 和 ASP.NET Core Web 应用。 

> [!NOTE]
> 发布设置文件 (\*.publishsettings) 与在 Visual Studio 中创建的发布配置文件 (\*.pubxml) 不同 。 发布设置文件由 Azure 应用服务创建，然后可将其导入 Visual Studio。

## <a name="prerequisites"></a>先决条件

::: moniker range=">=vs-2019"

* 必须安装 Visual Studio 2019 且具有 ASP.NET 和 web 开发工作负载。

    如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads/)页免费安装。
::: moniker-end

::: moniker range="vs-2017"

* 须安装 Visual Studio 2017 且具有 ASP.NET 和 web 开发工作负载。

    如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads/)页免费安装。
::: moniker-end

* 创建 Azure 应用服务。 有关详细说明，请参阅[使用 Visual Studio 将 ASP.NET Core Web 应用部署到 Azure](/aspnet/core/tutorials/publish-to-azure-webapp-using-vs)。

## <a name="create-a-new-aspnet-project-in-visual-studio"></a>在 Visual Studio 中新建 ASP.NET 项目

1. 在运行 Visual Studio 的计算机上，创建新项目。

    选择正确的模板。 在此示例中，选择“ASP.NET Web 应用程序(.NET Framework)”或“ASP.NET Core Web 应用程序”（仅限 C#），然后选择“确定”  。

    如果没有看到指定的项目模板，请转到“新建项目”对话框左侧窗格中的“打开 Visual Studio 安装程序”链接 。 Visual Studio 安装程序启动。 安装“ASP.NET 和 Web 开发”工作负载。

    选择的项目模板（ASP.NET 或 ASP.NET Core）必须与安装在 Web 服务器上的 ASP.NET 版本相对应。

1. 选择“MVC”(.NET Framework) 或“Web 应用程序(模型-视图-控制器)”（适用于 .NET Core），并确保已选中“无身份验证”，然后选择“确定”   。

1. 键入名称（例如“MyWebApp”），然后选择“确定” 。

    Visual Studio 随即创建项目。

1. 选择“生成” > “生成解决方案”以生成项目 。

## <a name="create-the-publish-settings-file-in-azure-app-service"></a>在 Azure 应用服务中创建发布设置文件

1. 在 Azure 门户中打开 Azure 应用服务。

1. 转到“获取发布配置文件”并在本地保存配置文件。

    ![获取发布配置文件](../deployment/media/tutorial-azure-app-service-get-publish-profile.png)

    已在保存该文件的位置生成了带 .publishsettings 文件扩展名的文件。 以下代码显示了该文件的部分示例（格式更易读）。

    ```xml
    <publishData>
      <publishProfile
        profileName="DeployASPDotNetCore - Web Deploy"
        publishMethod="MSDeploy"
        publishUrl="deployaspdotnetcore.scm.azurewebsites.net:443"
        msdeploySite="DeployASPDotNetCore"
        userName="$DeployASPDotNetCore"
        userPWD="abcdefghijklmnopqrstuzwxyz"
        destinationAppUrl="http://deployaspdotnetcore2021.azurewebsites.net"
        SQLServerDBConnectionString=""
        mySQLDBConnectionString=""
        hostingProviderForumLink=""
        controlPanelLink="http://windows.azure.com"
        webSystem="WebSites">
        <databases />
      </publishProfile>
    </publishData>
    ```

    通常，前面的 *.publishsettings 文件包含两个可在 Visual Studio 中使用的发布配置文件：一个使用 Web 部署进行部署，另一个使用 FTP 进行部署。 前面的代码显示了 Web 部署配置文件。 导入配置文件时，稍后将导入两个配置文件。

## <a name="import-the-publish-settings-in-visual-studio-and-deploy"></a>在 Visual Studio 中导入发布设置并进行部署

[!INCLUDE [import publish settings](../deployment/includes/import-publish-settings-vs.md)]

## <a name="next-steps"></a>后续步骤

在本教程中，创建了发布设置文件，将其导入 Visual Studio，并将 ASP.NET 应用部署到 Azure 应用服务。 建议了解 Visual Studio 中发布选项的概述。

> [!div class="nextstepaction"]
> [初探部署](../deployment/deploying-applications-services-and-components.md)

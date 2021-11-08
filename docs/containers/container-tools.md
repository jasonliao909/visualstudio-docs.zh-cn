---
title: 带有 ASP.NET 的 Visual Studio 容器工具
author: ghogen
description: 了解如何使用 Visual Studio 容器工具和用于 Windows 的 Docker
ms.author: ghogen
ms.date: 10/27/2021
ms.technology: vs-container-tools
ms.topic: quickstart
ms.openlocfilehash: 99696d6c0a3b5603ce173a6e2c7a3171aac76a4b
ms.sourcegitcommit: aff49629012f4d5fa07c75ea0ca5bf53d28aa173
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2021
ms.locfileid: "131662595"
---
# <a name="quickstart-docker-in-visual-studio"></a>快速入门：Visual Studio 中的 Docker

::: moniker range="vs-2017"

[!include[Visual Studio Container Tools](includes/vs-2017/container-tools.md)]

::: moniker-end

::: moniker range="vs-2019"

[!include[Visual Studio Container Tools](includes/vs-2019/container-tools.md)]

::: moniker-end
::: moniker range=">=vs-2022"

使用 Visual Studio，可以轻松地生成、调试和运行容器化的 .NET、ASP.NET 和 ASP.NET Core 应用并将其发布到 Azure 容器注册表、Docker Hub、Azure 应用服务或你自己的容器注册表。 本文中，我们将发布一个 ASP.NET Core 应用到 Azure 容器注册表。

## <a name="prerequisites"></a>先决条件

* [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
* 安装了“Web 开发”、“Azure 工具”工作负载和/或“.NET Core 跨平台开发”工作负载的 [Visual Studio 2022 RC](https://visualstudio.microsoft.com/downloads)  
* 用于使用 .NET Core 进行开发的 [.NET Core 开发工具](https://dotnet.microsoft.com/download/dotnet-core/)
* 若要发布到 Azure 容器注册表，需要 Azure 订阅。 [注册免费试用版](https://azure.microsoft.com/free/dotnet/)。

## <a name="installation-and-setup"></a>安装和设置

要安装 Docker，请先查看[用于 Windows 的 Docker Desktop：安装须知](https://docs.docker.com/docker-for-windows/install/#what-to-know-before-you-install)了解相关信息。 然后安装[用于 Windows 的 Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows)。

## <a name="add-a-project-to-a-docker-container"></a>向 Docker 容器添加项目

1. 使用“ASP.NET Core Web 应用”模板创建新项目，或如果要使用 .NET Framework 而不是 .NET Core，请选择“ASP.NET Web 应用程序(.NET Framework)” 。
1. 在“创建 Web 应用”屏幕上，确保已选中“启用 Docker 支持”复选框 。

   ![“启用 Docker 支持”复选框的屏幕截图。](media/container-tools/vs-2022/web-app-additional-information-6-docker.png)

   屏幕截图显示 .NET 6.0；如果使用的是 .NET Framework，则略有不同。

1. 选择所需的容器类型（Windows 或 Linux），然后单击“创建”  。

## <a name="dockerfile-overview"></a>Dockerfile 概述

Dockerfile，用于创建最终 Docker 映像的方案，已在项目中创建  。 请查看 [Dockerfile 参考](https://docs.docker.com/engine/reference/builder/)，了解其中的命令：

```dockerfile
#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["WebApplication3/WebApplication3.csproj", "WebApplication3/"]
RUN dotnet restore "WebApplication3/WebApplication3.csproj"
COPY . .
WORKDIR "/src/WebApplication3"
RUN dotnet build "WebApplication3.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebApplication3.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebApplication3.dll"]
```

前面的 Dockerfile 基于 [Microsoft Container Registry (MCR)](https://azure.microsoft.com/blog/microsoft-syndicates-container-catalog/) .NET 6 映像，并且有说明介绍如何通过构建项目并将其添加到容器中来修改基本映像。 如果使用的是 .NET Framework，则基本映像将有所不同。

如果选中了新建项目对话框的“为 HTTPS 配置”复选框，则 Dockerfile 公开两个端口   。 一个端口用于 HTTP 流量；另一个端口用于 HTTPS。 如果未选中该复选框，则为 HTTP 流量公开单个端口 (80)。

## <a name="debug"></a>调试

在工具栏的调试下拉列表中选择“Docker”，然后开始调试应用。 你可能会看到提示信任证书的消息；选择信任证书以继续。

“输出”  窗口中的“容器工具”  选项显示正在进行的操作。 第一次时，可能需要一些时间来下载基本映像，但在后续运行时速度要快得多。

生成后，会显示浏览器，并显示应用的主页。 在浏览器的地址栏中，可以看到用于调试的 localhost URL 和端口号。

>[!NOTE]
> 如果需要更改用于调试的端口，可以在 launchSettings.json 文件中执行此操作  。 请参阅[容器启动设置](container-launch-settings.md)。

## <a name="containers-window"></a>容器窗口

可使用“容器”窗口来查看正在计算机上运行的容器，还可查看你可使用的映像。

在 IDE 中使用搜索框打开“容器”窗口（按 Ctrl+Q 可进行使用），键入 `container`然后从列表中选择“容器”窗口     。

可将“容器”窗口四处移动并沿着窗口放置参考线操作，将此窗口装载到便利的位置，例如在编辑器下方  。

在窗口中，找到你的容器并逐个浏览每个选项卡，以查看环境变量、端口映射、日志和文件系统。

![“容器”窗口的屏幕截图。](media/container-tools/vs-2022/container-tools-window.png)

有关详细信息，请参阅[使用“容器”窗口](view-and-diagnose-containers.md)。

## <a name="publish-docker-images"></a>发布 Docker 映像

完成应用程序的开发和调试循环后，可以创建应用程序的生产映像。

1. 将配置下拉列表更改为“发布”，然后生成应用。
1. 在解决方案资源管理器中右键单击项目，并选择“发布” 。
1. 在“发布”对话框中，选择“Docker 容器注册表”选项卡 。

   ![“‘发布’对话框 - 选择‘Docker 容器注册表’”的屏幕截图。](media/container-tools/vs-2022/docker-container-registry.png)

1. 选择“新建 Azure 容器注册表”。

   ![“‘发布’对话框 - 选择‘新建 Azure 容器注册表’”的屏幕截图。](media/container-tools/vs-2022/select-existing-or-create-new-azure-container-registry.png)

1. 在“创建新 Azure 容器注册表”中填写所需的值  。

    | 设置      | 建议的值  | 描述                                |
    | ------------ |  ------- | -------------------------------------------------- |
    | **DNS 前缀** | 全局唯一名称 | 用于唯一标识容器注册表的名称。 |
    | **订阅** | 选择订阅 | 要使用的 Azure 订阅。 |
    | **[资源组](/azure/azure-resource-manager/resource-group-overview)** | myResourceGroup |  要在其中创建容器注册表的资源组的名称。 选择“新建”  创建新的资源组。|
    | **[SKU](/azure/container-registry/container-registry-skus)** | 标准 | 容器注册表的服务层  |
    | **注册表位置** | 靠近你的位置 | 在你附近或将使用容器注册表的其他服务附近的[区域](https://azure.microsoft.com/regions/)中，选择位置。 |

    ![Visual Studio 的创建 Azure 容器注册表对话框的屏幕截图。](media/container-tools/vs-2022/vs-azure-container-registry-provisioning-dialog.png)

1. 单击 **“创建”** 。 现在，“发布”对话框显示已创建的注册表。

   ![显示已创建的 Azure 容器注册表的“发布”对话框的屏幕截图。](media/container-tools/vs-2022/created-azure-container-registry.png)

1. 选择“完成”，以完成将容器映像发布到 Azure 中新创建的注册表的过程。

   :::image type="content" source="media/container-tools/vs-2022/publish-succeeded.png" alt-text="显示成功发布的屏幕截图。" lightbox="media/container-tools/vs-2022/publish-succeeded.png" :::

## <a name="next-steps"></a>后续步骤

现在可以将容器从注册表中拖放到任何能够运行 Docker 映像的主机上，例如[Azure 容器实例](/azure/container-instances/container-instances-tutorial-deploy-app)。

::: moniker-end

## <a name="additional-resources"></a>其他资源

* [利用 Visual Studio 进行容器开发](./index.yml)
* [使用 Docker 排查 Visual Studio 开发方面的问题](troubleshooting-docker-errors.md)
* [Visual Studio 容器工具 GitHub 存储库](https://github.com/Microsoft/DockerTools)

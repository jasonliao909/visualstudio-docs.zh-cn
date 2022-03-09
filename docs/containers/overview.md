---
title: Windows 上的 Visual Studio Container Tools for Docker
description: 了解 Visual Studio 中可用于 Docker 的工具
author: ghogen
ms.author: ghogen
ms.topic: overview
ms.date: 10/27/2021
ms.technology: vs-container-tools
ms.openlocfilehash: 4b46bdaf53f9f7070944ee5b97ec32e6eac6b97d
ms.sourcegitcommit: f53c6f4e9f9de1e2aadf853b970c3654f0c193d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2022
ms.locfileid: "139691675"
---
# <a name="visual-studio-container-tools-for-docker"></a>Visual Studio Container Tools for Docker

Visual Studio 中用于使用 Docker 容器进行开发的工具易于使用，并大大简化了生成、调试和部署容器化应用程序的过程。 可以将容器用于单个项目，也可以将容器业务流程与 Docker Compose 或 Service Fabric 结合使用，以便使用容器中的多个服务。

::: moniker range="vs-2017"

## <a name="prerequisites"></a>先决条件

* [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
* 安装了“Web 开发”、“Azure 工具”工作负载和/或“.NET Core 跨平台开发”工作负载的 [Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)  
* 若要发布到 Azure 容器注册表，需要 Azure 订阅。 [注册免费试用版](https://azure.microsoft.com/offers/ms-azr-0044p/)。
Visual Studio 中的 andDocker 支持

Docker 支持可用于 ASP.NET 项目、ASP.NET Core 项目、Azure Functions、.net Core 控制台项目和 .NET Framework 控制台项目。

Visual Studio 中的 Docker 支持因版本而异，以响应客户需求。 可以向项目添加两个级别的 Docker 支持，并且受支持的选项因项目类型和 Visual Studio 版本而异。 借助某些受支持的项目类型，如果只想将容器用于单个项目，而不使用业务流程，则可以通过添加 Docker 支持来完成。  下一级别是容器业务流程支持，该支持可为所选的特定业务流程协调程序添加相应的支持文件。

借助 Visual Studio 2017，可以将 Docker Compose 和 Service Fabric 用作容器业务流程服务。

> [!NOTE]
> 如果使用的是 15.8 之前的 Visual Studio 2017 版本或使用的是 .NET Framework 项目模板（而不是 .NET Core），则在添加 Docker 支持时，会使用 Docker Compose 自动添加业务流程支持。 

::: moniker-end

::: moniker range="vs-2019"

## <a name="prerequisites"></a>先决条件

* [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
* 安装了“Web 开发”、“Azure 工具”工作负载和/或“.NET Core 跨平台开发”工作负载的 [Visual Studio 2019](https://visualstudio.microsoft.com/downloads)   
* 用于使用 .NET Core 进行开发的 [.NET Core 开发工具](https://dotnet.microsoft.com/download/dotnet-core/)。
* 若要发布到 Azure 容器注册表，需要 Azure 订阅。 [注册免费试用版](https://azure.microsoft.com/offers/ms-azr-0044p/)。

## <a name="docker-support-in-visual-studio"></a>Visual Studio 中的 Docker 支持

Docker 支持适用于 ASP.NET 项目、ASP.NET Core 项目，以及 .NET Core 和 .NET Framework 控制台项目。

Visual Studio 中的 Docker 支持因版本而异，以响应客户需求。 可以向项目添加两个级别的 Docker 支持，并且受支持的选项因项目类型和 Visual Studio 版本而异。 借助某些受支持的项目类型，如果只想将容器用于单个项目，而不使用业务流程，则可以通过添加 Docker 支持来完成。  下一级别是容器业务流程支持，该支持可为所选的特定业务流程协调程序添加相应的支持文件。

借助 Visual Studio 2019，可以将 Docker Compose、Kubernetes 和 Service Fabric 用作容器业务流程服务。

> [!NOTE]
> 创建 .NET Framework 或 .net Core 控制台项目时，没有 **添加 Docker 支持** 的选项。 创建 .NET Core 控制台应用程序项目后，可以使用 " **添加 Docker 支持** " 选项。 创建项目后，.net Framework 控制台应用程序项目不支持 " **添加 Docker 支持** " 选项。 创建后 .NET Framework 或 .net Core 控制台项目都支持使用 Service Fabric 或 Docker Compose **添加容器 Orchestrator 支持** 选项。

在 Visual Studio 2019 版本 16.4 及更高版本中，提供了“容器”窗口，你可用它来查看正在运行的容器，浏览可用的映像，查看环境变量、日志和端口映射，检查文件系统，附加调试器，或者在容器环境中打开终端窗口。 请参阅[使用“容器”窗口](view-and-diagnose-containers.md)。

::: moniker-end

::: moniker range=">=vs-2022"

## <a name="prerequisites"></a>先决条件

* [Docker Desktop](https://www.docker.com/get-docker)
* 安装了“Web 开发”、“Azure 工具”工作负载和/或“.NET 桌面开发”工作负载的 [Visual Studio 2022](https://visualstudio.microsoft.com/downloads)  
* 若要发布到 Azure 容器注册表，需要 Azure 订阅。 [注册免费试用版](https://azure.microsoft.com/offers/ms-azr-0044p/)。

## <a name="docker-support-in-visual-studio"></a>Visual Studio 中的 Docker 支持

Docker 支持适用于 ASP.NET 项目、ASP.NET Core 项目，以及 .NET Core 和 .NET Framework 控制台项目。

Visual Studio 中的 Docker 支持因版本而异，以响应客户需求。 可以向项目添加两个级别的 Docker 支持，并且受支持的选项因项目类型和 Visual Studio 版本而异。 借助某些受支持的项目类型，如果只想将容器用于单个项目，而不使用业务流程，则可以通过添加 Docker 支持来完成。  下一级别是容器业务流程支持，该支持可为所选的特定业务流程协调程序添加相应的支持文件。

借助 Visual Studio 2022，可将 Docker Compose 或 Service Fabric 用作容器业务流程服务。

> [!NOTE]
> 如果你使用完整的 .NET Framework 控制台项目模板，则在创建项目后，支持的选项是“添加容器业务流程协调程序支持”，它包括使用 Service Fabric 或 Docker Compose 的选项。 对于没有业务流程的单个项目，无法在项目创建时添加支持，也无法添加 Docker 支持。

在 Visual Studio 2022 中，提供了“容器”窗口，你可用它来查看正在运行的容器，浏览可用的映像，查看环境变量、日志和端口映射，检查文件系统，附加调试器，或者在容器环境中打开终端窗口。 请参阅[使用“容器”窗口](view-and-diagnose-containers.md)。

::: moniker-end

### <a name="adding-docker-support"></a>添加 Docker 支持

可以通过在创建新项目时选择“启用 Docker 支持”来在项目创建期间启用 Docker 支持，如以下屏幕截图所示：

::: moniker range="vs-2017"
![屏幕截图显示如何在 Visual Studio 中为新的 ASP.NET Core Web 应用启用 Docker 支持。](./media/overview/enable-docker-support-visual-studio.png)
::: moniker-end
::: moniker range="vs-2019"
![屏幕截图显示如何在 Visual Studio 中为新的 ASP.NET Core Web 应用启用 Docker 支持。](./media/overview/vs-2019/enable-docker-support-visual-studio.png)
::: moniker-end
::: moniker range=">=vs-2022"
![屏幕截图显示如何在 Visual Studio 中为新的 ASP.NET Core Web 应用启用 Docker 支持。](./media/overview/vs-2022/enable-docker-support-visual-studio.png)
::: moniker-end

> [!NOTE]
> 对于 .NET Framework 项目（而不是 .NET Core），只有 Windows 容器可用。

可以通过在“解决方案资源管理器”中选择“添加” > “Docker 支持”来向现有项目添加 Docker 支持。 Add > Docker Support 和 Add > Container Orchestrator Support 命令位于“解决方案资源管理器”中 ASP.NET Core 项目的项目节点的右键单击菜单（或上下文菜单）上，如以下屏幕截图所示：

:::moniker range="<=vs-2019"
![屏幕截图显示如何在 Visual Studio 中添加“Docker 支持”菜单选项。](./media/overview/add-docker-support-menu.png)
:::moniker-end
:::moniker range=">=vs-2022"
![屏幕截图显示如何在 Visual Studio 中添加“Docker 支持”菜单选项。](./media/overview/vs-2022/add-docker-support.png)
:::moniker-end

当添加或启用 Docker 支持时，Visual Studio 会向项目添加以下各项：

* Dockerfile 文件
* .dockerignore 文件
* 对 Microsoft.VisualStudio.Azure.Containers.Tools.Targets 的 NuGet 包引用

添加的 Dockerfile 将类似于以下代码。 在此示例中，项目命名为 `WebApplication-Docker`，并且你选择了 Linux 容器：

:::moniker range="<=vs-2019"

```Dockerfile
#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["WebApplication-Docker/WebApplication-Docker.csproj", "WebApplication-Docker/"]
RUN dotnet restore "WebApplication-Docker/WebApplication-Docker.csproj"
COPY . .
WORKDIR "/src/WebApplication-Docker"
RUN dotnet build "WebApplication-Docker.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebApplication-Docker.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebApplication-Docker.dll"]
```

:::moniker-end
:::moniker range=">=vs-2022"

```dockerfile
#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["WebApplication-Docker/WebApplication-Docker.csproj", "WebApplication-Docker/"]
RUN dotnet restore "WebApplication-Docker/WebApplication-Docker.csproj"
COPY . .
WORKDIR "/src/WebApplication-Docker"
RUN dotnet build "WebApplication-Docker.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebApplication-Docker.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebApplication-Docker.dll"]
```

:::moniker-end
::: moniker range="vs-2017"
> [!NOTE]
> 在项目创建期间启用 Docker 支持时， (.NET Framework，而不是 .net Core 项目) ，如以下屏幕截图中所示，还会添加容器 orchestrator 支持 ASP.NET。

![屏幕截图显示为 ASP.NET 项目启用 Docker Compose 支持。](media/overview/enable-docker-compose-support.png)
::: moniker-end

## <a name="use-the-containers-window"></a>使用“容器”窗口

使用“容器”窗口可以查看计算机上的容器和映像及其运行情况。 可以查看文件系统、装载的卷、环境变量、使用的端口，以及检查日志文件。

通过使用快速启动 (Ctrl+Q) 并键入 `containers` 来打开“容器”窗口  。 可以使用停靠控件将该窗口固定在某个位置。 由于窗口的宽度，将其停靠在屏幕底部时是最好用的。

选择一个容器，然后使用选项卡查看可用的信息。 若要查看，请运行启用了 Docker 的应用，打开“文件”选项卡，然后展开“应用”文件夹以查看容器上已部署的应用 。

:::moniker range="<=vs-2019"
![“容器”窗口的屏幕截图。](media/overview/vs-2019/container-tools-window-2.png)
:::moniker-end
:::moniker range=">=vs-2022"
![“容器”窗口的屏幕截图。](media/overview/vs-2022/containers-files.png)
:::moniker-end

有关详细信息，请参阅[使用“容器”窗口](view-and-diagnose-containers.md)。

## <a name="docker-compose-support"></a>Docker Compose 支持

如果要使用 Docker Compose 撰写多容器解决方案，请将容器 orchestrator 支持添加到项目。 这样就可以同时运行和调试一组容器（整个解决方案或项目组）（如果已在同一个 docker-compose.yml 文件中定义这些容器）。

若要使用 Docker Compose 添加容器 orchestrator 支持，请右键单击 **解决方案资源管理器** 中的项目节点，然后选择 " **添加 > 容器 orchestrator 支持**"。 然后，选择“Docker Compose”以管理容器。

向项目添加容器 orchestrator 支持后，会看到添加到项目的 *Dockerfile* ， (如果没有) 并在 **解决方案资源管理器** 中向解决方案添加了 **docker 组合** 文件夹，如下所示：

:::moniker range="<=vs-2019"
![Visual Studio 解决方案资源管理器中的 Docker 文件的屏幕截图。](media/overview/docker-support-solution-explorer.png)
:::moniker-end
:::moniker range=">=vs-2022"
![Visual Studio 解决方案资源管理器中的 Docker 文件的屏幕截图。](media/overview/vs-2022/docker-compose-solution-explorer.png)
:::moniker-end

如果 docker-compose.yml 已存在，Visual Studio 只需向其添加配置代码所需的行。

对要使用 Docker Compose 控制的其他项目重复该过程。

如果使用大量服务，可以通过选择要在调试会话中启动的服务子集来节省时间和计算资源。 请参阅[启动 Compose 服务的子集](launch-profiles.md)。

## <a name="service-fabric-support"></a>Service Fabric 支持

借助 Visual Studio 中的 Service Fabric 工具，可以开发和调试 Azure Service Fabric、进行本地运行和调试并部署到 Azure。

::: moniker range="vs-2017"
安装了 Azure 开发工作负载的 Visual Studio 2017 版本 15.9 及更高版本支持使用 Windows 容器和 Service Fabric 业务流程来开发容器化微服务。
::: moniker-end
::: moniker range=">=vs-2019"
Visual Studio 2019 及更高版本支持使用 Windows 容器和 Service Fabric 业务流程来开发容器化微服务。
::: moniker-end

有关详细教程，请参阅[教程：将 Windows 容器中的 .NET 应用程序部署到 Azure Service Fabric](/azure/service-fabric/service-fabric-host-app-in-a-container)。

有关 Azure Service Fabric 的详细信息，请参阅 [Service Fabric](/azure/service-fabric)。

## <a name="continuous-delivery-and-continuous-integration-cicd"></a>持续交付和持续集成 (CI/CD)

Visual Studio 与 Azure Pipelines 轻松集成，以便自动完成服务代码和配置更改的持续集成和交付。 若要开始使用，请参阅[创建第一个管道](/azure/devops/pipelines/create-first-pipeline?view=azure-devops&tabs=tfs-2018-2&preserve-view=true)。

有关 Service Fabric 的信息，请参阅[教程：使用 Azure DevOps Projects 将 ASP.NET Core 应用部署到 Azure Service Fabric](/azure/devops-project/azure-devops-project-service-fabric)。

## <a name="next-steps"></a>后续步骤

有关服务实现以及将 Visual Studio 工具用于容器的更多详细信息，请阅读以下文章：

在本地 Docker 容器中调试应用  

[使用 Visual Studio 将 ASP.NET 容器部署到容器注册表](hosting-web-apps-in-docker.md)

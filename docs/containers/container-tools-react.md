---
title: 带有 ASP.NET Core 和 React.js 的 Visual Studio 容器工具
titleSuffix: ''
ms.custom: SEO-VS-2020
author: ghogen
description: 了解如何使用 Visual Studio 容器工具和 Docker 创建容器化 React SPA 应用
ms.author: ghogen
ms.date: 10/25/2021
ms.technology: vs-container-tools
ms.topic: quickstart
ms.openlocfilehash: 884024196a4b6d43ebc4d2c0a1d6e3c70259d649
ms.sourcegitcommit: 67dc39e93c86ba50eb5ca877b0471fb8ab8475ac
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/08/2021
ms.locfileid: "132001307"
---
# <a name="quickstart-use-docker-with-a-react-single-page-app-in-visual-studio"></a>快速入门：将 Docker 与 Visual Studio 中的 React 单页面应用结合使用

借助 Visual Studio，可以轻松地生成、调试和运行容器化的 ASP.NET Core 应用（包括使用客户端 JavaScript 的应用，如 React.js 单页应用）并将其发布到 Azure 容器注册表、Docker Hub、Azure 应用服务或你自己的容器注册表。 在本文中，我们将发布到 Azure 容器注册表。

## <a name="prerequisites"></a>先决条件

::: moniker range="vs-2017"
* [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
* 安装了“Web 开发”、“Azure 工具”工作负载和/或“.NET Core 跨平台开发”工作负载的 [Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)  
* 若要发布到 Azure 容器注册表，需要 Azure 订阅。 [注册免费试用版](https://azure.microsoft.com/offers/ms-azr-0044p/)。
* [Node.js](https://nodejs.org/en/download/)
* 对于 Windows 容器、Windows 10 版本 1809 或更高版本，使用本文中引用的 Docker 映像。
::: moniker-end
::: moniker range="vs-2019"
* [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
* 安装了“Web 开发”、“Azure 工具”工作负载和/或“.NET Core 跨平台开发”工作负载的 [Visual Studio 2019](https://visualstudio.microsoft.com/downloads)  
* 用于使用 .NET Core 3.1 进行开发的 [.NET Core 3.1 开发工具](https://dotnet.microsoft.com/download/dotnet-core/3.1)。
* 若要发布到 Azure 容器注册表，需要 Azure 订阅。 [注册免费试用版](https://azure.microsoft.com/offers/ms-azr-0044p/)。
* [Node.js](https://nodejs.org/en/download/)
* 对于 Windows 容器、Windows 10 版本 1809 或更高版本，使用本文中引用的 Docker 映像。
::: moniker-end
::: moniker range=">=vs-2022"
* [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
* 安装了“Web 开发”、“Azure 工具”工作负载和/或“.NET Core 跨平台开发”工作负载的 [Visual Studio 2022](https://visualstudio.microsoft.com/downloads)
* 若要发布到 Azure 容器注册表，需要 Azure 订阅。 [注册免费试用版](https://azure.microsoft.com/offers/ms-azr-0044p/)。
* [Node.js](https://nodejs.org/en/download/)
* 对于 Windows 容器、Windows 10 版本 1809 或更高版本，使用本文中引用的 Docker 映像。

::: moniker-end

## <a name="installation-and-setup"></a>安装和设置

要安装 Docker，请先查看[用于 Windows 的 Docker Desktop：安装须知](https://docs.docker.com/docker-for-windows/install/#what-to-know-before-you-install)了解相关信息。 然后安装[用于 Windows 的 Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows)。

## <a name="create-a-project-and-add-docker-support"></a>创建项目并添加 Docker 支持

::: moniker range="vs-2017"

1. 使用“ASP.NET Core Web 应用程序”模板创建新项目。

1. 选择“React.js”。 你无法选择“启用 Docker 支持”，但不要担心，你可以在创建项目后添加该支持。

   ![新 React.js 项目的屏幕截图。](media/container-tools-react/vs-2017/new-react-project.png)

1. 右键单击项目节点，然后选择“添加”>“Docker 支持”，将 Dockerfile 添加到你的项目中 。

   ![添加 Docker 支持菜单项的屏幕截图。](media/container-tools-react/vs-2017/add-docker-support.png)

1. 选择容器类型，然后单击“确定”。
::: moniker-end

::: moniker range="vs-2019"

1. 使用“带 React.js 的 ASP.NET Core”模板创建新项目。

   ![创建新 React.js 项目的屏幕截图。](media/container-tools-react/vs-2019/create-reactjs-project.png)

1. 在“其他信息”屏幕上，你无法选择“启用 Docker 支持”，但不要担心，可以稍后添加该支持。

   ![“创建新 React.js 项目 - 其他信息”屏幕的屏幕截图。](media/container-tools-react/vs-2019/new-react-project-additional-information.png)

1. 右键单击项目节点，然后选择“添加”>“Docker 支持”，将 Dockerfile 添加到你的项目中 。

   ![添加 Docker 支持菜单项的屏幕截图。](media/container-tools-react/vs-2017/add-docker-support.png)

1. 选择容器类型。
::: moniker-end
::: moniker range=">=vs-2022"

1. 使用“带 React.js 的 ASP.NET Core”模板创建新项目。

   ![创建新 React.js 项目的屏幕截图。](media/container-tools-react/vs-2022/create-reactjs-project.png)

1. 在“其他信息”屏幕上，你无法选择“启用 Docker 支持”，但不要担心，可以稍后添加该支持。

   ![“创建新 React.js 项目 - 其他信息”屏幕的屏幕截图。](media/container-tools-react/vs-2022/react-project-additional-information.png)

1. 右键单击项目节点，然后选择“添加”>“Docker 支持”，将 Dockerfile 添加到你的项目中 。

   ![添加 Docker 支持菜单项的屏幕截图。](media/container-tools-react/vs-2022/add-docker-support.png)

1. 选择容器类型。
:::moniker-end

根据你使用的是 Linux 容器还是 Windows 容器，下一步会有所不同。

## <a name="modify-the-dockerfile-linux-containers"></a>修改 Dockerfile（Linux 容器）

Dockerfile，用于创建最终 Docker 映像的方案，已在项目中创建。 请参阅 [Dockerfile 引用](https://docs.docker.com/engine/reference/builder/)，了解其中的命令。

在项目中打开“Dockerfile”，并添加以下代码行以将 curl、Node.js 14.x 和某些必需的 Node 库安装到容器中。 请务必在第一部分中添加这些行，以将 Node 包管理器 npm.exe 的安装添加到基础映像以及 `build` 部分中。

```Dockerfile
RUN apt-get update
RUN apt-get install -y curl
RUN apt-get install -y libpng-dev libjpeg-dev curl libxi6 build-essential libgl1-mesa-glx
RUN curl -sL https://deb.nodesource.com/setup_14.x | bash -
RUN apt-get install -y nodejs
```

“Dockerfile”现在看起来如下所示：

:::moniker range="<=vs-2019"

```Dockerfile
#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443
RUN apt-get update
RUN apt-get install -y curl
RUN apt-get install -y libpng-dev libjpeg-dev curl libxi6 build-essential libgl1-mesa-glx
RUN curl -sL https://deb.nodesource.com/setup_14.x | bash -
RUN apt-get install -y nodejs

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
RUN apt-get update
RUN apt-get install -y curl
RUN apt-get install -y libpng-dev libjpeg-dev curl libxi6 build-essential libgl1-mesa-glx
RUN curl -sL https://deb.nodesource.com/setup_14.x | bash -
RUN apt-get install -y nodejs
WORKDIR /src
COPY ["ReactSPA/ReactSPA.csproj", "ReactSPA/"]
RUN dotnet restore "ReactSPA/ReactSPA.csproj"
COPY . .
WORKDIR "/src/ReactSPA"
RUN dotnet build "ReactSPA.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ReactSPA.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ReactSPA.dll"]
```

:::moniker-end
:::moniker range=">=vs-2022"

```Dockerfile
#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443
RUN apt-get update
RUN apt-get install -y curl
RUN apt-get install -y libpng-dev libjpeg-dev curl libxi6 build-essential libgl1-mesa-glx
RUN curl -sL https://deb.nodesource.com/setup_14.x | bash -
RUN apt-get install -y nodejs

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
RUN apt-get update
RUN apt-get install -y curl
RUN apt-get install -y libpng-dev libjpeg-dev curl libxi6 build-essential libgl1-mesa-glx
RUN curl -sL https://deb.nodesource.com/setup_14.x | bash -
RUN apt-get install -y nodejs
WORKDIR /src
COPY ["ReactSPA/ReactSPA.csproj", "ReactSPA/"]
RUN dotnet restore "ReactSPA/ReactSPA.csproj"
COPY . .
WORKDIR "/src/ReactSPA"
RUN dotnet build "ReactSPA.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ReactSPA.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ReactSPA.dll"]
```

:::moniker-end

前面的 Dockerfile 基于 [mcr.microsoft.com/dotnet/core/aspnet](https://hub.docker.com/_/microsoft-dotnet-core-aspnet/) 映像，并包括通过构建项目并将其添加到容器中修改基本映像的说明。

如果选中了新建项目对话框的“为 HTTPS 配置”复选框，则 Dockerfile 公开两个端口。 一个端口用于 HTTP 流量；另一个端口用于 HTTPS。 如果未选中该复选框，则为 HTTP 流量公开单个端口 (80)。

## <a name="modify-the-dockerfile-windows-containers"></a>修改 Dockerfile（Windows 容器）

通过双击项目节点来打开项目文件，然后通过将以下属性添加为 `<PropertyGroup>` 元素的子元素来更新项目文件 (*.csproj)：

   ```xml
    <DockerfileFastModeStage>base</DockerfileFastModeStage>
   ```

通过添加以下行来更新 Dockerfile。 这样会将节点和 npm 复制到容器。

   1. 将 ``# escape=` `` 添加到 Dockerfile 的第一行
   1. 在 `FROM … base` 之前添加以下行

      ```Dockerfile
      FROM mcr.microsoft.com/powershell AS downloadnodejs
      ENV NODE_VERSION=14.16.0
      SHELL ["pwsh", "-Command", "$ErrorActionPreference = 'Stop';$ProgressPreference='silentlyContinue';"]
      RUN Invoke-WebRequest -OutFile nodejs.zip -UseBasicParsing "https://nodejs.org/dist/v$($env:NODE_VERSION)/node-v$($env:NODE_VERSION)-win-x64.zip"; `
          Expand-Archive nodejs.zip -DestinationPath C:\; `
          Rename-Item "C:\node-v$($env:NODE_VERSION)-win-x64" c:\nodejs
      ```

   1. 在 `FROM … build` 之前和之后添加以下行

      ```Dockerfile
      COPY --from=downloadnodejs C:\nodejs\ C:\Windows\system32\
      ```

   1. 完整的 Dockerfile 现在看起来如下所示：

      :::moniker range="<=vs-2019"

      ```Dockerfile
      # escape=`
      #Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
      #For more information, please see https://aka.ms/containercompat
      FROM mcr.microsoft.com/powershell AS downloadnodejs
      ENV NODE_VERSION=14.16.0
      SHELL ["pwsh", "-Command", "$ErrorActionPreference = 'Stop';$ProgressPreference='silentlyContinue';"]
      RUN Invoke-WebRequest -OutFile nodejs.zip -UseBasicParsing "https://nodejs.org/dist/v$($env:NODE_VERSION)/node-v$($env:NODE_VERSION)-win-x64.zip"; \
          Expand-Archive nodejs.zip -DestinationPath C:\; \
          Rename-Item "C:\node-v$($env:NODE_VERSION)-win-x64" c:\nodejs

      FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS base
      WORKDIR /app
      EXPOSE 80
      EXPOSE 443
      COPY --from=downloadnodejs C:\nodejs\ C:\Windows\system32\

      FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
      COPY --from=downloadnodejs C:\nodejs\ C:\Windows\system32\
      WORKDIR /src
      COPY ["WebApplicationReact1/WebApplicationReact1.csproj", "WebApplicationReact1/"]
      RUN dotnet restore "WebApplicationReact1/WebApplicationReact1.csproj"
      COPY . .
      WORKDIR "/src/WebApplicationReact1"
      RUN dotnet build "WebApplicationReact1.csproj" -c Release -o /app/build

      FROM build AS publish
      RUN dotnet publish "WebApplicationReact1.csproj" -c Release -o /app/publish

      FROM base AS final
      WORKDIR /app
      COPY --from=publish /app/publish .
      ENTRYPOINT ["dotnet", "WebApplicationReact1.dll"]
      ```

      :::moniker-end
      :::moniker range=">=vs-2022"
      ```Dockerfile
      # escape=`
      #Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
      #For more information, please see https://aka.ms/containercompat
      FROM mcr.microsoft.com/powershell AS downloadnodejs
      ENV NODE_VERSION=14.16.0
      SHELL ["pwsh", "-Command", "$ErrorActionPreference = 'Stop';$ProgressPreference='silentlyContinue';"]
      RUN Invoke-WebRequest -OutFile nodejs.zip -UseBasicParsing "https://nodejs.org/dist/v$($env:NODE_VERSION)/node-v$($env:NODE_VERSION)-win-x64.zip"; \
          Expand-Archive nodejs.zip -DestinationPath C:\; \
          Rename-Item "C:\node-v$($env:NODE_VERSION)-win-x64" c:\nodejs

      FROM mcr.microsoft.com/dotnet/core/aspnet:6.0 AS base
      WORKDIR /app
      EXPOSE 80
      EXPOSE 443
      COPY --from=downloadnodejs C:\nodejs\ C:\Windows\system32\

      FROM mcr.microsoft.com/dotnet/core/sdk:6.0 AS build
      COPY --from=downloadnodejs C:\nodejs\ C:\Windows\system32\
      WORKDIR /src
      COPY ["WebApplicationReact1/WebApplicationReact1.csproj", "WebApplicationReact1/"]
      RUN dotnet restore "WebApplicationReact1/WebApplicationReact1.csproj"
      COPY . .
      WORKDIR "/src/WebApplicationReact1"
      RUN dotnet build "WebApplicationReact1.csproj" -c Release -o /app/build

      FROM build AS publish
      RUN dotnet publish "WebApplicationReact1.csproj" -c Release -o /app/publish

      FROM base AS final
      WORKDIR /app
      COPY --from=publish /app/publish .
      ENTRYPOINT ["dotnet", "WebApplicationReact1.dll"]
      ```

      ::: moniker-end

   1. 通过删除 `**/bin`来更新 .dockerignore 文件。

## <a name="debug"></a>调试

:::moniker range=">=vs-2022"
设置用于调试的默认 URL。 可以使用“开始”按钮旁的下拉菜单，并选择“调试属性”。 在出现的“启动配置文件”对话框中，选择“Docker”并编辑 URL，以将 `/weatherforecast` 追加到已有内容。
:::moniker-end

在工具栏的调试下拉列表中选择“Docker”，然后开始调试应用。 你可能会看到提示信任证书的消息；选择信任证书以继续。  第一次生成时，docker 会下载基础映像，因此可能需要更长的时间。

“输出”窗口中的“容器工具”选项显示正在进行的操作。 你将看到与 npm.exe 关联的安装步骤。

浏览器将显示应用的主页。

   ::: moniker range="vs-2017"
   ![正在运行的应用的屏幕截图。](media/container-tools-react/vs-2017/running-app.png)
   ::: moniker-end
   ::: moniker range="vs-2019"
   ![正在运行的应用的屏幕截图。](media/container-tools-react/vs-2019/running-app.png)
   ::: moniker-end
   ::: moniker range=">=vs-2022"
   ![正在运行的应用的屏幕截图。](media/container-tools-react/vs-2022/running-app.png)
   ::: moniker-end

:::moniker range="<=vs-2019"
尝试导航到“计数器”页面，并单击“递增”按钮测试计数器的客户端代码。

依次选择“工具”菜单 >“NuGet 包管理器”>“包管理器控制台”，打开包管理器控制台 (PMC)  。

最终得到的应用的 Docker 映像标记为“开发”。 该映像基于 dotnet/core/aspnet 基础映像的 3.1 标记 。 在“包管理器控制台”(PMC) 窗口中运行 `docker images` 命令。 显示了计算机上的映像：

```console
REPOSITORY                             TAG                 IMAGE ID            CREATED             SIZE
webapplicationreact1                   dev                 09be6ec2405d        2 hours ago         352MB
mcr.microsoft.com/dotnet/core/aspnet   3.1                 e3559b2d50bb        10 days ago         207MB
```

> [!NOTE]
> “开发”映像不包含应用程序二进制文件和其他内容，因为“调试”配置使用卷装载提供迭代编辑和调试体验 。 若要创建包含所有内容的生产映像，请使用“版本”配置。

在 PMC 中运行 `docker ps` 命令。 请注意，应用使用容器运行：

```console
CONTAINER ID        IMAGE                      COMMAND               CREATED             STATUS              PORTS                                           NAMES
56d1b1008c89        webapplicationreact1:dev   "tail -f /dev/null"   2 hours ago         Up 2 hours          0.0.0.0:32771->80/tcp, 0.0.0.0:32770->443/tcp   WebApplication-ReactSPA
```

:::moniker-end

:::moniker range=">=vs-2022"

打开“容器”工具窗口。 可以在“查看” > “其他 Windows” > “容器”下找到它，或按 Ctrl+Q 并开始在搜索框中键入 `containers`，然后从结果中选择“容器”窗口。 窗口打开时，将其停靠在编辑器窗格的底部。

“容器”窗口显示正在运行的容器，并可查看相关信息。 可以查看环境变量、标签、端口、卷、文件系统和日志。 使用工具栏按钮，可以在容器内创建一个终端（shell 提示）、附加调试器或删除未使用的容器。 请参阅[使用“容器”窗口](view-and-diagnose-containers.md)。

![“容器”窗口的屏幕截图。](media/container-tools-react/vs-2022/container-tools-window.png)

单击“文件”选项卡，然后展开 `app` 文件夹以查看已发布的应用程序文件。

还可以查看图像并检查相关信息。 选择“图像”选项卡，找到项目对应的选项卡，然后选择“详细信息”选项卡以查看包含图像相关信息的 json 文件。

![显示图像和详细信息的“容器”窗口的屏幕截图。](media/container-tools-react/vs-2022/container-tools-window-images-details.png)

> [!NOTE]
> “开发”映像不包含应用程序二进制文件和其他内容，因为“调试”配置使用卷装载提供迭代编辑和调试体验 。 若要创建包含所有内容的生产映像，请使用“版本”配置。

:::moniker-end

## <a name="publish-docker-images"></a>发布 Docker 映像

完成应用程序的开发和调试循环后，可以创建应用程序的生产映像。

:::moniker range="vs-2017"

1. 将配置下拉列表更改为“发布”，然后生成应用。
1. 在解决方案资源管理器中右键单击项目，并选择“发布” 。
1. 在“发布目标”对话框中，选择“容器注册表”。
1. 选择“创建新的 Azure 容器注册表”并单击“发布” 。
1. 在“创建新 Azure 容器注册表”中填写所需的值  。

    | 设置      | 建议的值  | 描述                                |
    | ------------ |  ------- | -------------------------------------------------- |
    | **DNS 前缀** | 全局唯一名称 | 用于唯一标识容器注册表的名称。 |
    | **订阅** | 选择订阅 | 要使用的 Azure 订阅。 |
    | **[资源组](/azure/azure-resource-manager/resource-group-overview)** | myResourceGroup |  要在其中创建容器注册表的资源组的名称。 选择“新建”  创建新的资源组。|
    | **[SKU](/azure/container-registry/container-registry-skus)** | 标准 | 容器注册表的服务层  |
    | **注册表位置** | 靠近你的位置 | 在你附近或将使用容器注册表的其他服务附近的[区域](https://azure.microsoft.com/regions/)中，选择位置。 |

    ![Visual Studio 的创建 Azure 容器注册表对话框的屏幕截图。](media/hosting-web-apps-in-docker/vs-azure-container-registry-provisioning-dialog.png)

1. 选择“创建”。

   ![显示成功发布的屏幕截图。](media/container-tools/publish-succeeded.png)
:::moniker-end

:::moniker range="vs-2019"

1. 将配置下拉列表更改为“发布”，然后生成应用。
1. 在解决方案资源管理器中右键单击项目，并选择“发布” 。
1. 在“发布目标”对话框中，选择“Docker 容器注册表”。

   ![选择“Docker 容器注册表”。](media/container-tools-react/vs-2019/publish-dialog1.png)

1. 接下来，选择“Azure 容器注册表”。

   ![选择“Azure 容器注册表”。](media/container-tools-react/vs-2019/publish-dialog-azure-container-registry.png)

1. 选择“新建 Azure 容器注册表”。
1. 在“新建 Azure 容器注册表”屏幕中填写所需的值。

    | 设置      | 建议的值  | 描述                                |
    | ------------ |  ------- | -------------------------------------------------- |
    | **DNS 前缀** | 全局唯一名称 | 用于唯一标识容器注册表的名称。 |
    | **订阅** | 选择订阅 | 要使用的 Azure 订阅。 |
    | **[资源组](/azure/azure-resource-manager/resource-group-overview)** | myResourceGroup |  要在其中创建容器注册表的资源组的名称。 选择“新建”  创建新的资源组。|
    | **[SKU](/azure/container-registry/container-registry-skus)** | 标准 | 容器注册表的服务层  |
    | **注册表位置** | 靠近你的位置 | 在你附近或将使用容器注册表的其他服务附近的[区域](https://azure.microsoft.com/regions/)中，选择位置。 |

    ![Visual Studio 的创建 Azure 容器注册表对话框的屏幕截图。](media/container-tools-react/vs-2019/azure-container-registry-details.png)

1. 选择“创建”，然后选择“完成” 。

   ![显示选择或创建新 Azure 容器注册表的屏幕截图。](media/container-tools-react/vs-2019/publish-dialog2.png)

   发布过程结束时，你可查看发布设置并在需要时对其进行编辑，也可使用“发布”按钮再次发布该图像。

   ![显示成功发布的屏幕截图。](media/container-tools-react/vs-2019/publish-finished.png)

   若要使用“发布”对话框重新开始，请使用此页上的“删除”链接删除发布配置文件，然后再次选择“发布”  。
:::moniker-end

:::moniker range=">=vs-2022"

1. 将配置下拉列表更改为“发布”，然后生成应用。
1. 在解决方案资源管理器中右键单击项目，并选择“发布” 。
1. 在“发布目标”对话框中，选择“Docker 容器注册表”。

   ![显示选择 Docker 容器注册表的屏幕截图。](media/container-tools-react/vs-2022/publish-dialog-1.png)

1. 接下来，选择“Azure 容器注册表”。

   ![显示选择 Azure 容器注册表的屏幕截图。](media/container-tools-react/vs-2022/publish-dialog-azure-container-registry.png)

1. 选择“新建 Azure 容器注册表”。
1. 在“新建 Azure 容器注册表”屏幕中填写所需的值。

    | 设置      | 建议的值  | 描述                                |
    | ------------ |  ------- | -------------------------------------------------- |
    | **DNS 前缀** | 全局唯一名称 | 用于唯一标识容器注册表的名称。 |
    | **订阅** | 选择订阅 | 要使用的 Azure 订阅。 |
    | **[资源组](/azure/azure-resource-manager/resource-group-overview)** | myResourceGroup |  要在其中创建容器注册表的资源组的名称。 选择“新建”  创建新的资源组。|
    | **[SKU](/azure/container-registry/container-registry-skus)** | 标准 | 容器注册表的服务层  |
    | **注册表位置** | 靠近你的位置 | 在你附近或将使用容器注册表的其他服务附近的[区域](https://azure.microsoft.com/regions/)中，选择位置。 |

    ![Visual Studio 的创建 Azure 容器注册表对话框的屏幕截图。](media/container-tools-react/vs-2022/azure-container-registry-details.png)

1. 选择“创建”，然后选择“完成” 。

   ![显示选择或创建新 Azure 容器注册表的屏幕截图。](media/container-tools-react/vs-2022/publish-dialog-2.png)

   发布过程结束时，你可查看发布设置并在需要时对其进行编辑，也可使用“发布”按钮再次发布该图像。

   :::image type="content" alt-text="显示成功发布的屏幕截图" source="media/container-tools-react/vs-2022/publish-succeeded.png" lightbox="media/container-tools-react/vs-2022/publish-succeeded.png":::

   若要使用“发布”对话框重新开始，请使用此页上的“删除”链接删除发布配置文件，然后再次选择“发布”  。
:::moniker-end

## <a name="next-steps"></a>后续步骤

现在可以将容器从注册表中拖放到任何能够运行 Docker 映像的主机上，例如[Azure 容器实例](/azure/container-instances/container-instances-tutorial-deploy-app)。

## <a name="additional-resources"></a>其他资源

* [利用 Visual Studio 进行容器开发](./index.yml)
* [使用 Docker 排查 Visual Studio 开发方面的问题](troubleshooting-docker-errors.md)
* [Visual Studio 容器工具 GitHub 存储库](https://github.com/Microsoft/DockerTools)


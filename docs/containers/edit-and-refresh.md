---
title: 在本地 Docker 容器中调试应用 | Microsoft Docs
description: 了解如何通过编辑和刷新以及设置调试断点功能来修改本地 Docker 容器中运行的应用以及刷新容器。
ms.author: ghogen
author: ghogen
manager: jmartens
ms.assetid: 480e3062-aae7-48ef-9701-e4f9ea041382
ms.topic: how-to
ms.workload: multiple
ms.date: 10/27/2021
ms.technology: vs-container-tools
ms.openlocfilehash: facc4cc696cd42672bec49f8df2e2907e9e9aadf
ms.sourcegitcommit: 1ed233bb3afc5ae1f52aff8e41f7e650342033ad
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/31/2022
ms.locfileid: "141274758"
---
# <a name="debug-apps-in-a-local-docker-container"></a>在本地 Docker 容器中调试应用

Visual Studio 提供了一种一致方法来开发 Docker 容器，并在本地验证应用程序。
可以在安装了 Docker 的本地 Windows 桌面上运行的 Linux 或 Windows 容器中运行和调试应用，且每次更改代码时都无需重新启动容器。

:::moniker range="vs-2017"
本文介绍了如何使用 Visual Studio 在本地 Docker 容器中启动应用、进行更改，并刷新浏览器以查看所做的更改。 本文还介绍了如何为容器化的应用设置用于调试的断点。 支持的项目类型包括 .NET Framework 和 .NET Core Web 及控制台应用。 本文使用 ASP.NET Core Web 应用和 .NET Framework 控制台应用。
:::moniker-end

:::moniker range=">=vs-2019"
本文介绍了如何使用 Visual Studio 在本地 Docker 容器中启动应用、进行更改，并刷新浏览器以查看所做的更改。 本文还介绍了如何为容器化的应用设置用于调试的断点。 支持的项目类型包括 .NET Framework、.NET Core Web 和控制台应用以及 Azure Functions。 本文使用 ASP.NET Core Web 应用和 .NET Framework 控制台应用。
:::moniker-end

如果你具有支持类型的项目，则 Visual Studio 可以创建 Dockerfile 并将项目配置为在容器中运行。 请参阅 [Visual Studio 中的容器工具](overview.md)。

## <a name="prerequisites"></a>先决条件

若要在本地 Docker 容器中调试应用，必须安装以下工具：

::: moniker range="vs-2017"

* 安装了 Web 开发工作负荷的 [Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)

::: moniker-end

::: moniker range="vs-2019"

* 安装了 Web 开发工作负荷的 [Visual Studio 2019](https://visualstudio.microsoft.com/downloads)

::: moniker-end

::: moniker range="vs-2022"

* 安装了 Web 开发工作负荷的 [Visual Studio 2022](https://visualstudio.microsoft.com/downloads)

::: moniker-end

若要在本地运行 Docker 容器，必须安装本地 Docker 客户端。 你可以使用 [Docker Desktop](https://www.docker.com/get-docker)，这需要 Windows 10 或更高版本。

Docker 容器可用于 .NET Framework 和 .NET Core 项目。 请看以下两个示例。 首先，我们来了解一下 .NET Core Web 应用。 接下来，我们来了解 .NET Framework 控制台应用。

## <a name="create-a-web-app"></a>创建 Web 应用

如果你有一个项目，并且已按照[概述](overview.md)中的说明添加了 Docker 支持，请跳过此部分。

::: moniker range="vs-2017"
[!INCLUDE [create-aspnet5-app](../azure/includes/create-aspnet5-app.md)]
::: moniker-end
::: moniker range="vs-2019"
[!INCLUDE [create-aspnet5-app-2019](../azure/includes/vs-2019/create-aspnet5-app-2019.md)]
::: moniker-end
::: moniker range=">=vs-2022"
[!INCLUDE [create-aspnet5-app-2022](../azure/includes/vs-2022/create-aspnet5-app-2022.md)]
::: moniker-end

### <a name="edit-your-razor-pages-and-refresh"></a>编辑 Razor 页面并刷新

若要在 Razor 页中快速访问更改，可以在容器中启动应用程序。 然后，继续进行更改，就像查看 IIS Express 一样查看这些更改。 

1. 请确保 Docker 设置为使用你所使用的容器类型（Linux 或 Windows）。 右键单击任务栏上的 Docker 图标，然后选择相应的“切换到 Linux 容器”或“切换到 Windows 容器”。

1. （仅限 .NET Core 3 及更高版本）在 3.0 及以上版本的 .NET Core 中的默认模板不支持按此部分所述的方式编辑代码和刷新运行的站点。 为了启用此功能，请添加 NuGet 包 [Microsoft.AspNetCore.Mvc.Razor.RuntimeCompilation](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Razor.RuntimeCompilation/) 在 Startup.cs 中，在 `ConfigureServices` 方法的代码中添加对扩展方法 `IMvcBuilder.AddRazorRuntimeCompilation` 的调用。 由于你只需在调试模式中启用此功能，因此请按如下所示的方法进行编码：

    ```csharp
    public IWebHostEnvironment Env { get; set; }

    public void ConfigureServices(IServiceCollection services)
    {
        IMvcBuilder builder = services.AddRazorPages();

    #if DEBUG
        if (Env.IsDevelopment())
        {
            builder.AddRazorRuntimeCompilation();
        }
    #endif

        // code omitted for brevity
    }
    ```

    按如下所示修改 `Startup` 方法：

    ```csharp
    public Startup(IConfiguration configuration, IWebHostEnvironment webHostEnvironment)
    {
        Configuration = configuration;
        Env = webHostEnvironment;
    }
    ```

   有关详细信息，请参阅 [ASP.NET Core 中的 Razor 文件编译](/aspnet/core/mvc/views/view-compilation?view=aspnetcore-3.1&preserve-view=true)。

1. 将“解决方案配置”设置为“调试” 。 然后，按 Ctrl+F5 以生成 Docker 映像并在本地运行该映像 。

    在 Docker 容器中生成映像并运行该映像后，Visual Studio 会在默认浏览器中启动 Web 应用。

1. 转到“索引”页。 我们将在此页上进行更改。
1. 返回到 Visual Studio 并打开 Index.cshtml。
1. 将以下 HTML 内容添加到文件末尾，然后保存所做的更改。

    ```html
    <h1>Hello from a Docker container!</h1>
    ```

1. 在输出窗口中，在 .NET 生成完成并看到下面的行后，切换回浏览器并刷新页面：

   ```output
   Now listening on: http://*:80
   Application started. Press Ctrl+C to shut down.
   ```

你的更改已应用！

### <a name="debug-with-breakpoints"></a>使用断点进行调试

通常，需要对所做的更改进行进一步检查。 可以使用 Visual Studio 的调试功能来完成此任务。

1. 在 Visual Studio 中，打开 Index.cshtml.cs。
2. 将 `OnGet` 方法的内容替换为以下代码：

   ```csharp
       ViewData["Message"] = "Your application description page from within a container";
   ```

3. 在代码行的左侧设置一个断点。
4. 要启动调试并命中断点，请按 F5。
5. 切换到 Visual Studio 以查看断点。 检查值。

   :::moniker range="vs-2019"
   ![显示 Visual Studio 中 Index.cshtml.cs 的部分代码的屏幕截图，其中在以黄色突出显示的代码行的左侧设置了一个断点。](media/edit-and-refresh/breakpoint.png)
   :::moniker-end
   :::moniker range=">=vs-2022"
   ![显示 Visual Studio 中 Index.cshtml.cs 的部分代码的屏幕截图，其中在以黄色突出显示的代码行的左侧设置了一个断点。](media/edit-and-refresh/vs-2022/breakpoint.png)
   :::moniker-end

## <a name="create-a-net-framework-console-app"></a>创建 .NET Framework 控制台应用

使用 .NET Framework 控制台应用项目时，不支持在没有业务流程的情况下添加 Docker 支持的方式。 即使仅使用单个 Docker 项目，你仍可以使用以下过程。

1. 创建新的 .NET Framework 控制台应用项目。
1. 在解决方案资源管理器中，右键单击项目节点，然后选择“添加” > “容器业务流程支持” 。  在出现的对话框中，选择“Docker Compose”。 将 Dockerfile 添加到项目中，并添加一个包含相关支持文件的 Docker Compose 项目。

### <a name="debug-with-breakpoints"></a>使用断点进行调试

1. 在解决方案资源管理器中，打开 Program.cs。
2. 将 `Main` 方法的内容替换为以下代码：

   ```csharp
       System.Console.WriteLine("Hello, world!");
   ```

3. 在代码行的左侧设置一个断点。
4. 要启动调试并命中断点，请按 F5。
5. 切换到 Visual Studio 以查看断点，并检查值。

   :::moniker range="<=vs-2019"
   ![Visual Studio 中 Program.cs 的代码窗口的屏幕截图，其中在以黄色突出显示的代码行的左侧设置了一个断点。](media/edit-and-refresh/breakpoint-console.png)
   ::: moniker-end

## <a name="container-reuse"></a>容器重复使用

在开发周期中，Visual Studio 在你更改 Dockerfile 后仅重新生成容器映像和容器本身。 如果不更改 Dockerfile，Visual Studio 将重复使用以前运行的容器。

如果你手动修改了容器，并希望使用干净的容器映像重启，请使用 Visual Studio 中的“Build” > “Clean”命令，然后按常规操作生成 。

## <a name="troubleshoot"></a>疑难解答

了解如何对 [Visual Studio Docker 开发进行故障排除](troubleshooting-docker-errors.md)。

## <a name="next-steps"></a>后续步骤

有关更多详细信息，请参阅 [Visual Studio 如何构建容器化应用](container-build.md)。

## <a name="more-about-docker-with-visual-studio-windows-and-azure"></a>有关 Visual Studio、Windows 和 Azure 中 Docker 的详细信息

* 详细了解[使用 Visual Studio 进行容器开发](./index.yml)。
* 要生成和部署 Docker 容器，请参阅 [Azure Pipelines 的 Docker 集成](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker)。
* 有关 Windows Server 和 Nano Server 文章的索引，请参阅 [Windows 容器信息](/virtualization/windowscontainers/)。
* 详细了解 [Azure Kubernetes 服务](https://azure.microsoft.com/services/kubernetes-service/)并查看 [Azure Kubernetes 服务文档](/azure/aks)。

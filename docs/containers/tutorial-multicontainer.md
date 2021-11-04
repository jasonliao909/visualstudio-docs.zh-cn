---
title: 使用 Docker Compose 处理多个容器
author: ghogen
description: 了解如何将多个容器与 Docker Compose 配合使用
ms.custom: SEO-VS-2020
ms.author: ghogen
ms.date: 10/08/2021
ms.technology: vs-container-tools
ms.topic: tutorial
ms.openlocfilehash: 50e634e56f88c08ff23a0b668b74c0373d8d9dca
ms.sourcegitcommit: 4efdab6a579b31927c42531bb3f7fdd92890e4ac
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/26/2021
ms.locfileid: "130351519"
---
# <a name="tutorial-create-a-multi-container-app-with-docker-compose"></a>教程：使用 Docker Compose 创建多容器应用

本教程介绍如何在 Visual Studio 中使用容器工具管理多个容器并在容器之间通信。  管理多个容器需要容器业务流程，并需要 Docker Compose、Kubernetes 或 Service Fabric 等业务流程协调程序  。 我们将在这里使用 Docker Compose。 Docker Compose 非常适用于开发周期中的本地调试和测试。

## <a name="prerequisites"></a>先决条件

::: moniker range="vs-2017"

* [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
* 安装了“Web 开发”、“Azure 工具”工作负载或“.NET Core 跨平台开发”工作负载的 [Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)   
::: moniker-end

::: moniker range="vs-2019"

* [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
* 安装了“Web 开发”、“Azure 工具”工作负载和/或“.NET 跨平台开发”工作负载的 [Visual Studio 2019](https://visualstudio.microsoft.com/downloads)
* 用于使用 .NET Core 3.1 进行开发的 [.NET Core 3 开发工具](https://dotnet.microsoft.com/download/dotnet-core/3.1)。
::: moniker-end

::: moniker range=">=vs-2022"

* [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
* 安装了“Web 开发”、“Azure 工具”工作负载和/或“.NET 跨平台开发”工作负载的 [Visual Studio 2022 RC](https://visualstudio.microsoft.com/vs/preview/)  。 这包括 .NET Core 3.1 和 .NET 6 开发工具。
* [.NET 5 开发工具](https://dotnet.microsoft.com/download/dotnet-core/5.0)，用于通过 .NET 5 进行开发。
::: moniker-end

## <a name="create-a-web-application-project"></a>创建 Web 应用程序项目

在 Visual Studio 中，创建一个名为 `WebFrontEnd` 的“ASP.NET Core Web 应用”项目，以使用 Razor Pages 创建 Web 应用程序。
  
::: moniker range="vs-2017"

请不要选择“启用 Docker 支持”  。 稍后添加 Docker 支持。

![创建 Web 项目的屏幕截图。](./media/tutorial-multicontainer/docker-tutorial-enable-docker-support.png)

::: moniker-end

::: moniker range="vs-2019"

![显示“创建 ASP.NET Core Web 项目”的屏幕截图。](./media/tutorial-multicontainer/vs-2019/create-web-project1.png)

请不要选择“启用 Docker 支持”  。 稍后添加 Docker 支持。

![创建 Web 项目时的“其他信息”屏幕的屏幕截图。 未选择“启用 Docker 支持”选项。](./media/tutorial-multicontainer/vs-2019/create-web-project-additional-information.png)

::: moniker-end
::: moniker range=">=vs-2022"

![显示“创建 ASP.NET Core Web 项目”的屏幕截图。](./media/tutorial-multicontainer/vs-2022/create-web-project.png)

请不要选择“启用 Docker 支持”  。 稍后添加 Docker 支持。

![创建 Web 项目时的“其他信息”屏幕的屏幕截图。 未选择“启用 Docker 支持”选项。](./media/tutorial-multicontainer/vs-2022/create-web-project-additional-information.png)

::: moniker-end

## <a name="create-a-web-api-project"></a>创建 Web API 项目

将项目添加到同一解决方案中，并将其称为 MyWebAPI  。 对于“项目类型”，选择“API”，并清除“HTTPS 配置”复选框   。 在此设计中，我们仅将 SSL 用于客户端通信，而不用于在同一个 Web 应用程序中的容器之间进行通信。 只有 `WebFrontEnd` 需要 HTTPS，且示例中的代码假定你已清除该复选框。 通常，Visual Studio 使用的 .NET 开发人员证书仅支持用于外部到容器的请求，而不适用于容器到容器的请求。

::: moniker range="vs-2017"
   ![创建 Web API 项目的屏幕截图。](./media/tutorial-multicontainer/docker-tutorial-mywebapi.png)
::: moniker-end
::: moniker range="vs-2019"
   ![创建 Web API 项目的屏幕截图。](./media/tutorial-multicontainer/vs-2019/create-webapi-project.png)
::: moniker-end
::: moniker range=">=vs-2022"
   ![创建 Web API 项目的屏幕截图。](media/tutorial-multicontainer/vs-2022/create-web-api-project.png)
::: moniker-end

## <a name="add-code-to-call-the-web-api"></a>添加用于调用 Web API 的代码

:::moniker range="vs-2017"

1. 在 `WebFrontEnd` 项目中，打开 Index.cshtml.cs 文件，使用以下代码替换 `OnGet` 方法。

   ```csharp
    public async Task OnGet()
    {
       ViewData["Message"] = "Hello from webfrontend";

       using (var client = new System.Net.Http.HttpClient())
       {
          // Call *mywebapi*, and display its response in the page
          var request = new System.Net.Http.HttpRequestMessage();
          request.RequestUri = new Uri("http://mywebapi/WeatherForecast");
          // request.RequestUri = new Uri("http://mywebapi/api/values/1"); // For ASP.NET 2.x, comment out previous line and uncomment this line.
          var response = await client.SendAsync(request);
          ViewData["Message"] += " and " + await response.Content.ReadAsStringAsync();
       }
    }
   ```
   
    > [!NOTE]
    > 在实际的代码中，不应在每次请求后释放 `HttpClient`。 有关最佳做法，请参阅[使用 HttpClientFactory 实现复原 HTTP 请求](/dotnet/architecture/microservices/implement-resilient-applications/use-httpclientfactory-to-implement-resilient-http-requests)。

1. 在 Index.cshtml 文件中，添加一行以显示 `ViewData["Message"]`，以便该文件看起来如以下代码：
    
      ```cshtml
      @page
      @model IndexModel
      @{
          ViewData["Title"] = "Home page";
      }
    
      <div class="text-center">
          <h1 class="display-4">Welcome</h1>
          <p>Learn about <a href="/aspnet/core">building Web apps with ASP.NET Core</a>.</p>
          <p>@ViewData["Message"]</p>
      </div>
      ```

1. （仅限 ASP.NET 2.x）现在在 Web API 项目中，将代码添加到“值”控制器以自定义 API 针对从 webfrontend 添加的调用返回的消息。
    
      ```csharp
        // GET api/values/5
        [HttpGet("{id}")]
        public ActionResult<string> Get(int id)
        {
            return "webapi (with value " + id + ")";
        }
      ```

    使用 .NET Core 3.1 和更高版本则不需要执行此操作，因为你可以使用已存在的 WeatherForecast API。 但是，你需要在 Web API 项目中注释掉对 <xref:Microsoft.AspNetCore.Builder.HttpsPolicyBuilderExtensions.UseHttpsRedirection*> 的调用，因为此代码使用 HTTP 而不是 HTTPS 来调用 Web API。

    ```csharp
                //app.UseHttpsRedirection();
    ```

1. 在 `WebFrontEnd` 项目中，依次选择“添加”、“容器业务流程协调程序支持”。 此时显示“Docker 支持选项”对话框。

1. 选择“Docker Compose”。

1. 选择目标操作系统，例如 Linux。

   ![选择目标操作系统的屏幕截图。](media/tutorial-multicontainer/docker-tutorial-docker-support-options.PNG)

   Visual Studio 会在解决方案中的“docker-compose”节点上创建 docker-compose.yml 文件和 .dockerignore 文件，该项目以粗体字体显示，表明其为启动项目。

   ![添加了 docker-compose 项目的解决方案资源管理器的屏幕截图。](media/tutorial-multicontainer/multicontainer-solution-explorer.png)

   显示 docker-compose.yml，如下所示：

   ```yaml
   version: '3.4'

    services:
      webfrontend:
        image: ${DOCKER_REGISTRY-}webfrontend
        build:
          context: .
          dockerfile: WebFrontEnd/Dockerfile
   ```

   .dockerignore 文件包含你不希望 Docker 在容器中包含的文件类型和扩展名。 这些文件通常与开发环境和源代码管理相关联，并不属于正在开发的应用或服务。

   查看“输出”窗格的“容器工具”部分，深入了解正在运行的命令。  可看到命令行工具 docker-compose 用于配置和创建运行时容器。

1. 在 Web API 项目中，再次右键单击项目节点，然后选择“添加” > “容器业务流程协调程序支持” 。 选择“Docker Compose”，然后选择相同的目标操作系统。  

    > [!NOTE]
    > 在此步中，Visual Studio 会创建 Dockerfile。 如果对已具有 Docker 支持的项目执行此操作，系统将提示是否要覆盖现有的 Dockerfile。 如果已在 Dockerfile 中进行了所需的更改，请选择“否”。

    Visual Studio 对 docker compose YML 文件进行一些更改。 现在，这两项服务都包括在内。

    ```yaml
    version: '3.4'
    
    services:
      webfrontend:
        image: ${DOCKER_REGISTRY-}webfrontend
        build:
          context: .
          dockerfile: WebFrontEnd/Dockerfile
    
      mywebapi:
        image: ${DOCKER_REGISTRY-}mywebapi
        build:
          context: .
          dockerfile: MyWebAPI/Dockerfile
    ```

1. 若要在本地运行站点，必须使用不同的 URL 来请求 Web API 服务，因为 docker compose 在其自己的网络中设置主机名，以便 `mywebapi` 作为主机名显示给其他服务。 若要在本地运行，请先将 Index.cshtml.cs 中 `OnGet` 方法中的 `mywebapi` 替换为 localhost 和端口语法。 你可以从启动 webapi 项目自行获得端口号，或者从“项目属性”的“调试”部分中的“应用 URL”设置中获取端口号 (Alt+Enter)。

   ```csharp
   request.RequestUri = new Uri("http://localhost:{port}/WeatherForecast");
   ```

1. 立即在本地运行站点，验证站点是否按预期方式工作。 右键单击 Web API 项目，选择“设为启动项目”，然后选择“调试” > “在不调试的情况下启动”。 然后，右键单击 WebFrontEnd 项目节点，选择“设为启动项目”，并按 F5 开始调试。

   如果 .NET Core 2.x 版本中的所有内容配置正确，你将看到消息“来自 webfrontend 和 webapi 的问候(值为 1)。”  通过 .NET Core 3，可以看到天气预测数据。

   验证其在本地运行后，请在 Index.cshtml.cs 中将 `OnGet` 中的 URL 更改回引用 mywebapi，以准备在 Docker Compose 中运行。 如果要对 Docker 和非容器运行和调试配置使用相同代码，可能需要使用配置文件来获取 URL。

1. 添加容器业务流程时使用的第一个项目设置为在运行或调试时启动。 可以在 docker-compose 项目的“项目属性”中配置启动操作。  在 docker-compose 项目节点上，右键单击以打开上下文菜单，然后选择“属性”，或使用 Alt+Enter。  以下屏幕截图显示需要解决方案在此使用的属性。  例如，可以通过自定义“服务 URL”属性来更改已加载的页面。

   ![docker-compose 项目属性的屏幕截图。](media/tutorial-multicontainer/launch-action.png)

   下面是启动时看到的内容（.NET Core 2.x 版本）：

   ![正在运行的 Web 应用的屏幕截图。](media/tutorial-multicontainer/webfrontend.png)

   适用于 .NET 3.1 的 Web 应用显示 JSON 格式的天气数据。

:::moniker-end

::: moniker range="vs-2019"

1. 在 `WebFrontEnd` 项目中，打开 Index.cshtml.cs 文件，使用以下代码替换 `OnGet` 方法。

   ```csharp
    public async Task OnGet()
    {
       ViewData["Message"] = "Hello from webfrontend";

       using (var client = new System.Net.Http.HttpClient())
       {
          // Call *mywebapi*, and display its response in the page
          var request = new System.Net.Http.HttpRequestMessage();
          request.RequestUri = new Uri("http://mywebapi/WeatherForecast");
          // request.RequestUri = new Uri("http://mywebapi/api/values/1"); // For ASP.NET 2.x, comment out previous line and uncomment this line.
          var response = await client.SendAsync(request);
          ViewData["Message"] += " and " + await response.Content.ReadAsStringAsync();
       }
    }
   ```
   
    > [!NOTE]
    > 在实际的代码中，不应在每次请求后释放 `HttpClient`。 有关最佳做法，请参阅[使用 HttpClientFactory 实现复原 HTTP 请求](/dotnet/architecture/microservices/implement-resilient-applications/use-httpclientfactory-to-implement-resilient-http-requests)。

1. 在 Index.cshtml 文件中，添加一行以显示 `ViewData["Message"]`，以便该文件看起来如以下代码：
    
      ```cshtml
      @page
      @model IndexModel
      @{
          ViewData["Title"] = "Home page";
      }
    
      <div class="text-center">
          <h1 class="display-4">Welcome</h1>
          <p>Learn about <a href="/aspnet/core">building Web apps with ASP.NET Core</a>.</p>
          <p>@ViewData["Message"]</p>
      </div>
      ```

1. （仅限 ASP.NET 2.x）现在在 Web API 项目中，将代码添加到“值”控制器以自定义 API 针对从 webfrontend 添加的调用返回的消息。
    
      ```csharp
        // GET api/values/5
        [HttpGet("{id}")]
        public ActionResult<string> Get(int id)
        {
            return "webapi (with value " + id + ")";
        }
      ```

    使用 .NET Core 3.1 和更高版本则不需要执行此操作，因为你可以使用已存在的 WeatherForecast API。 但是，你需要在 Web API 项目中注释掉对 <xref:Microsoft.AspNetCore.Builder.HttpsPolicyBuilderExtensions.UseHttpsRedirection*> 的调用，因为此代码使用 HTTP 而不是 HTTPS 来调用 Web API。

    ```csharp
                //app.UseHttpsRedirection();
    ```

1. 在 `WebFrontEnd` 项目中，依次选择“添加”、“容器业务流程协调程序支持”。 此时显示“Docker 支持选项”对话框。

1. 选择“Docker Compose”。

1. 选择目标操作系统，例如 Linux。

   ![选择目标操作系统的屏幕截图。](media/tutorial-multicontainer/docker-tutorial-docker-support-options.PNG)

   Visual Studio 会在解决方案中的“docker-compose”节点上创建 docker-compose.yml 文件和 .dockerignore 文件，该项目以粗体字体显示，表明其为启动项目。

   ![添加了 docker-compose 项目的解决方案资源管理器的屏幕截图。](media/tutorial-multicontainer/multicontainer-solution-explorer.png)

   显示 docker-compose.yml，如下所示：

   ```yaml
   version: '3.4'

    services:
      webfrontend:
        image: ${DOCKER_REGISTRY-}webfrontend
        build:
          context: .
          dockerfile: WebFrontEnd/Dockerfile
   ```

   .dockerignore 文件包含你不希望 Docker 在容器中包含的文件类型和扩展名。 这些文件通常与开发环境和源代码管理相关联，并不属于正在开发的应用或服务。

   查看“输出”窗格的“容器工具”部分，深入了解正在运行的命令。  可看到命令行工具 docker-compose 用于配置和创建运行时容器。

1. 在 Web API 项目中，再次右键单击项目节点，然后选择“添加” > “容器业务流程协调程序支持” 。 选择“Docker Compose”，然后选择相同的目标操作系统。  

    > [!NOTE]
    > 在此步中，Visual Studio 会创建 Dockerfile。 如果对已具有 Docker 支持的项目执行此操作，系统将提示是否要覆盖现有的 Dockerfile。 如果已在 Dockerfile 中进行了所需的更改，请选择“否”。

    Visual Studio 对 docker compose YML 文件进行一些更改。 现在，这两项服务都包括在内。

    ```yaml
    version: '3.4'
    
    services:
      webfrontend:
        image: ${DOCKER_REGISTRY-}webfrontend
        build:
          context: .
          dockerfile: WebFrontEnd/Dockerfile
    
      mywebapi:
        image: ${DOCKER_REGISTRY-}mywebapi
        build:
          context: .
          dockerfile: MyWebAPI/Dockerfile
    ```

1. 若要在本地运行站点，必须使用不同的 URL 来请求 Web API 服务，因为 docker compose 在其自己的网络中设置主机名，以便 `mywebapi` 作为主机名显示给其他服务。 若要在本地运行，请先将 Index.cshtml.cs 中 `OnGet` 方法中的 `mywebapi` 替换为 localhost 和端口语法。 你可以从启动 webapi 项目自行获得端口号，或者从“项目属性”的“调试”部分中的“应用 URL”设置中获取端口号 (Alt+Enter)。

   ```csharp
   request.RequestUri = new Uri("http://localhost:{port}/WeatherForecast");
   ```

1. 立即在本地运行站点，验证站点是否按预期方式工作。 右键单击 Web API 项目，选择“设为启动项目”，然后选择“调试” > “在不调试的情况下启动”。 然后，右键单击 WebFrontEnd 项目节点，选择“设为启动项目”，并按 F5 开始调试。

   如果 .NET Core 2.x 版本中的所有内容配置正确，你将看到消息“来自 webfrontend 和 webapi 的问候(值为 1)。”  通过 .NET Core 3，可以看到天气预测数据。

   验证其在本地运行后，请在 Index.cshtml.cs 中将 `OnGet` 中的 URL 更改回引用 mywebapi，以准备在 Docker Compose 中运行。 如果要对 Docker 和非容器运行和调试配置使用相同代码，可能需要使用配置文件来获取 URL。

1. 添加容器业务流程时使用的第一个项目设置为在运行或调试时启动。 可以在 docker-compose 项目的“项目属性”中配置启动操作。  在 docker-compose 项目节点上，右键单击以打开上下文菜单，然后选择“属性”，或使用 Alt+Enter。  以下屏幕截图显示需要解决方案在此使用的属性。  例如，可以通过自定义“服务 URL”属性来更改已加载的页面。

   ![docker-compose 项目属性的屏幕截图。](media/tutorial-multicontainer/launch-action.png)

   下面是启动时看到的内容（.NET Core 2.x 版本）：

   ![正在运行的 Web 应用的屏幕截图。](media/tutorial-multicontainer/webfrontend.png)

   适用于 .NET 3.1 的 Web 应用显示 JSON 格式的天气数据。

1. 现在假设只需将调试器附加到 WebFrontEnd，而不是 Web API 项目。 从菜单栏中，可以使用“开始”按钮旁的下拉列表来显示调试选项菜单；选择“管理 Docker Compose 启动设置”。

   ![调试“管理 Compose 设置”菜单项的屏幕截图。](media/launch-settings/debug-dropdown-manage-compose.png)

   随即出现“管理 Docker Compose 启动设置”对话框。 使用此对话框，你可以控制在调试会话过程中启动的服务子集，这些服务子集在附加或未附加调试器、启动服务和 URL的情况下启动。 请参阅[启动 Compose 服务的子集](launch-profiles.md)。

   ![“管理 Docker Compose 启动设置”对话框的屏幕截图。](media/tutorial-multicontainer/vs-2022/launch-profile-1.png)

   选择“新建”以创建新的配置文件，并将其命名为 `Debug WebFrontEnd only`。 然后，将 Web API 项目设置为“在不调试的情况下启动”，将“WebFrontEnd”项目设置为“启动时调试”，然后选择“保存”。

   新配置将被选作下一个 F5 的默认配置。

1. 按 F5 确认它按预期方式工作。

恭喜，你运行的是具有自定义 Docker Compose 配置文件的 Docker Compose 应用程序。


::: moniker-end
::: moniker range=">=vs-2022"

1. 在 `WebFrontEnd` 项目中，打开 Index.cshtml.cs 文件，使用以下代码替换 `OnGet` 方法。

   ```csharp
    public async Task OnGet()
    {
       ViewData["Message"] = "Hello from webfrontend";

       using (var client = new System.Net.Http.HttpClient())
       {
          // Call *mywebapi*, and display its response in the page
          var request = new System.Net.Http.HttpRequestMessage();
          request.RequestUri = new Uri("http://mywebapi/WeatherForecast");
          ViewData["Message"] += " and " + await response.Content.ReadAsStringAsync();
       }
    }
   ```

    > [!NOTE]
    > 在实际的代码中，不应在每次请求后释放 `HttpClient`。 有关最佳做法，请参阅[使用 HttpClientFactory 实现复原 HTTP 请求](/dotnet/architecture/microservices/implement-resilient-applications/use-httpclientfactory-to-implement-resilient-http-requests)。

1. 在 Index.cshtml 文件中，添加一行以显示 `ViewData["Message"]`，以便该文件看起来如以下代码：

      ```cshtml
      @page
      @model IndexModel
      @{
          ViewData["Title"] = "Home page";
      }
    
      <div class="text-center">
          <h1 class="display-4">Welcome</h1>
          <p>Learn about <a href="/aspnet/core">building Web apps with ASP.NET Core</a>.</p>
          <p>@ViewData["Message"]</p>
      </div>
      ```

1. 在 Web API 项目中，注释掉对 <xref:Microsoft.AspNetCore.Builder.HttpsPolicyBuilderExtensions.UseHttpsRedirection*> 的调用，因为此代码使用 HTTP 而不是 HTTPS 来调用 Web API。

    ```csharp
                //app.UseHttpsRedirection();
    ```

1. 在 `WebFrontEnd` 项目中，依次选择“添加”、“容器业务流程协调程序支持”。 此时显示“Docker 支持选项”对话框。

1. 选择“Docker Compose”。

1. 选择目标操作系统，例如 Linux。

   ![选择目标操作系统的屏幕截图。](media/tutorial-multicontainer/docker-tutorial-docker-support-options.PNG)

   Visual Studio 会在解决方案中的“docker-compose”节点上创建 docker-compose.yml 文件和 .dockerignore 文件，该项目以粗体字体显示，表明其为启动项目。

   ![添加了 docker-compose 项目的解决方案资源管理器的屏幕截图。](media/tutorial-multicontainer/vs-2022/multicontainer-solution-explorer.png)

   显示 docker-compose.yml，如下所示：

   ```yaml
   version: '3.4'

    services:
      webfrontend:
        image: ${DOCKER_REGISTRY-}webfrontend
        build:
          context: .
          dockerfile: WebFrontEnd/Dockerfile
   ```

   .dockerignore 文件包含你不希望 Docker 在容器中包含的文件类型和扩展名。 这些文件通常与开发环境和源代码管理相关联，并不属于正在开发的应用或服务。

   查看“输出”窗格的“容器工具”部分，深入了解正在运行的命令。  可看到命令行工具 docker-compose 用于配置和创建运行时容器。

1. 在 Web API 项目中，再次右键单击项目节点，然后选择“添加” > “容器业务流程协调程序支持” 。 选择“Docker Compose”，然后选择相同的目标操作系统。  

    > [!NOTE]
    > 在此步中，Visual Studio 会创建 Dockerfile。 如果对已具有 Docker 支持的项目执行此操作，系统将提示是否要覆盖现有的 Dockerfile。 如果已在 Dockerfile 中进行了所需的更改，请选择“否”。

    Visual Studio 对 docker compose YML 文件进行一些更改。 现在，这两项服务都包括在内。

    ```yaml
    version: '3.4'
    
    services:
      webfrontend:
        image: ${DOCKER_REGISTRY-}webfrontend
        build:
          context: .
          dockerfile: WebFrontEnd/Dockerfile
    
      mywebapi:
        image: ${DOCKER_REGISTRY-}mywebapi
        build:
          context: .
          dockerfile: MyWebAPI/Dockerfile
    ```

1. 若要在本地运行站点，必须使用不同的 URL 来请求 Web API 服务，因为 docker compose 在其自己的网络中设置主机名，以便 `mywebapi` 作为主机名显示给其他服务。 若要在本地运行，请先将 Index.cshtml.cs 中 `OnGet` 方法中的 `mywebapi` 替换为 localhost 和端口语法。 可以获取端口号，只需自行启动 webapi 项目，也可以在“调试”部分的“项目属性”中找到它，选择“打开调试启动配置文件 UI”，然后选择“IIS Express”，并查找“应用 URL”设置。

   ```csharp
   request.RequestUri = new Uri("http://localhost:{port}/WeatherForecast");
   ```

   立即在 IIS Express 中本地运行该站点，验证它是否按预期方式工作：右键单击 Web API 项目，然后选择“调试” > “在不调试的情况下启动”。 然后，右键单击 WebFrontEnd 项目节点，选择“设为启动项目”，并按 F5 开始调试。 如果一切配置正确，则会看到天气预报数据。

   验证其在本地运行后，请在 Index.cshtml.cs 中将 `OnGet` 中的 URL 更改回引用 mywebapi，以准备在 Docker Compose 中运行。 如果要对 Docker 和非容器运行和调试配置使用相同代码，可能需要使用配置文件来获取 URL。

1. 添加容器业务流程时使用的第一个项目设置为在运行或调试时启动。 可以在 docker-compose 项目的“项目属性”中配置启动操作。  在 docker-compose 项目节点上，右键单击以打开上下文菜单，然后选择“属性”，或使用 Alt+Enter。  以下屏幕截图显示需要解决方案在此使用的属性。  例如，可以通过自定义“服务 URL”属性来更改已加载的页面。

   ![docker-compose 项目属性的屏幕截图。](media/tutorial-multicontainer/launch-action.png)

   下面是启动时显示的内容：

   ![正在运行的 Web 应用的屏幕截图。](media/tutorial-multicontainer/vs-2022/webfrontend.png)

   Web 应用显示 JSON 格式的天气数据。

1. 现在假设只需将调试器附加到 WebFrontEnd，而不是 Web API 项目。 从菜单栏中，可以使用“开始”按钮旁的下拉列表来显示调试选项菜单；选择“管理 Docker Compose 启动设置”。

   ![调试“管理 Compose 设置”菜单项的屏幕截图。](media/tutorial-multicontainer/vs-2022/debug-dropdown-manage-compose.png)

   随即出现“管理 Docker Compose 启动设置”对话框。 使用此对话框，你可以控制在调试会话过程中启动的服务子集，这些服务子集在附加或未附加调试器、启动服务和 URL的情况下启动。 请参阅[启动 Compose 服务的子集](launch-profiles.md)。

   ![“管理 Docker Compose 启动设置”对话框的屏幕截图。](media/tutorial-multicontainer/vs-2022/launch-profile-1.png)

   选择“新建”以创建新的配置文件，并将其命名为 `Debug WebFrontEnd only`。 然后，将 Web API 项目设置为“在不调试的情况下启动”，将“WebFrontEnd”项目设置为“启动时调试”，然后选择“保存”。

   新配置将被选作下一个 F5 的默认配置。

1. 按 F5 确认它按预期方式工作。

恭喜，你运行的是具有自定义 Docker Compose 配置文件的 Docker Compose 应用程序。

::: moniker-end

## <a name="next-steps"></a>后续步骤

查看用于[将容器部署到 Azure](/azure/containers) 的选项。

## <a name="see-also"></a>另请参阅
  
[Docker Compose](https://docs.docker.com/compose/)  
[容器工具](./index.yml)
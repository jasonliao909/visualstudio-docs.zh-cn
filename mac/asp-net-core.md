---
title: ASP.NET Core 入门
description: 本文介绍如何在 Visual Studio for Mac 中开始使用 ASP.NET，包括安装和创建新项目。
author: jmatthiesen
ms.author: jomatthi
manager: dominicn
ms.date: 05/02/2022
ms.assetid: 6E8B0C90-33D6-4546-8207-CE0787584565
ms.custom: video, devdivchpfy22
no-loc:
- Blazor
- Blazor WebAssembly
ms.topic: how-to
monikerRange: '>=vsmac-2019'
ms.openlocfilehash: 698e342418c08e5f93ce13fb2958d4036f205959
ms.sourcegitcommit: 3034382894e610b55f3ad07e737fa59b91680869
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2022
ms.locfileid: "144548511"
---
# <a name="getting-started-with-aspnet-core"></a>ASP.NET Core 入门

 [!INCLUDE [Visual Studio for Mac](~/includes/applies-to-version/vs-mac-only.md)]

Visual Studio for Mac 支持最新的 ASP.NET Core Web 开发平台，使你可轻松开发自己的应用服务。 ASP.NET Core在 .NET 平台和运行时的最新演变上运行。 它经过调优，可提供极快的性能，进行分解后，更便于小规模安装，且经过重新构思设计，可在 Linux 和 macOS 以及 Windows 上运行。

::: moniker range="vsmac-2019"
## <a name="installing-net-core"></a>安装 .NET Core

安装 Visual Studio for Mac 时，将自动安装 .NET Core 3.1。 有关Visual Studio for Mac支持的 .NET Core 版本的详细信息，请参阅[支持的 .NET 版本](./supported-versions-net.md)。
::: moniker-end

::: moniker range="vsmac-2022"
## <a name="installing-net-6"></a>安装 .NET 6

安装Visual Studio for Mac时，会自动安装 .NET 6。 有关Visual Studio for Mac中支持的 .NET 版本的详细信息，请参阅[支持的 .NET 版本](./supported-versions-net.md)。
::: moniker-end

## <a name="creating-an-aspnet-core-app-in-visual-studio-for-mac"></a>在 Visual Studio for Mac 中创建 ASP.NET Core 应用

打开 Visual Studio for Mac。 在开始屏幕上，选择“新建项目…”

![此屏幕截图显示了在Visual Studio for Mac中创建 ASP.NET Core应用时的新Project对话框 ](media/asp-net-core-2019-new-asp-core.png)

将显示 **“新建Project**”对话框。 它允许你选择用于创建应用程序的模板。

有许多项目将为你提供预构建模板，以开始生成 ASP.NET Core应用程序。 它们分别是：

- **.NET Core > 空**
- **.NET Core > API**
- **.NET Core > Web 应用**
- **.NET Core > Web 应用（模型-视图-控制器）**
- **.NET Core > Blazor Server 应用**
- **.NET Core > Blazor WebAssembly 应用**

![此屏幕截图显示了在Visual Studio for Mac中创建 ASP.NET Core应用时 ASP.NET Project选项](media/asp-net-core-2019-new-asp-core.png)

选择 **ASP.NET Core空 Web 应用程序**，然后选择“**下一步**”。 为Project指定一个名称，然后选择“**创建**”。 这会创建新的 ASP.NET Core 应用。 在 **解决方案** 窗口的左窗格中，展开第二个箭头，然后选择 **Startup.cs**。 它应类似于下图：

:::image type="content" source="media/asp-net-core-2019-empty-project.png" alt-text="此屏幕截图显示创建 ASP.NET Core应用时的新 ASP.NET Core空Project视图。" lightbox="media/asp-net-core-2019-empty-project.png":::

ASP.NET Core空模板创建包含两个默认文件的 Web 应用程序：**Program.cs** 和 **Startup.cs**，此处对此进行了说明。 它还会创建一个 **Dependencies** 文件夹，其中包含项目的NuGet包依赖项，例如 ASP.NET Core、.NET Core 框架和生成项目的MSBuild目标：

![这是显示依赖项的解决方案窗口的屏幕截图。](media/asp-net-core-2019-solution-dependencies.png)

### <a name="programcs"></a>Program.cs

::: moniker range="vsmac-2019"

在项目中打开并检查“Program.cs”文件。 请注意，在 `Main` 方法中会发生几件事 – 应用中的项：

```csharp
    public class Program
    {
        public static void Main(string[] args)
        {
            CreateWebHostBuilder(args).Build().Run();
        }

        public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
            WebHost.CreateDefaultBuilder(args)
                .UseStartup<Startup>();
    }
```

ASP.NET Core 应用将通过 [`WebHostBuilder`](/aspnet/core/fundamentals/hosting) 实例配置并启动主机，以此在其 Main 方法中创建一个 Web 服务器。 此生成器提供配置主机的方法。 在模板应用中使用了以下配置：

- `.UseStartup<Startup>()`：指定启动类。

但是，也可以添加其他配置，例如：

- `UseKestrel`：指定应用将使用的 Kestrel 服务器
- `UseContentRoot(Directory.GetCurrentDirectory())`：从 Web 项目的根文件夹启动应用时，使用此文件夹作为应用的内容根
- `.UseIISIntegration()`：指定应用应使用 IIS。 要在 ASP.NET Core 中使用 IIS，需要指定 `UseKestrel` 和 `UseIISIntegration`。

### <a name="startupcs"></a>Startup.cs

可在 `CreateWebHostBuilder` 上的 `UseStartup()` 方法中指定应用的 Startup 类。 在此类中，你将指定请求处理管道，以及配置任何服务的位置。

在项目中打开并检查“Startup.cs”文件：

```csharp
    public class Startup
    {
        // This method gets called by the runtime. Use this method to add services to the container.
        // For more information on how to configure your application, visit https://go.microsoft.com/fwlink/?LinkID=398940
        public void ConfigureServices(IServiceCollection services)
        {
        }

        // This method gets called by the runtime. Use this method to configure the HTTP request pipeline.
        public void Configure(IApplicationBuilder app, IHostingEnvironment env)
        {
            if (env.IsDevelopment())
            {
                app.UseDeveloperExceptionPage();
            }

            app.Run(async (context) =>
            {
                await context.Response.WriteAsync("Hello World!");
            });
        }
    }
```

Startup 类必须始终遵守以下规则：

- 始终为公共
- 包含两个公共方法：`ConfigureServices` 和 `Configure`

`ConfigureServices` 方法定义将在应用中使用的服务。

使用`Configure`[中间件](/aspnet/core/fundamentals/middleware)编写请求管道。 这些组件在 ASP.NET 应用程序管道中使用，用于处理请求和响应。 HTTP 管道由许多请求委托组成，按顺序调用。 每个委托可选择处理请求本身，或将其传递给下一个委托。

可通过在 `IApplicationBuilder` 上使用 `Run`、`Map` 和 `Use` 方法配置委托。但 `Run` 方法不会调用下一个委托，应始终用于管道末尾。

预建模板的 `Configure` 方法有数种作用。 首先，它会配置开发中使用的意外处理页面。 其次，它会向请求网页发送响应，内容为简单的“Hello World”。

不添加任何其他代码也可运行此简单的“Hello, World”项目。 若要运行应用，可以选择要使用 **“播放** ”按钮右下拉来运行应用的应用的浏览器。 或者，可以点击 **“播放** ” (三角) 按钮以使用默认浏览器：

![浏览器运行，可以在其中选择想要使用“播放”按钮右下拉的应用运行应用的浏览器。 或者，可以点击“播放 (三角) 按钮以使用默认浏览器。](media/asp-net-web-picker.png)

Visual Studio for Mac 使用随机端口启动 Web 项目。 要找到该端口，请打开“视图”>“其他窗口”菜单下列出的“应用程序输出”。 应找到如下所示的输出：

![这是显示侦听端口的应用程序输出的插图。](media/asp-net-core-image6.png)

项目运行后，默认 web 浏览器应启动并连接到“应用程序输出”中列出的 URL。 或者，可以打开选择的任何浏览器，输入 `http://localhost:5000/`，将 `5000` 替换为“应用程序输出”中 Visual Studio 输出的端口。 将显示文本 `Hello World!`：

![这是显示文本的浏览器的屏幕截图。](media/asp-net-core-image7.png)

### <a name="adding-a-controller"></a>添加控制器

ASP.NET Core 应用使用模型视图控制器 (MVC) 设计模式，来为应用的每一部分提供职责逻辑分离。 MVC 设计模式包括：

- **模型**：代表应用数据的类。
- **视图**：显示应用的用户界面（通常为模型数据）。
- **控制器**：处理浏览器请求、响应用户输入和交互的类。

有关使用 MVC 的详细信息，请参阅 [ASP.NET Core MVC 概述](/aspnet/core/mvc/overview)指南。

若要添加控制器，请执行以下步骤：

1. 右键单击 **Project** 名称，然后选择“**添加>新建文件**”。 选择“常规”>“空类”，然后输入控制器名称：

    ![这是添加控制器时“新建文件”对话框的屏幕截图。](media/asp-net-core-image8.png)

2. 向新控制器添加以下代码：

    ```csharp
    using System;
    using Microsoft.AspNetCore.Mvc;
    using System.Text.Encodings.Web;

    namespace Hello_ASP
    {
        public class HelloWorldController : Controller
        {
            //
            // GET: /HelloWorld/

            public string Index()
            {
                return "This is my default action...";
            }

        }
    }
    ```

3. 通过右键单击“依赖项”文件夹并选择“添加包...”来添加 `Microsoft.AspNetCore.Mvc` 依赖项 。

4. 使用搜索框浏览 NuGet 库，查找其中的 `Microsoft.AspNetCore.Mvc`，然后选择“添加包”。 安装可能需要几分钟时间，系统可能会提示你接受所需依赖项的各种许可证：

    ![这是添加控制器时添加 Nuget 的屏幕截图。](media/asp-net-core-image9.png)

5. 在 Startup 类中，删除 `app.Run` lambda并设置 URL 路由逻辑，MVC 将用其决定应调用到以下内容的代码：

    ```csharp
    app.UseMvc(routes =>
    {
        routes.MapRoute(
        name: "default",
        template: "{controller=HelloWorld}/{action=Index}/{id?}");
    });
    ```

    请务必删除 `app.Run` lambda，因为这将重写路由逻辑。

    MVC 使用以下格式来决定运行的代码：

    `/[Controller]/[ActionName]/[Parameters]`

    添加上面的代码片段时，你将告诉应用默认为 `HelloWorld` 控制器和 `Index` 操作方法。

6. 添加对方法的`services.AddMvc();``ConfigureServices`调用，如以下代码所示：

    ```csharp
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddMvc();
    }
    ```

    也可将参数信息从 URL 传递到控制器。

7. 将另一种方法添加到 HelloWorldController，如以下代码所示：

    ```csharp
    public string Xamarin(string name)
    {
        return HtmlEncoder.Default.Encode($"Hello {name}, welcome to Visual Studio for Mac");
    }
    ```

8. 如果现在运行应用，它应自动打开浏览器：

    ![添加控制器时在浏览器中运行应用的屏幕截图。](media/asp-net-core-image13.png)

9. 尝试浏览到 `http://localhost:xxxx/HelloWorld/Xamarin?name=Amy` (替换为 `xxxx` 正确的端口) ，应会看到以下页面：

    ![在浏览器中运行应用的屏幕截图，其中包含添加控制器时的参数。](media/asp-net-core-image10.png)

::: moniker-end

::: moniker range="vsmac-2022"
在项目中打开并检查“Program.cs”文件。 请注意，发生了一些情况。 第一个是没有 `Main` 方法。 默认情况下，空模板配置为使用 .NET 6 中引入的最小 Web API 类型项目。

```csharp
var builder = WebApplication.CreateBuilder(args);
var app = builder.Build();

app.MapGet("/", () => "Hello World!");

app.Run();
```

以下代码使用预配置的默认值创建 [WebApplicationBuilder](/dotnet/api/microsoft.aspnetcore.builder.webapplicationbuilder) 和 [WebApplication](/dotnet/api/microsoft.aspnetcore.builder.webapplication) ：

```csharp
var builder = WebApplication.CreateBuilder(args);
var app = builder.Build();
```

以下代码创建和返回的 `Hello World!`HTTP GET 终结点`/`：

```csharp
app.MapGet("/", () => "Hello World!");
```

`app.Run();` 运行应用。

不添加任何其他代码也可运行此简单的“Hello, World”项目。 若要运行应用，可以使用“播放”按钮的下拉列表选择要在其中运行应用的浏览器，或只需点击“播放”（三角形）按钮即可使用默认浏览器：

![浏览器运行](media/asp-net-web-picker.png)

Visual Studio for Mac 使用随机端口启动 Web 项目。 要找到该端口，请打开“视图”>“其他窗口”菜单下列出的“应用程序输出”。 之后应找到类似下图内容的输出：

![显示侦听端口的应用程序输出](media/asp-net-core-image6.png)

项目运行后，默认 web 浏览器应启动并连接到“应用程序输出”中列出的 URL。 或者，可以打开选择的任何浏览器，输入 `http://localhost:5000/`，将 `5000` 替换为“应用程序输出”中 Visual Studio 输出的端口。 将显示文本 `Hello World!`：

![显示文本的浏览器](media/asp-net-core-image7.png)
::: moniker-end

## <a name="troubleshooting"></a>故障排除

如果需要在 macOS 10.12 (Sierra) 及更高版本上手动安装 .NET Core，请执行以下步骤：

1. 在开始安装 .NET Core 之前，请确保已将所有 OS 更新更新更新更新到最新的稳定版本。 可以通过转到App Store应用程序并选择“**更新**”选项卡进行检查。

2. 请遵循 [.NET Core 站点](https://www.microsoft.com/net/core#macos) 上列出的步骤。

请确保成功完成所有步骤，以确保成功安装 .NET Core。

## <a name="summary"></a>总结

本指南介绍了 ASP.NET Core。 介绍了它是什么，何时使用，并提供了在 Visual Studio for Mac 中使用它的信息。
有关后续步骤的详细信息，请参阅以下指南：

- [ASP.NET Core ](/aspnet/core/) 文档。
- [为本机移动应用程序创建后端服务](/aspnet/core/mobile/native-mobile-backend)，该服务演示如何使用 Xamarin.Forms 应用的 ASP.NET Core生成 REST 服务。
- [ASP.NET Core 动手实验](https://github.com/Microsoft/vs4mac-labs/tree/master/Web/Getting-Started)。

## <a name="related-video"></a>相关视频

> [!Video https://docs.microsoft.com/shows/Visual-Studio-Toolbox/Visual-Studio-for-Mac-Build-Your-First-App/player]

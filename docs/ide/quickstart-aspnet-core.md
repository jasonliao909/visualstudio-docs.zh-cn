---
title: 使用 C# 创建 ASP.NET Core Web 应用
description: 了解如何在 Visual Studio 中使用 C# 和 ASP.NET Core 逐步创建简单的 Hello World Web 应用。
ms.custom: vs-acquisition
ms.date: 11/06/2019
ms.topic: quickstart
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.technology: vs-ide-general
dev_langs:
- CSharp
ms.workload:
- aspnet
- dotnetcore
ms.openlocfilehash: 974f6bf70d6866893a61a14f9e2999ba265fb166
ms.sourcegitcommit: 8f8804b885c3a68f20bf0e9fe3729f2764145815
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2021
ms.locfileid: "123097013"
---
# <a name="quickstart-use-visual-studio-to-create-your-first-aspnet-core-web-app"></a>快速入门：使用 Visual Studio 创建首个 ASP.NET Core Web 应用

在这篇关于如何使用 Visual Studio 的 5-10 分钟简介中，将使用 ASP.NET 项目模板和 C# 编程语言创建一个简单的“Hello World”Web 应用。

## <a name="before-you-begin"></a>在开始之前

### <a name="install-visual-studio"></a>安装 Visual Studio

::: moniker range="vs-2017"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)页免费安装。

::: moniker-end

::: moniker range="vs-2019"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页免费安装。

::: moniker-end

::: moniker range="vs-2022"

如果尚未安装 Visual Studio 2022 预览版，请转到 [Visual Studio 2022 预览版下载](https://visualstudio.microsoft.com/vs/preview/vs2022)页免费安装。

::: moniker-end

### <a name="choose-your-theme-optional"></a>选择主题（可选）

本快速入门教程包含使用深色主题的屏幕截图。 如果没有深色主题但想要使用，请参阅[个性化设置 Visual Studio IDE 和编辑器](quickstart-personalize-the-ide.md)页面，了解具体方法。

## <a name="create-a-project"></a>创建项目

首先，将创建 ASP.NET Core web 应用程序项目。 项目类型随附了用于创建 Web 应用的全部模板文件，无需添加任何内容！

::: moniker range="vs-2017"

1. 打开 Visual Studio 2017。

1. 从顶部菜单栏中选择“文件” **“新建”** “项目”>  >  。

1. 在“新建项目”对话框的左侧窗格中，展开“Visual C#”，然后选择“.NET Core”    。 在中间窗格中，选择“ASP.NET Core Web 应用程序”  。 <br/><br/>然后，将文件命名为 `HelloWorld`，并选择“确定”  。

   ![创建面向 C# 的新 ASP.NET Core Web 应用程序项目](../ide/media/csharp-aspnet-choose-template-name-file.png)

   > [!NOTE]
   > 如果没有看到“.NET Core”  项目模板类别，请选择左侧窗格中的“打开 Visual Studio 安装程序”链接  。 （根据你的显示设置，进行滚动以便查看。）
   >
   > ![从“新建项目”对话框中打开 Visual Studio 安装程序](../ide/media/open-visual-studio-installer.png)
   >
   > Visual Studio 安装程序启动。 选择“ASP.NET 和 Web 开发”工作负载，然后选择“修改”   。
   >
   > ![VS 安装程序的 ASP.NET 工作负载](../ide/media/quickstart-aspnet-workload.png)
   >
   > （你可能需要关闭 Visual Studio，然后才能继续安装新的工作负载。）

1. 在“新建 ASP.NET Core Web 应用程序”对话框中，从顶部下拉菜单选择“ASP.NET Core 2.1”   。 接下来，选择“Web 应用程序”，然后选择“确定”   。

   ![“新建 ASP.NET Core Web 应用程序”对话框](../ide/media/aspnet-core-2dot1.png)

   > [!NOTE]
   > 如果没有看到 ASP.NET Core 2.1，请确保你运行的是最新版 Visual Studio  。 要详细了解如何更新安装，请参阅[将 Visual Studio 更新到最新版本](../install/update-visual-studio.md)页面。

不久之后，Visual Studio 将打开你的项目文件。

::: moniker-end

::: moniker range=">=vs-2019"

1. 在“开始”窗口上，选择“创建新项目”。

   :::image type="content" source="../get-started/media/vs-2019/create-new-project-dark-theme.png" alt-text="查看“创建新项目”窗口":::

1. 在“创建新项目”窗口中，从“语言”列表中选择“C#”。 接下来，从“平台”列表中选择“Windows”，然后从“项目类型”列表中选择“Web”。

      应用语言、平台和项目类型筛选器之后，选择“ASP.NET Core Web 应用”模板，然后选择“下一步” 。

   :::image type="content" source="../get-started/csharp/media/vs-2019/csharp-create-new-project-aspnet-core.png" alt-text="为 ASP.NET Core Web 应用选择 C# 模板":::

   > [!NOTE]
   > 如果未看到“ASP.NET Core Web 应用”模板，则可以从“创建新项目”窗口安装该模板。 在“找不到所需内容?”消息中，选择“安装更多工具和功能”链接   。
   >
   > ![“创建新项目”窗口内“找不到所需内容”消息中的“安装更多工具和功能”链接](../get-started/media/vs-2019/not-finding-what-looking-for.png)
   >
   > 然后，在 Visual Studio 安装程序中，选择“ASP.NET 和 Web 开发”工作负载  。
   >
   > ![Visual Studio 安装程序中的 .NET Core 跨平台开发工作负荷](../get-started/media/aspnet-core-web-dev-workload.png)
   >
   > 之后，在 Visual Studio 安装程序中选择“修改”按钮  。 如果系统提示你保存工作，请保存。 接下来，选择“继续”，以安装工作负载  。 然后，返回到“[创建项目](#create-a-project)”过程中的步骤 2。

1. 在“配置新项目”窗口中，在“项目名称”框中键入或输入“HelloWorld”    。 然后，选择“下一步”。

    :::image type="content" source="../get-started/csharp/media/vs-2019/csharp-name-your-aspnet-helloworld-project.png" alt-text="在“配置新项目”窗口中，将项目命名为“MyCoreApp”":::

1. 在“附加信息”窗口中，验证顶部下拉菜单中是否显示“.NET Core 3.1”。 请注意，可以通过选中相应的复选框来启用 Docker 支持。 此外，可以通过单击“更改身份验证”按钮来添加身份验证支持。 可以从中选择下列项目：
    - 无：不进行身份验证。
    - 个人帐户：这些存储在本地或基于 Azure 的数据库。
    - Microsoft 标识平台：此选项使用 Active Directory、Azure AD 或 Microsoft 365 进行身份验证。
    - Windows：适用于 Intranet 应用程序。
    
    保持“启用 Docker”框处于未选中状态，并选择“无”作为身份验证类型。 然后选择“创建”  。

   :::image type="content" source="../get-started/csharp/media/vs-2019/aspnet-core-additional-information.png" alt-text="在“附加信息”窗口中，确保已选择“.NET Core 3.1”并保留所有默认值":::

   Visual Studio 将打开你的新项目。

::: moniker-end

## <a name="create-and-run-the-app"></a>创建并运行应用

::: moniker range="vs-2017"

1. 在“解决方案资源管理器”中，展开“Pages”文件夹，然后选择“About.cshtml”    。

   ![Visual Studio 解决方案资源管理器的屏幕截图，其中显示了 HelloWorld 项目中的文件。 展开了“Pages”文件夹，并选中了“About.cshtml”。](../ide/media/csharp-aspnet-about-page-html-file.png)

   此文件对应于 Web 应用中名为“关于”的页，该页在 Web 浏览器中运行。

   ![Web 应用中的“About”页](../ide/media/csharp-aspnet-about-page.png)

   在编辑器中，你将看到“About”页的“其他信息”区域的 HTML 代码。

   ![Visual Studio 编辑器中“其他信息”区域的 HTML 代码](../ide/media/csharp-aspnet-about-cshtml-page.png)

1. 将“其他信息”文本更改为“Hello World!”。

   ![更改 Visual Studio 编辑器中“其他信息”区域的默认 HTML 代码](../ide/media/csharp-aspnet-about-cshtml-page-hello-world.png)

1. 在“解决方案资源管理器”中，展开“About.cshtml”，然后选择“About.cshtml.cs”。 （此文件也对应于 web 浏览器中的“关于”页。）

   ![Visual Studio 解决方案资源管理器的屏幕截图，其中显示了 HelloWorld 项目中的文件。 展开了“About.cshtml”，并选中了“About.cshtml.cs”。](../ide/media/csharp-aspnet-about-page-code-file.png)

   在编辑器中，你将看到包含“关于”页的“应用程序说明”区域的文本的 C# 代码。

   ![Visual Studio 编辑器中“应用程序说明”区域的 C# 代码](../ide/media/csharp-aspnet-about-cshtml-cs-code.png)

1. 将“应用程序说明”消息文本更改为“我的消息是什么？”。

   ![更改 Visual Studio 编辑器中“应用程序说明”区域的默认消息文本](../ide/media/csharp-aspnet-about-cshtml-cs-message.png)

1. 选择“IIS Express”或按 Ctrl+F5 运行此应用，并在 Web 浏览器中打开它。

   ![在 Visual Studio 中选择“IIS Express”按钮](../ide/media/csharp-aspnet-helloworld-iisbutton.png)

   > [!NOTE]
   > 如果收到错误消息“无法连接到 Web 服务器 "IIS Express"”，或者收到提及 SSL 证书的错误消息，请关闭 Visual Studio。 接下来，右键单击上下文菜单，使用其中的“以管理员身份运行”选项打开 Visual Studio。 然后，再次运行应用。

1. 在 Web 浏览器中，验证“关于”页是否包含更新的文本。

   ![查看更新的“关于”页，其中包含你所做的更改](../ide/media/csharp-aspnet-about-page-hello-world.png)

1. 关闭 Web 浏览器。

### <a name="review-your-work"></a>检查工作

查看以下动画以检查你在上一节中完成的工作。

  ![查看动画 .gif 文件，该文件显示如何在 Visual Studio 中创建和运行简单的 C# ASP.NET Core Web 应用](../ide/media/csharp-aspnet-animated-hello-world.gif)

祝贺你完成此快速入门！ 希望你已对 C#、ASP.NET Core 和 Visual Studio IDE 有了一定了解（集成的开发环境）。

::: moniker-end

::: moniker range=">=vs-2019"

1. 在解决方案资源管理器中，展开“Pages”文件夹，然后选择“Index.cshtml”。

   ![从解决方案资源管理器中选择 Index.cshtml 文件](../ide/media/vs-2019/csharp-aspnet-index-page-cshtml-file.png)

   此文件与 Web 应用中名为“主页”的页面相对应，该页在 Web 浏览器中运行。

   ![Web 应用中的“About”页](../ide/media/vs-2019/csharp-aspnet-index-page.png)

   在编辑器，你将看到主页上显示的文本的 HTML 代码。

   ![Visual Studio 编辑器中主页的 Index.cshtml 文件中的 HTML 代码](../ide/media/vs-2019/csharp-aspnet-index-cshtml-page.png)

1. 更改“欢迎”文本，使其读作“Hello World!”。

   ![在 Visual Studio 编辑器中，更改默认 HTML 代码，使其不显示“欢迎”一词而是显示“Hello World”](../ide/media/vs-2019/csharp-aspnet-index-cshtml-page-hello-world.png)

1. 选择“IIS Express”或按 Ctrl+F5 运行此应用，并在 Web 浏览器中打开它。

   ![在 Visual Studio 中选择“IIS Express”按钮](../ide/media/vs-2019/csharp-aspnet-generic-iisbutton.png)

   > [!NOTE]
   > 如果收到错误消息“无法连接到 Web 服务器 "IIS Express"”，或者收到提及 SSL 证书的错误消息，请关闭 Visual Studio。 接下来，右键单击上下文菜单，使用其中的“以管理员身份运行”选项打开 Visual Studio。 然后，再次运行应用。

1. 在 Web 浏览器中，验证主页是否包含更新后的文本。

   ![查看更新后的主页，其中包含你所做的更改](../ide/media/vs-2019/csharp-aspnet-index-page-hello-world.png)

1. 关闭 Web 浏览器。

::: moniker-end

## <a name="next-steps"></a>后续步骤

要详细了解如何创建 ASP.NET Web 应用，请继续学习以下教程：

> [!div class="nextstepaction"]
> [Visual Studio 中的 C# 和 ASP.NET 入门](../get-started/csharp/tutorial-aspnet-core.md)

或者，了解如何使用 Docker 来容器化 Web 应用：

> [!div class="nextstepaction"]
> [Visual Studio 中的容器工具](../containers/overview.md)

## <a name="see-also"></a>另请参阅

[使用 Visual Studio 将 Web 应用发布到 Azure App Service](../deployment/quickstart-deploy-to-azure.md)

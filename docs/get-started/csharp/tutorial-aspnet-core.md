---
title: 教程：C# 和 ASP.NET Core 入门
titleSuffix: ''
description: 了解如何在 Visual Studio 中使用 C# 逐步创建 ASP.NET Core Web 应用。
ms.custom: vs-acquisition, get-started
ms.date: 09/14/2021
ms.technology: vs-ide-general
ms.prod: visual-studio-windows
ms.topic: tutorial
ms.devlang: CSharp
author: anandmeg
ms.author: meghaanand
manager: jmartens
dev_langs:
- CSharp
ms.workload:
- aspnet
- dotnetcore
ms.openlocfilehash: 53da4978405d17305fa0d5bf730e720eba4bf01b
ms.sourcegitcommit: d38d1b083322019663fec7d1d85a4cda456aadca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/22/2021
ms.locfileid: "135534198"
---
# <a name="tutorial-get-started-with-c-and-aspnet-core-in-visual-studio"></a>教程：Visual Studio 中的 C# 和 ASP.NET Core 入门

在这一使用 Visual Studio 的 C# 开发和 ASP.NET Core 的教程中，你将创建 C# ASP.NET Core Web 应用、对其进行更改、探索 IDE 的一些功能，然后运行该应用。

## <a name="prerequisites"></a>先决条件

1. 安装 Visual Studio
   ::: moniker range="vs-2017"
   
   如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)页免费安装。
   
   ::: moniker-end
   
   ::: moniker range=">=vs-2019"
   
   如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页免费安装。
   
   ::: moniker-end

1. 更新 Visual Studio - 如果已经安装 Visual Studio，请确保运行的是最新版本。 要详细了解如何更新安装，请参阅[将 Visual Studio 更新到最新版本](../../install/update-visual-studio.md)页面。

1. 选择主题（可选）- 本教程包含使用深色主题的屏幕截图。 你可以访问[个性化设置 Visual Studio IDE 和编辑器](../../ide/quickstart-personalize-the-ide.md)页，以了解具体方法。

## <a name="create-a-project"></a>创建项目

首先，你将创建一个 ASP.NET Core项目。 项目类型随附了构建功能完备的网站所需的全部模板文件，无需添加任何内容！

::: moniker range="vs-2017"

1. 打开 Visual Studio 2017。

2. 从顶部菜单栏中选择“文件”>“新建”>“项目”    。

3. 在“新建项目”对话框左侧的窗格中，展开“Visual C#”和“Web”，然后选择“.NET Core”     。 在中间窗格中，选择“ASP.NET Core Web 应用程序”  。 然后，将文件命名为 MyCoreApp 并选择“确定”   。

   ![Visual Studio IDE 中“新建项目”对话框中的 ASP.NET Core Web 应用程序项目模板](media/csharp-aspnet-choose-template-name-razor-mycoreapp-file.png)

### <a name="add-a-workload-optional"></a>添加工作负载（可选）

如果未显示“ASP.NET Core Web 应用程序”  项目模板，可通过添加“ASP.NET 和 Web 开发”  工作负载获取它。 可通过以下两种方式添加此工作负载，具体取决于计算机上安装的 Visual Studio 2017 更新。

#### <a name="option-1-use-the-new-project-dialog-box"></a>选项 1：使用“新建项目”对话框

1. 选择“新建项目”  对话框左窗格中的“打开 Visual Studio 安装程序”  链接。 （根据你的显示设置，进行滚动以便查看。）

   ![选择“新建项目”对话框中的“打开 Visual Studio 安装程序”链接](../media/open-visual-studio-installer-mycoreapp.png)

1. Visual Studio 安装程序启动。 选择“ASP.NET 和 Web 开发”工作负载，然后选择“修改”   。

   ![Visual Studio 安装程序中的 .NET Core 跨平台开发工作负荷](../media/tutorial-aspnet-workload.png)

   （你可能需要关闭 Visual Studio，然后才能继续安装新的工作负载。）

#### <a name="option-2-use-the-tools-menu-bar"></a>选项 2：使用“工具”菜单栏

1. 取消“新建项目”对话框  。 然后，从顶部菜单栏中选择“工具” > “获取工具和功能”   。

1. Visual Studio 安装程序启动。 选择“ASP.NET 和 Web 开发”工作负载，然后选择“修改”   。

   （你可能需要关闭 Visual Studio，然后才能继续安装新的工作负载。）

### <a name="add-a-project-template"></a>添加项目模板

1. 在“新建 ASP.NET Core Web 应用程序”  对话框中，选择“Web 应用程序”  项目模板。

1. 验证顶部下拉菜单中是否显示 ASP.NET Core 2.1  。 然后选择“确定”  。

   ![“新建 ASP.NET Core Web 应用程序”对话框](media/new-project-csharp-aspnet-razor-web-app.png)

   > [!NOTE]
   > 如果没有从顶部下拉菜单中看到“ASP.NET Core 2.1”  ，请确保运行的是最新版本的 Visual Studio。 要详细了解如何更新安装，请参阅[将 Visual Studio 更新到最新版本](../../install/update-visual-studio.md)页面。

::: moniker-end

::: moniker range="vs-2019"

1. 在“开始”窗口上，选择“创建新项目”。

   :::image type="content" source="../../get-started/media/vs-2019/create-new-project-dark-theme.png" alt-text="显示 Visual Studio“开始”窗口的屏幕截图，其中突出显示“创建新项目”选项。":::

1. 在“创建新项目”窗口中，从“语言”列表中选择“C#”。 接下来，从“平台”列表中选择“Windows”，然后从“项目类型”列表中选择“Web”。

      应用语言、平台和项目类型筛选器之后，选择“ASP.NET Core Web 应用”模板，然后选择“下一步” 。

   :::image type="content" source="./media/vs-2019/csharp-create-new-project-aspnet-core.png" alt-text="显示 ASP.NET Core Web 应用项目模板（在“新建项目”对话框中突出显示）的屏幕截图。":::

   > [!NOTE]
   > 如果未看到“ASP.NET Core Web 应用”模板，则可以从“创建新项目”窗口安装该模板。 在“找不到所需内容?”消息中，选择“安装更多工具和功能”链接   。
   >
   > ![显示“找不到要查找的内容”消息中的“安装更多工具和功能”链接的屏幕截图。](../../get-started/media/vs-2019/not-finding-what-looking-for.png)
   >
   > 然后，在 Visual Studio 安装程序中，选择“ASP.NET 和 Web 开发”工作负载  。
   >
   > ![显示 Visual Studio 安装程序中“.NET Core 跨平台开发”工作负载的屏幕截图。](../../get-started/media/aspnet-core-web-dev-workload.png)
   >
   > 之后，在 Visual Studio 安装程序中选择“修改”按钮  。 如果系统提示你保存工作，请保存。 接下来，选择“继续”，以安装工作负载  。 然后，返回到“[创建项目](#create-a-project)”过程中的步骤 2。

1. 在“配置新项目”窗口中，在“项目名称”框中键入或输入“MyCoreApp”    。 然后，选择“下一步”。

   :::image type="content" source="./media/vs-2019/csharp-name-your-aspnet-app.png" alt-text="显示“配置新项目”窗口的屏幕截图，其中“项目名称”字段中输入了“MyCoreApp”。":::

1. 在“附加信息”窗口中，验证顶部下拉菜单中是否显示“.NET Core 3.1”。 请注意，可以通过选中相应的复选框来启用 Docker 支持。 此外，可以通过单击“更改身份验证”按钮来添加身份验证支持。 可以从中选择下列项目：
    - 无：不进行身份验证。
    - 个人帐户：这些存储在本地或基于 Azure 的数据库。
    - Microsoft 标识平台：此选项使用 Active Directory、Azure AD 或 Microsoft 365 进行身份验证。
    - Windows：适用于 Intranet 应用程序。
    
    保持“启用 Docker”框处于未选中状态，并选择“无”作为身份验证类型。 然后选择“创建”  。

   :::image type="content" source="./media/vs-2019/aspnet-core-additional-information.png" alt-text="显示“附加信息”窗口中默认设置的屏幕截图。Framework 值为“.NET Core 3.1”。":::

   Visual Studio 将打开你的新项目。

::: moniker-end

::: moniker range=">=vs-2022"

1. 在“开始”窗口上，选择“创建新项目”。

   :::image type="content" source="media/vs-2022/start-window-create-new-project.png" alt-text="显示 Visual Studio“开始”窗口的屏幕截图，其中突出显示“创建新项目”选项。":::

1. 在“创建新项目”窗口中，从“语言”列表中选择“C#”。 接下来，从“平台”列表中选择“Windows”，然后从“项目类型”列表中选择“Web”。

      应用语言、平台和项目类型筛选器之后，选择“ASP.NET Core Web 应用”模板，然后选择“下一步” 。

   :::image type="content" source="media/vs-2022/csharp-create-new-project-aspnet-core.png" alt-text="显示 ASP.NET Core Web 应用项目模板（在“新建项目”对话框中突出显示）的屏幕截图。":::

   > [!NOTE]
   > 如果未看到“ASP.NET Core Web 应用”模板，则可以从“创建新项目”窗口安装该模板。 在“找不到所需内容?”消息中，选择“安装更多工具和功能”链接   。
   >
   > :::image type="content" source="media/vs-2022/not-finding-what-looking-for.png" alt-text="显示“找不到要查找的内容”消息中的“安装更多工具和功能”链接的屏幕截图。":::
   >
   > 然后，在 Visual Studio 安装程序中，选择“ASP.NET 和 Web 开发”工作负载  。
   >
   > :::image type="content" source="media/vs-2022/aspnet-core-web-dev-workload.png" alt-text="显示 Visual Studio 安装程序中的 ASP.NET 和 Web 开发工作负载的屏幕截图。":::
   >
   > 之后，在 Visual Studio 安装程序中选择“修改”按钮  。 如果系统提示你保存工作，请保存。 接下来，选择“继续”，以安装工作负载  。 然后，返回到“[创建项目](#create-a-project)”过程中的步骤 2。

1. 在“配置新项目”窗口中，在“项目名称”框中键入或输入“MyCoreApp”    。 然后，选择“下一步”。

   :::image type="content" source="media/vs-2022/csharp-name-your-aspnet-app.png" alt-text="显示“配置新项目”窗口的屏幕截图，其中“项目名称”字段中输入了“MyCoreApp”。":::

1. 在“附加信息”窗口中，验证“框架”字段中显示了“.NET 6.0”。   在此窗口中，可以通过选中相应的复选框来启用 Docker 支持。 还可以通过从“身份验证类型”下拉列表中选择一个值来添加身份验证支持。 可以从中选择下列项目：

    - 无：不进行身份验证。
    - 个人帐户：存储在本地或基于 Azure 的数据库中的身份验证。
    - Microsoft 标识平台：此选项使用 Active Directory、Azure AD 或 Microsoft 365 进行身份验证。
    - Windows：适用于 Intranet 应用程序。
    
    将“启用 Docker”框保持未选中状态，并选择“无”作为身份验证类型 。 然后选择“创建”。

   :::image type="content" source="media/vs-2022/aspnet-core-additional-information.png" alt-text="显示“附加信息”窗口中默认设置的屏幕截图。Framework 值为“.NET 6.0”。":::

   Visual Studio 将打开你的新项目。

::: moniker-end

### <a name="about-your-solution"></a>关于解决方案

此解决方案遵循 Razor 页面  设计模式。 它与 [Model-View-Controller (MVC)](/aspnet/core/tutorials/first-mvc-app/start-mvc?view=aspnetcore-2.1&tabs=aspnetcore2x&preserve-view=true) 设计模式的不同之处在于，它进行了优化，以包含 Razor Page 本身的模型和控制器代码。

::: moniker range="vs-2017"
## <a name="tour-your-solution"></a>浏览解决方案

 1. 项目模板会创建一个解决方案，其中包含一个名为 MyCoreApp  的 ASP.NET Core 项目。 选择“解决方案资源管理器”  选项卡以查看其内容。

    ![Visual Studio 中适用于 Razor 页面解决方案的名为 MyCoreApp 的 ASP.NET 解决方案资源管理器](media/csharp-aspnet-razor-solution-explorer-mycoreapp.png)

 1. 展开“页面”  文件夹，然后展开“About.cshtml”  。

     ![Visual Studio 解决方案资源管理器中的 About.cshtml 文件](media/csharp-aspnet-razor-solution-explorer-aboutcshtml.png)

 1. 查看代码编辑器中的“About.cshtml”  文件。

     ![显示 Visual Studio 代码编辑器中 About.cshtml 文件的前 10 行的屏幕截图。](media/csharp-aspnet-razor-aboutcshtml-mycoreapp-code.png)

 1. 选择“About.cshtml.cs”  文件。

     ![选择 Visual Studio 代码编辑器中的 About.cshtml.cs 文件](media/csharp-aspnet-razor-solution-explorer-aboutcshtmlcs.png)

 1. 查看代码编辑器中的“About.cshtml.cs”  文件。

     ![显示 Visual Studio 代码编辑器中 About.cshtml.cs 文件的前 18 行的屏幕截图。 ](media/csharp-aspnet-razor-aboutcshtmlcs-mycoreapp-code.png)

 1. 该项目包含一个 wwwroot  文件夹，它是网站的根。 展开文件夹以查看其内容。

     ![Visual Studio 解决方案资源管理器中的 wwwroot 文件夹](media/csharp-aspnet-razor-solution-explorer-wwwroot.png)

    可将静态站点内容&mdash;如 CSS、图像和 JavaScript 库&mdash;直接放在所需的路径中。

 1. 该项目还包含在运行时管理 Web 应用的配置文件。 默认应用程序[配置](/aspnet/core/fundamentals/configuration)存储在 appsettings.json  中。 但是，可使用 appsettings.Development.json 替代这些设置  。 展开 appsettings.json 文件以查看 appsettings.Development.json 文件   。

     ![Visual Studio 解决方案资源管理器中的配置文件](media/csharp-aspnet-razor-solution-explorer-appsettingsjson.png)

## <a name="run-debug-and-make-changes"></a>运行、调试和更改

1. 在 IDE 中选择“IIS Express”  按钮，在调试模式下生成并运行应用。 （或者，按 F5  或从菜单栏选择“调试”   > “启动调试”  。）

     ![在 Visual Studio 中选择“IIS Express”按钮](media/csharp-aspnet-razor-iisexpress.png)

     > [!NOTE]
     > 如果看到内容为“无法连接到 Web 服务器‘IIS Express’”  的错误消息，请关闭 Visual Studio，再使用右键单击菜单或上下文菜单中的“以管理员身份运行”  选项打开它。 然后，再次运行应用。
     >
     > 系统可能会向你发送一条消息，询问你是否接受 IIS SSL Express 证书。 要在 Web 浏览器中查看代码，请选择“是”，如果收到后续的安全警告消息，也请选择“是”   。

1. Visual Studio 启动浏览器窗口。 然后，应在菜单栏中看到“主页”  、“关于”  和“联系人”  页面。 （如果没有看到该页面，请选择“汉堡”菜单项来查看它们。）

    ![从 Web 应用中的菜单栏中选择“汉堡”菜单项](media/csharp-aspnet-razor-browser-page.png)

1. 选择菜单栏中的“关于”  。

   ![在应用的浏览器窗口的菜单栏中选择“关于”](media/csharp-aspnet-razor-browser-page-about-menu.png)

   此外，浏览器中的“关于”  页呈现 About.cshtml  文件中设置的文本。

   ![查看“关于”页面上的文本](media/csharp-aspnet-razor-browser-page-about.png)

1. 返回到 Visual Studio，然后按 Shift+F5  停止调试模式。 这还会关闭浏览器窗口中的项目。

1. 在 Visual Studio 中，选择“About.cshtml”  。 然后，删除“another”一词并在该位置添加词文件和目录。

    ![更改 About.cshtml 文件中的文本](media/csharp-aspnet-razor-aboutcshtml-mycoreapp-code-changed.png)

1. 选择“About.cshtml.cs”  。 然后，使用以下快捷方式清理文件顶部的 `using` 指令：

   选择任何灰色的 `using` 指令，插入点下方或左边距会显示[快速操作](../../ide/quick-actions.md)灯泡。 选择此灯泡，然后选择“删除不必要的 Using”  。

   ![删除 About.cshtml.cs 文件中不必要的 Using](media/csharp-aspnet-razor-remove-unnecessary-usings.png)

     Visual Studio 从文件中删除不必要的 `using` 指令。

1. 接下来，在 `OnGet()` 方法中，将主体更改为以下代码：

     ```csharp
     public void OnGet()
     {
         string directory = Environment.CurrentDirectory;
         Message = String.Format("Your directory is {0}.", directory);
     }
    ```

1. 请注意在环境  和字符串  下显示的两个波浪下划线。 显示波浪下划线是因为这些类型不在作用域内。

   ![OnGet 方法中使用波浪下划线标记的错误](media/csharp-aspnet-razor-add-new-on-get-method.png)

    打开“错误列表”工具栏，查看此处列出的相同错误  。 （如果没有看到“错误列表”  工具栏，请选择顶部菜单栏中的“视图”   > “错误列表”  。）

   ![Visual Studio 中的错误列表](media/csharp-aspnet-razor-error-list.png)

1. 让我们来解决此问题。 在代码编辑器中，将光标放在包含错误的任意一条线上，然后选择左边距中的“快速操作”灯泡。 然后，从下拉菜单中，选择“使用系统”  将此指令添加到文件顶部并解析错误。

   ![添加“使用系统”指令](media/csharp-aspnet-razor-add-usings.png)

1. 按 Ctrl  +S  保存所做的更改，然后按 F5  在 Web 浏览器中打开项目。

1. 在网站顶部，选择“关于”  查看你的更改。

   ![查看更新的“关于”页，其中包含你所做的更改](media/csharp-aspnet-razor-browser-page-about-changed.png)

1. 关闭 Web 浏览器，按 Shift  +F5  停止调试模式，然后关闭 Visual Studio。

::: moniker-end

::: moniker range="=vs-2019"

## <a name="tour-your-solution"></a>浏览解决方案

 1. 项目模板会创建一个解决方案，其中包含一个名为 MyCoreApp  的 ASP.NET Core 项目。 选择“解决方案资源管理器”  选项卡以查看其内容。

    ![Visual Studio 中解决方案资源管理器的屏幕截图，显示了名为"MyCoreApp"的 ASP.NET Core 项目的内容。](media/csharp-aspnet-razor-solution-explorer-mycoreapp.png)

 1. 展开“页面”文件夹  。

     ![Visual Studio 中解决方案资源管理器的屏幕截图，显示了“MyCoreApp”的“Pages”文件夹的内容。](media/vs-2019/csharp-aspnet-solution-explorer-pages.png)

 1. 查看代码编辑器中的“Index.cshtml”文件  。

     ![显示 Visual Studio 代码编辑器中打开的 Index.cshtml 文件的屏幕截图。](media/vs-2019/csharp-aspnet-index-cshtml.png)

 1. 每个 .cshtml 文件都具有关联的代码文件。 若要在编辑器中打开代码文件，请在解决方案资源管理器中展开“Index.cshtml”节点，并选择“Index.cshtml.cs”文件   。

     ![Visual Studio 中解决方案资源管理器的屏幕截图，其中显示已选中 Index.cshtml.cs 文件。](media/vs-2019/csharp-aspnet-choose-index-cshtml.png)

 1. 查看代码编辑器中的“Index.cshtml.cs”文件  。

     ![显示 Visual Studio 代码编辑器中打开的 Index.cshtml.cs 文件的屏幕截图。](media/vs-2019/csharp-aspnet-index-cshtml-editing.png)

 1. 该项目包含一个 wwwroot  文件夹，它是网站的根。 展开文件夹以查看其内容。

     ![Visual Studio 中解决方案资源管理器的屏幕截图，显示了“wwwroot”文件夹的内容。](media/csharp-aspnet-razor-solution-explorer-wwwroot.png)

    可将静态站点内容&mdash;如 CSS、图像和 JavaScript 库&mdash;直接放在所需的路径中。

 1. 该项目还包含在运行时管理 Web 应用的配置文件。 默认应用程序[配置](/aspnet/core/fundamentals/configuration)存储在 appsettings.json  中。 但是，可使用 appsettings.Development.json 替代这些设置  。 展开 appsettings.json 文件以查看 appsettings.Development.json 文件   。

     ![Visual Studio 中解决方案资源管理器的屏幕截图，显示已选中 appsettings.json 文件，展开后显示 appsettings.Development.json 文件。](media/csharp-aspnet-razor-solution-explorer-appsettingsjson.png)

## <a name="run-debug-and-make-changes"></a>运行、调试和更改

1. 在 IDE 中选择“IIS Express”  按钮，在调试模式下生成并运行应用。 （或者，按 F5  或从菜单栏选择“调试”   > “启动调试”  。）

     ![显示 Visual Studio IDE 中突出显示的 IIS Express 按钮的屏幕截图。](media/csharp-aspnet-razor-iisexpress.png)

     > [!NOTE]
     > 如果看到内容为“无法连接到 Web 服务器‘IIS Express’”  的错误消息，请关闭 Visual Studio，再使用右键单击菜单或上下文菜单中的“以管理员身份运行”  选项打开它。 然后，再次运行应用。
     >
     > 系统可能会向你发送一条消息，询问你是否接受 IIS SSL Express 证书。 要在 Web 浏览器中查看代码，请选择“是”，如果收到后续的安全警告消息，也请选择“是”   。

1. Visual Studio 启动浏览器窗口。 然后，应在菜单栏中看到“主页”和“隐私”页面   。

1. 选择菜单栏中的“隐私”  。

   浏览器中的“隐私”页呈现 Privacy.cshtml 文件中设置的文本   。

   ![显示“MyCoreApp 隐私”页的屏幕截图，其中包含文本“使用此页详细说明网站的隐私策略”。](media/vs-2019/csharp-aspnet-browser-page-privacy.png)

1. 返回到 Visual Studio，然后按 Shift+F5  停止调试模式。 这还会关闭浏览器窗口中的项目。

1. 在 Visual Studio 中，打开要编辑的“Privacy.cshtml”  。 然后，删除“使用此页面详细说明网站的隐私策略”字词，并在其位置添加“此页面自 @ViewData["TimeStamp"] 起构建”字词   。

    ![显示 Visual Studio 代码编辑器中打开的 Privacy.cshtml 文件的屏幕截图，其中包含更新后的文本。](media/vs-2019/csharp-aspnet-privacy-cshtml-code-changed.png)

1. 现在，让我们对代码进行更改。 选择“Privacy.cshtml.cs”  。 然后，使用以下快捷方式清理文件顶部的 `using` 指令：

   选择任何灰色的 `using` 指令，插入点下方或左边距会显示[快速操作](../../ide/quick-actions.md)灯泡。 选择灯泡，然后将鼠标悬停在“删除不必要的 using”  。

   ![屏幕截图显示了 Visual Studio 代码编辑器中的 Privacy.cshtml 文件，其中打开了“删除不必要的 Using”对话框。](media/vs-2019/csharp-aspnet-remove-unnecessary-usings.png)

   现选择“预览更改”，查看更改的内容  。

   ![显示“预览更改”对话框的屏幕截图，其中显示了“Using”的新列表和 Privacy.cshtm 文件中的代码。](media/vs-2019/csharp-aspnet-preview-changes.png)

   选择“应用”。  Visual Studio 从文件中删除不必要的 `using` 指令。

1. 接下来，在 `OnGet()` 方法中，将主体更改为以下代码：

     ```csharp
     public void OnGet()
     {
        string dateTime = DateTime.Now.ToShortDateString();
        ViewData["TimeStamp"] = dateTime;
     }
    ```

1. 请注意在“DateTime”下显示的两个波浪下划线  。 显示波浪下划线是因为此类型不在范围内。

   ![显示 OnGet 方法中用波浪下划线标记的错误的屏幕截图。](media/vs-2019/csharp-aspnet-add-new-onget-method.png)

    打开“错误列表”工具栏，查看此处列出的相同错误  。 （如果没有看到“错误列表”  工具栏，请选择顶部菜单栏中的“视图”   > “错误列表”  。）

   ![Visual Studio 中的错误列表](media/vs-2019/csharp-aspnet-error-list.png)

1. 让我们来解决此问题。 在代码编辑器中，将光标放在包含错误的任意一条线上，然后选择左边距中的“快速操作”灯泡。 然后，从下拉菜单中，选择“使用系统”  将此指令添加到文件顶部并解析错误。

   ![显示“快速操作”菜单的屏幕截图，其中显示了添加“using System”指令的建议。](media/vs-2019/csharp-aspnet-add-usings.png)

1. 按 F5，即可在 Web 浏览器中打开项目  。

1. 在网站顶部，选择“隐私”查看你的更改  。

   ![显示更新的“隐私”页的屏幕截图，其中包含你所做的更改。](media/vs-2019/csharp-aspnet-browser-page-privacy-changed.png)

1. 关闭 Web 浏览器，按 Shift  +F5  停止调试模式，然后关闭 Visual Studio。
::: moniker-end

::: moniker range=">=vs-2022"

## <a name="tour-your-solution"></a>浏览解决方案

 1. 项目模板会创建一个解决方案，其中包含一个名为 MyCoreApp  的 ASP.NET Core 项目。 选择“解决方案资源管理器”  选项卡以查看其内容。

     :::image type="content" source="media/vs-2022/csharp-aspnet-razor-solution-explorer-mycoreapp.png" alt-text="Visual Studio 中解决方案资源管理器的屏幕截图，显示了名为&quot;MyCoreApp&quot;的 ASP.NET Core 项目的内容。":::

 1. 展开“页面”文件夹  。

     :::image type="content" source="media/vs-2022/csharp-aspnet-solution-explorer-pages.png" alt-text="Visual Studio 中解决方案资源管理器的屏幕截图，显示了“MyCoreApp”的“Pages”文件夹的内容。":::

 1. 查看代码编辑器中的“Index.cshtml”文件  。

     :::image type="content" source="media/vs-2022/csharp-aspnet-index-cshtml.png" alt-text="显示 Visual Studio 代码编辑器中打开的 Index.cshtml 文件的屏幕截图。":::

 1. 每个 .cshtml 文件都具有关联的代码文件。 若要在编辑器中打开代码文件，请在解决方案资源管理器中展开“Index.cshtml”节点，并选择“Index.cshtml.cs”文件   。

     :::image type="content" source="media/vs-2022/csharp-aspnet-choose-index-cshtml.png" alt-text="Visual Studio 中解决方案资源管理器的屏幕截图，其中显示已选中 Index.cshtml.cs 文件。":::

 1. 查看代码编辑器中的“Index.cshtml.cs”文件  。

     :::image type="content" source="media/vs-2022/csharp-aspnet-index-cshtml-editing.png" alt-text="显示 Visual Studio 代码编辑器中打开的 Index.cshtml.cs 文件的屏幕截图。":::

 1. 该项目包含一个 wwwroot  文件夹，它是网站的根。 展开文件夹以查看其内容。

     :::image type="content" source="media/vs-2022/csharp-aspnet-razor-solution-explorer-wwwroot.png" alt-text="Visual Studio 中解决方案资源管理器的屏幕截图，显示了“wwwroot”文件夹的内容。":::

    可将静态站点内容&mdash;如 CSS、图像和 JavaScript 库&mdash;直接放在所需的路径中。

 1. 该项目还包含在运行时管理 Web 应用的配置文件。 默认应用程序[配置](/aspnet/core/fundamentals/configuration)存储在 appsettings.json  中。 但是，可使用 appsettings.Development.json 替代这些设置  。 展开 appsettings.json 文件以查看 appsettings.Development.json 文件   。

     :::image type="content" source="media/vs-2022/csharp-aspnet-razor-solution-explorer-appsettingsjson.png" alt-text="Visual Studio 中解决方案资源管理器的屏幕截图，显示已选中 appsettings.json 文件，展开后显示 appsettings.Development.json 文件。":::

## <a name="run-debug-and-make-changes"></a>运行、调试和更改

1. 在 IDE 中选择“IIS Express”按钮，在调试模式下生成并运行应用。 （或者，按 F5  或从菜单栏选择“调试”   > “启动调试”  。）

     :::image type="content" source="media/vs-2022/csharp-aspnet-razor-iisexpress.png" alt-text="显示 Visual Studio IDE 中突出显示的 IIS Express 按钮的屏幕截图。":::

     > [!NOTE]
     > 如果看到内容为“无法连接到 Web 服务器‘IIS Express’”  的错误消息，请关闭 Visual Studio，再使用右键单击菜单或上下文菜单中的“以管理员身份运行”  选项打开它。 然后，再次运行应用。
     >
     > 系统可能会向你发送一条消息，询问你是否接受 IIS SSL Express 证书。 要在 Web 浏览器中查看代码，请选择“是”，如果收到后续的安全警告消息，也请选择“是”   。

1. Visual Studio 启动浏览器窗口。 然后，应在菜单栏中看到“主页”和“隐私”页面   。

1. 选择菜单栏中的“隐私”  。

   浏览器中的“隐私”页呈现 Privacy.cshtml 文件中设置的文本   。

   :::image type="content" source="media/vs-2022/csharp-aspnet-browser-page-privacy.png" alt-text="显示“MyCoreApp 隐私”页的屏幕截图，其中包含文本“使用此页详细说明网站的隐私策略”。":::

1. 返回到 Visual Studio，然后按 Shift+F5  停止调试模式。 这还会关闭浏览器窗口中的项目。

1. 在 Visual Studio 中，打开要编辑的“Privacy.cshtml”  。 然后，删除“使用此页面详细说明网站的隐私策略”字词，并在其位置添加“此页面自 @ViewData["TimeStamp"] 起构建”字词   。

   :::image type="content" source="media/vs-2022/csharp-aspnet-privacy-cshtml-code-changed.png" alt-text="显示 Visual Studio 代码编辑器中打开的 Privacy.cshtml 文件的屏幕截图，其中包含更新后的文本。":::

1. 现在，让我们对代码进行更改。 选择“Privacy.cshtml.cs”  。 然后，选择以下快捷方式清理文件顶部的 `using` 指令：

   选择任何灰色的 `using` 指令，插入点下方或左边距会显示[快速操作](../../ide/quick-actions.md)灯泡。 选择灯泡，然后将鼠标悬停在“删除不必要的 using”  。

   :::image type="content" source="media/vs-2022/csharp-aspnet-remove-unnecessary-usings.png" alt-text="屏幕截图显示了 Visual Studio 代码编辑器中的 Privacy.cshtml 文件，其中打开了“删除不必要的 Using”对话框。":::

   现选择“预览更改”，查看更改的内容  。

   :::image type="content" source="media/vs-2022/csharp-aspnet-preview-changes.png" alt-text="显示“预览更改”对话框的屏幕截图，其中显示了“Using”的新列表和 Privacy.cshtm 文件中的代码。":::

   选择“应用”。  Visual Studio 从文件中删除不必要的 `using` 指令。

1. 接下来，使用 [DateTime.ToString](xref:System.DateTime.ToString%2A) 方法为针对区域性或区域设置格式的当前日期创建字符串。

   - 方法的第一个参数指定如何显示日期。 此示例使用格式说明符 (`d`) 指示短日期格式。 
   - 第二个参数是 [CultureInfo](/dotnet/api/system.globalization.cultureinfo) 对象，该对象指定日期的区域性或区域。 此参数确定日期中任意单词的语言以及所使用的分隔符类型等。
 
将 `OnGet()` 方法的主体更改为以下代码：

   ```csharp
   public void OnGet()
   {
      string dateTime = DateTime.Now.ToString("d", new CultureInfo("en-US"));
      ViewData["TimeStamp"] = dateTime;
   }
   ```

1. 请注意在“CultureInfo”下显示的两个波浪下划线。 显示波浪下划线是因为此类型不在范围内。

   :::image type="content" source="media/vs-2022/csharp-aspnet-add-new-onget-method.png" alt-text="显示代码编辑器中 OnGet 方法的屏幕截图，其中 CultureInfo 对象下方有波浪下划线。":::

    打开“错误列表”工具栏，查看此处列出的相同错误  。 （如果没有看到“错误列表”  工具栏，请选择顶部菜单栏中的“视图”   > “错误列表”  。）

   :::image type="content" source="media/vs-2022/csharp-aspnet-error-list.png" alt-text="显示 Visual Studio 中的“错误列表”窗口的屏幕截图。“CultureInfo”类型缺少一个 using 指令。":::

1. 让我们来解决此问题。 在代码编辑器中，将光标放在包含错误的任意一条线上，然后选择左边距中的“快速操作”灯泡。 然后，从下拉菜单中，选择“using System.Globalization;”，将此指令添加到文件顶部并解析错误。

   :::image type="content" source="media/vs-2022/csharp-aspnet-add-usings.png" alt-text="显示“快速操作”菜单的屏幕截图，其中显示了添加“using System.Globalization”指令的建议。":::

1. 按 F5，即可在 Web 浏览器中打开项目  。

1. 在网站顶部，选择“隐私”查看你的更改  。

   :::image type="content" source="media/vs-2022/csharp-aspnet-browser-page-privacy-changed.png" alt-text="显示 MyCoreApp 的“隐私”页的屏幕截图，其中包括添加日期所做的更改。":::

1. 关闭 Web 浏览器，按 Shift  +F5  停止调试模式，然后关闭 Visual Studio。

::: moniker-end

## <a name="quick-answers-faq"></a>快速解答常见问题

下面是一个快速 FAQ，突出介绍了一些关键概念。

### <a name="what-is-c"></a>什么是 C#？

[C#](/dotnet/csharp/tour-of-csharp/) 是一种类型安全且面向对象的编程语言，其可靠且易于学习。

### <a name="what-is-aspnet-core"></a>什么是 ASP.NET Core？

ASP.NET Core 是开放源跨平台框架，用于生成基于 Internet 连接的应用程序，例如 Web 应用和服务。 ASP.NET Core 应用可以在 .NET Core 或 .NET Framework 上运行。 可以在 Windows、Mac 和 Linux 上跨平台开发和运行 ASP.NET Core 应用。 ASP.NET Core 在 [GitHub](https://github.com/aspnet/home) 为开放源。

### <a name="what-is-visual-studio"></a>什么是 Visual Studio？

Visual Studio 是适用于开发人员的生产力工具集成开发套件。 可将其视为可用于创建程序和应用程序的程序。

## <a name="next-steps"></a>后续步骤

恭喜你完成本教程！ 希望你已对 C#、ASP.NET Core 和 Visual Studio IDE 有了一定了解。 要详细了解如何使用 C# 和 ASP.NET 创建 Web 应用或网站，请继续学习以下教程：

> [!div class="nextstepaction"]
> [使用 ASP.NET Core 创建 Razor 页面 Web 应用](/aspnet/core/tutorials/razor-pages/?view=aspnetcore-2.1&preserve-view=true)

或者，了解如何使用 Docker 容器化 Web 应用：

> [!div class="nextstepaction"]
> [Visual Studio 中的容器工具](../../containers/overview.md)

## <a name="see-also"></a>另请参阅

[使用 Visual Studio 将 Web 应用发布到 Azure App Service](../../deployment/quickstart-deploy-aspnet-web-app.md)

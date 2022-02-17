---
title: '教程：在 Visual Studio 中创建 c # ASP.NET Core web 应用'
description: '在本教程中，使用 c # 和 ASP.NET Core 在 Visual Studio 中创建 web 应用。'
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.technology: vs-ide-general
ms.topic: tutorial
ms.date: 02/16/2022
ms.prod: visual-studio-windows
ms.workload:
- aspnet
- dotnetcore
dev_langs:
- CSharp
ms.devlang: CSharp
ms.custom: vs-acquistion, get-started
ms.openlocfilehash: ca5e7cc7aa2e1bd539eb7e2cec84b4969f1ad273
ms.sourcegitcommit: 663f5cea9bf1481ce276764c74711baedeefb552
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/17/2022
ms.locfileid: "139039428"
---
# <a name="tutorial-get-started-with-c-and-aspnet-core-in-visual-studio"></a>教程：Visual Studio 中的 C# 和 ASP.NET Core 入门

在本教程中，对于使用 ASP.NET Core 进行 c # 开发，你将在 Visual Studio 中创建一个 c # ASP.NET Core web 应用。

本教程会说明如何：

> [!div class="checklist"]
>
> - 创建 Visual Studio 项目
> - 创建 c # ASP.NET Core web 应用
> - 对 web 应用进行更改
> - 浏览 IDE 功能
> - 运行 Web 应用

## <a name="prerequisites"></a>先决条件

   ::: moniker range="vs-2017"

   若要完成本教程，必须具有 Visual Studio。 请访问 [Visual Studio 下载页](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)获取免费版本。

   ::: moniker-end

   ::: moniker range=">=vs-2019"

   若要完成本教程，必须具有 Visual Studio。
   请访问 [Visual Studio 下载页](https://visualstudio.microsoft.com/vs)获取免费版本。

   ::: moniker-end

- 有关升级到最新 Visual Studio 版本的详细信息，请参阅[Visual Studio 更新](../../install/update-visual-studio.md)。

- 若要自定义 Visual Studio 体验，请参阅[个性化 Visual Studio IDE 和编辑器](../../ide/quickstart-personalize-the-ide.md)。

## <a name="create-a-project"></a>创建一个项目

首先，您将创建一个 ASP.NET Core 项目。 项目类型附带了生成功能完备的网站所需的所有模板文件。

::: moniker range="vs-2017"

1. 打开 Visual Studio 2017。

2. 在顶部菜单栏中，选择 "**文件** > " "**新建** > **Project**"。

3. 在左侧窗格的 "**新建 Project** " 对话框中，展开 " **Visual c #**"，展开 " **Web** 节点"，然后选择 " **.net Core**"。 在中间窗格中，选择“ASP.NET Core Web 应用程序”。 接下来，将该文件命名为 **MyCoreApp** ，然后选择 **"确定"**。

   ![Visual Studio IDE 中 "新建 Project" 对话框中 ASP.NET Core Web 应用程序项目模板。](media/csharp-aspnet-choose-template-name-razor-mycoreapp-file.png)

### <a name="add-a-workload-optional"></a>添加工作负载（可选）

如果未显示“ASP.NET Core Web 应用程序”  项目模板，可通过添加“ASP.NET 和 Web 开发”  工作负载获取它。 可通过以下两种方式添加此工作负载，具体取决于计算机上安装的 Visual Studio 2017 更新。

#### <a name="option-1-use-the-new-project-dialog-box"></a>选项 1：使用“新建项目”对话框

1. 选择“新建项目”  对话框左窗格中的“打开 Visual Studio 安装程序”  链接。 根据您的显示设置，您可能需要滚动才能看到它。

   ![从 "新建 Project" 对话框中选择 "打开 Visual Studio 安装程序" 链接。](../media/open-visual-studio-installer-mycoreapp.png)

1. 在 Visual Studio 安装程序启动后，选择 " **ASP.NET 和 web 开发**" 工作负载，然后选择 "**修改**"。 安装所选工作负荷时，Visual Studio 可能必须关闭。

   ![Visual Studio 安装程序中的 .net Core 跨平台开发工作负荷。](../media/tutorial-aspnet-workload.png)

#### <a name="option-2-use-the-tools-menu-bar"></a>选项 2：使用“工具”菜单栏

1. 取消“新建项目”对话框  。 然后，在顶部菜单栏中选择 "**工具**  >  " "**获取工具和功能**"。

1. Visual Studio 安装程序启动后，选择 " **ASP.NET 和 web 开发**" 工作负载，然后选择 "**修改**"。 安装所选工作负荷时，Visual Studio 可能必须关闭。

### <a name="add-a-project-template"></a>添加项目模板

1. 在 "**新建 ASP.NET Core web 应用程序**" 对话框中，选择 " **web 应用程序**" 项目模板。

1. 验证顶部下拉菜单中是否显示 ASP.NET Core 2.1  。 选择“确定”。 

   !["新建 ASP.NET Core Web 应用程序" 对话框。](media/new-project-csharp-aspnet-razor-web-app.png)

   > [!NOTE]
   > 如果没有从顶部下拉菜单中看到“ASP.NET Core 2.1”  ，请确保运行的是最新版本的 Visual Studio。 有关如何更新安装的详细信息，请参阅[更新 Visual Studio 到最新版本。](../../install/update-visual-studio.md) 页面。

::: moniker-end

::: moniker range="vs-2019"

1. 在“开始”窗口中，选择“创建新项目”。

   :::image type="content" source="../../get-started/media/vs-2019/create-new-project-dark-theme.png" alt-text="屏幕截图显示 Visual Studio 的开始窗口。突出显示 &quot;新建项目&quot; 选项。":::

1. 在 "新建 **项目** " 窗口的 "语言" 列表中，选择 " **c #** "。 接下来，从平台列表中选择 " **Windows** "，然后从 "项目类型" 列表中选择 " **Web** "。

      应用语言、平台和项目类型筛选器后，请选择 " **ASP.NET Core Web 应用**" 模板，然后选择 "**下一步**"。

   :::image type="content" source="./media/vs-2019/csharp-create-new-project-aspnet-core.png" alt-text="屏幕截图显示在 &quot;新建 Project&quot; 对话框中突出显示的 &quot;ASP.NET Core Web 应用程序&quot; 项目模板。":::

   > [!NOTE]
   > 如果未看到“ASP.NET Core Web 应用”模板，则可以从“创建新项目”窗口安装该模板。 在 " **找不到你要查找的内容"** 消息中，选择 " **安装更多工具和功能** " 链接。
   >
   > ![屏幕截图显示了 "安装更多工具和功能" 链接，它是未找到你要查找的消息的一部分。](../../get-started/media/vs-2019/not-finding-what-looking-for.png)
   >
   > 接下来，在 "Visual Studio 安装程序中，选择" **ASP.NET "和" web 开发**"。
   >
   > ![屏幕截图显示了 Visual Studio 安装程序中的 .net Core 跨平台开发工作负荷。](../../get-started/media/aspnet-core-web-dev-workload.png)
   >
   > 在 Visual Studio 安装程序中，选择“修改”。 系统可能会提示你保存工作内容。 接下来，选择“继续”以安装工作负载。

1. 在 "**配置新项目**" 窗口中，在 " **Project 名称**" 字段中输入 " **MyCoreApp** "。 然后，选择“下一步”。

   :::image type="content" source="./media/vs-2019/csharp-name-your-aspnet-app.png" alt-text="屏幕截图显示 &quot;配置新项目&quot; 窗口，并在 &quot;Project 名称&quot; 字段中输入 MyCoreApp。":::

1. 在 "**附加信息**" 窗口中，验证 "**目标框架**" 字段中是否显示了 " **.net Core 3.1** "。 在此窗口中，可以启用 Docker 支持并添加身份验证支持。 **身份验证类型** 的下拉菜单具有以下四个选项：
    - **无**。 无身份验证。
    - **个人帐户**。 这些身份验证存储在本地或基于 Azure 的数据库中。
    - **Microsoft 标识平台**。 此选项使用 Active Directory、Azure AD 或 Microsoft 365 进行身份验证。
    - **Windows**。 适用于 Intranet 应用程序。

    保持“启用 Docker”框处于未选中状态，并选择“无”作为身份验证类型。 接下来，选择“创建”。 

   :::image type="content" source="./media/vs-2019/aspnet-core-additional-information.png" alt-text="屏幕截图显示 &quot;其他信息&quot; 窗口中的默认设置。框架值为 .NET Core 3.1。":::

   Visual Studio 将打开你的新项目。

::: moniker-end

::: moniker range=">=vs-2022"

1. 在“开始”窗口中，选择“创建新项目”。

   :::image type="content" source="media/vs-2022/start-window-create-new-project.png" border="false" alt-text="屏幕截图显示 Visual Studio 的开始窗口。突出显示 &quot;新建项目&quot; 选项。":::

1. 在 "新建 **项目** " 窗口的 "语言" 列表中，选择 " **c #** "。 接下来，从平台列表中选择 " **Windows** "，然后从 "项目类型" 列表中选择 " **Web** "。

      应用语言、平台和项目类型筛选器后，请选择 " **ASP.NET Core Web 应用**" 模板，然后选择 "**下一步**"。

   :::image type="content" source="media/vs-2022/csharp-create-new-project-aspnet-core.png" border="false" alt-text="屏幕截图显示在 &quot;创建新项目&quot; 页面上选择和突出显示的 &quot;Web 应用程序&quot; 项目模板 ASP.NET Core。":::

   > [!NOTE]
   > 如果未看到“ASP.NET Core Web 应用”模板，则可以从“创建新项目”窗口安装该模板。 在 " **找不到你要查找的内容"** 消息中，选择 " **安装更多工具和功能** " 链接。
   >
   > :::image type="content" source="media/vs-2022/not-finding-what-looking-for.png" alt-text="屏幕截图显示了 &quot;安装更多工具和功能&quot; 链接，它是未找到你要查找的消息的一部分。":::
   >
   > 然后，在 "Visual Studio 安装程序中，选择" **ASP.NET "和" web 开发**"工作负荷。
   >
   > :::image type="content" source="media/vs-2022/aspnet-core-web-dev-workload.png" alt-text="屏幕截图显示 Visual Studio 安装程序中的 ASP.NET 和 web 开发工作负荷。":::
   >
   > 在 Visual Studio 安装程序中，选择“修改”。 系统可能会提示你保存工作内容。 接下来，选择“继续”以安装工作负载。

1. 在 "**配置新项目**" 窗口中，在 " **Project 名称**" 字段中输入 " **MyCoreApp** "。 然后，选择“下一步”。

   :::image type="content" source="media/vs-2022/csharp-name-your-aspnet-app.png" border="false" alt-text="屏幕截图显示 &quot;配置新项目&quot; 窗口，并在 &quot;Project 名称&quot; 字段中输入 MyCoreApp。":::

1. 在 "**附加信息**" 窗口中，确保 "**目标框架**" 字段中显示 **.net 6.0** 。 在此窗口中，可以启用 Docker 支持并添加身份验证支持。 **身份验证类型** 的下拉菜单具有以下四个选项：
    - **无**。 无身份验证。
    - **个人帐户**。 这些身份验证存储在本地或基于 Azure 的数据库中。
    - **Microsoft 标识平台**。 此选项使用 Active Directory、Azure AD 或 Microsoft 365 进行身份验证。
    - **Windows**。 适用于 Intranet 应用程序。

    保持“启用 Docker”框处于未选中状态，并选择“无”作为身份验证类型。 接下来，选择“创建”。 

   :::image type="content" source="media/vs-2022/aspnet-core-additional-information.png" border="false" alt-text="屏幕截图显示 &quot;其他信息&quot; 窗口中的默认设置。框架值为 .NET 6.0。":::

   Visual Studio 将打开你的新项目。

::: moniker-end

### <a name="about-your-solution"></a>关于解决方案

此解决方案遵循 Razor 页面  设计模式。 它与 [Model-View-Controller (MVC)](/aspnet/core/tutorials/first-mvc-app/start-mvc?view=aspnetcore-2.1&tabs=aspnetcore2x&preserve-view=true) 设计模式的不同之处在于，它进行了优化，以包含 Razor Page 本身的模型和控制器代码。

::: moniker range="vs-2017"

## <a name="tour-your-solution"></a>浏览解决方案

 1. 项目模板会创建一个解决方案，其中包含一个名为 MyCoreApp  的 ASP.NET Core 项目。 选择 " **解决方案资源管理器** " 选项卡以查看其内容。

    ![屏幕截图显示在 Visual Studio 的解决方案资源管理器中选择的 MyCoreApp 项目。](media/csharp-aspnet-razor-solution-explorer-mycoreapp.png)

 1. 展开“页面”  文件夹，然后展开“About.cshtml”  。

     ![屏幕截图显示在 Visual Studio 的解决方案资源管理器中选择的 "关于点 c s h t m l" 文件。](media/csharp-aspnet-razor-solution-explorer-aboutcshtml.png)

 1. 查看代码编辑器中的“About.cshtml”  文件。

     ![屏幕截图显示 Visual Studio 代码编辑器中的 "关于点 c s h t m l" 文件的文本。](media/csharp-aspnet-razor-aboutcshtml-mycoreapp-code.png)

 1. 选择 **关于 .cs** 文件。

     ![屏幕截图显示在 Visual Studio 中的解决方案资源管理器中选择的关于点 c s h t m l 点 c s 文件。](media/csharp-aspnet-razor-solution-explorer-aboutcshtmlcs.png)

 1. 查看代码编辑器中的“About.cshtml.cs”  文件。

     ![屏幕截图在 Visual Studio 代码编辑器中显示关于点 c s h t m l 点 c s 文件的内容。](media/csharp-aspnet-razor-aboutcshtmlcs-mycoreapp-code.png)

 1. 该项目包含一个 wwwroot  文件夹，它是网站的根。 展开文件夹以查看其内容。

     ![屏幕截图显示在 Visual Studio 中的解决方案资源管理器中选择的 w w w w w w w。](media/csharp-aspnet-razor-solution-explorer-wwwroot.png)

    可将静态站点内容&mdash;如 CSS、图像和 JavaScript 库&mdash;直接放在所需的路径中。

 1. 该项目还包含在运行时管理 Web 应用的配置文件。 默认应用程序[配置](/aspnet/core/fundamentals/configuration)存储在 appsettings.json  中。 但是，可使用 appsettings.Development.json 替代这些设置  。 展开 **appsettings** 节点以查看 **appsettings。开发 json** 文件。

     ![屏幕截图显示在 Visual Studio 的解决方案资源管理器中选择并展开的 appsettings 点 j 儿子。](media/csharp-aspnet-razor-solution-explorer-appsettingsjson.png)

## <a name="run-debug-and-make-changes"></a>运行、调试和更改

1. 在工具栏中选择 " **IIS Express** " 按钮，在调试模式下生成并运行应用。 或者，按 **F5**，或从菜单栏中转到 "**调试**  >  " "**启动调试**"。

     ![屏幕截图显示在 Visual Studio 的工具栏中突出显示的 "我的 I S" 按钮。](media/csharp-aspnet-razor-iisexpress.png)

     > [!NOTE]
     > 如果收到一条错误消息，指出 **无法连接到 web 服务器 "IIS Express"**，请关闭 Visual Studio，然后以管理员身份重新启动该程序。 为此，可以在 "开始" 菜单中右键单击 "Visual Studio" 图标，然后从上下文菜单中选择 "以 **管理员身份运行**" 选项。
     >
     > 系统可能会向你发送一条消息，询问你是否接受 IIS SSL Express 证书。 若要在 web 浏览器中查看代码，请选择 **"是**"，如果收到跟进安全警告消息，请选择 **"是"** 。

1. Visual Studio 启动浏览器窗口。 然后，应在菜单栏中看到“主页”  、“关于”  和“联系人”  页面。 如果看不到这些页面，请选择 "汉堡" 菜单项来查看它们。

    ![屏幕截图显示在 web 应用的菜单栏中突出显示的 "MyCoreApp" 项目和 "汉堡" 菜单项。](media/csharp-aspnet-razor-browser-page.png)

1. 从菜单栏中选择 " **关于** "。

   ![屏幕截图显示了有关 web 应用菜单栏中突出显示的信息。](media/csharp-aspnet-razor-browser-page-about-menu.png)

   此外，浏览器中的“关于”  页呈现 About.cshtml  文件中设置的文本。

   ![屏幕截图显示了 web 应用中的 "关于" 页。](media/csharp-aspnet-razor-browser-page-about.png)

1. 返回 Visual Studio，然后按 **Shift + F5** 停止调试。 此操作关闭浏览器窗口中的项目。

1. 在 Visual Studio 中，选择 "**关于 cshtml**"。 然后，删除 _另一个_ 单词，并将其替换为 _文件和目录_。

    ![屏幕截图在 Visual Studio 代码编辑器中显示 About 点 c s h t m l 文件中的内容。](media/csharp-aspnet-razor-aboutcshtml-mycoreapp-code-changed.png)

1. 选择 " **关于**"。 然后，使用以下快捷方式清理文件顶部的 `using` 指令：

   悬停或选择一个灰色 `using` 的指令。 " [快速操作](../../ide/quick-actions.md) " 灯泡将显示在插入符号或左边距的正下方。 选择灯泡，然后选择 " **删除不必要的 using**"。

   ![屏幕截图显示 "删除不必要的 Using"。  它位于 "快速操作" 灯泡图标的下方。](media/csharp-aspnet-razor-remove-unnecessary-usings.png)

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

   ![屏幕截图显示代码编辑器中环境和字符串的错误标记，其形式为波浪下划线。](media/csharp-aspnet-razor-add-new-on-get-method.png)

    打开“错误列表”工具栏，查看此处列出的相同错误  。 如果看不到 **错误列表** 工具栏，请从顶部菜单栏中转到 "**查看**  >  **错误列表**"。

   ![屏幕截图在列出了环境和字符串的 Visual Studio 中显示错误列表工具栏。](media/csharp-aspnet-razor-error-list.png)

1. 让我们修复此错误。 在代码编辑器中，将光标放在包含错误的任一行上，然后选择左边距中的 "快速操作" 灯泡。 然后，从下拉菜单中选择 " **使用系统** "，将此指令添加到文件顶部，然后解决错误。

   ![屏幕截图显示其下拉菜单中的 "快速操作" 选项，并在 "使用系统" 上悬停。](media/csharp-aspnet-razor-add-usings.png)

1. 按 Ctrl  +S  保存所做的更改，然后按 F5  在 Web 浏览器中打开项目。

1. 在网站顶部，选择 " **关于** " 以查看所做的更改。

   ![屏幕截图显示网页中的 "关于" 页，其中包含所做的更改。](media/csharp-aspnet-razor-browser-page-about-changed.png)

1. 关闭 web 浏览器，按 **Shift** + **F5** 停止调试。

## <a name="change-your-about-page"></a>更改你的 "关于" 页

1. 在 **解决方案资源管理器** 中，展开 " **页面** " 文件夹，然后选择 " **关于 cshtml**"。

   ![屏幕截图显示在解决方案资源管理器的 "页面" 节点下选择的点 c s h t m l。](media/csharp-aspnet-about-page-html-file.png)

   **关于. cshtml** 文件对应于 web 应用中标题为的页面，该 **页面在 web** 浏览器中运行。

   ![屏幕截图显示浏览器窗口中 web 应用的 "关于" 页。](media/csharp-aspnet-about-page.png)

   在代码编辑器中，你将看到 " **关于** " 页上显示的文本的 HTML 代码。

   ![屏幕截图在 Visual Studio 代码编辑器中显示主页的 "关于点 c s h t m l" 文件。](media/csharp-aspnet-about-cshtml-page.png)

1. 替换 _使用此区域来提供附加信息_ 文本与 _Hello World！_

   ![屏幕截图显示 Visual Studio 代码编辑器中的 "关于点 c s h t m l" 文件，默认文本更改为 "Hello World！](media/csharp-aspnet-about-cshtml-page-hello-world.png)

1. 在 **解决方案资源管理器** 中，展开 " **about** "，然后选择 " **关于**"。 此文件还对应于 web 浏览器中的 " **关于** " 页。

   ![屏幕截图显示了在解决方案资源管理器的 "关于点 c s h t m l" 节点下选择的关于点 c s h t m l 点 c s 文件。](media/csharp-aspnet-about-page-code-file.png)

   在代码编辑器中，你将看到 c # 代码，其中包含 "**关于**" 页的 "_应用程序说明_" 区域的文本。

   ![屏幕截图显示 "代码编辑器" 中的 "应用程序说明" 区域的 C 清晰代码。](media/csharp-aspnet-about-cshtml-cs-code.png)

1. _将您的应用程序说明页_ 文本替换为 _我的消息？_

   ![代码编辑器中的屏幕截图显示从应用程序说明更改为 "我的消息" 的文本：](media/csharp-aspnet-about-cshtml-cs-message.png)

1. 选择“IIS Express”或按 Ctrl+F5 运行此应用，并在 Web 浏览器中打开它  。

   ![屏幕截图显示工具栏中突出显示的 "IIS Express" 按钮 Visual Studio](media/csharp-aspnet-hello-world-iis-button.png)

1. 在 web 浏览器中，你将在 " **关于** " 页上看到新的更改。

   ![屏幕截图显示了浏览器窗口中 Web 应用的"关于"页。 更新后的文本显示"我的消息是什么？" Hello World!](media/csharp-aspnet-about-page-hello-world.png)

1. 关闭 Web 浏览器，按 **ShiftF5** + 停止调试并保存项目。 现在可以关闭Visual Studio。

### <a name="review-your-work"></a>回顾所做的工作

查看以下动画，检查在上一部分中完成的工作：

  ![动画 gif 显示更改"关于"页文本的所有步骤。](media/csharp-aspnet-animated-hello-world.gif)

::: moniker-end

::: moniker range="=vs-2019"

## <a name="tour-your-solution"></a>浏览解决方案

 1. 项目模板会创建一个解决方案，其中包含一个名为 MyCoreApp  的 ASP.NET Core 项目。 选择" **解决方案资源管理器** "选项卡以查看其内容。

    ![屏幕截图显示"MyCoreApp"项目在 解决方案资源管理器 中Visual Studio。](media/csharp-aspnet-razor-solution-explorer-mycoreapp.png)

 1. 展开“页面”文件夹  。

     ![屏幕截图显示了"页面"文件夹的内容，该文件夹解决方案资源管理器"Visual Studio。"](media/vs-2019/csharp-aspnet-solution-explorer-pages.png)

 1. 选择 **Index.cshtml** 文件，在代码编辑器中查看。

     ![屏幕截图显示索引点 c s h t m l 文件在Visual Studio编辑器中打开。](media/vs-2019/csharp-aspnet-index-cshtml.png)

 1. 每个 .cshtml 文件都具有关联的代码文件。 若要在编辑器中打开代码文件，请展开 解决方案资源管理器 中的 **Index.cshtml** 节点，然后选择 **Index.cshtml.cs** 文件。

     ![屏幕截图显示已选择索引点 c s h t m l 文件，该文件在 解决方案资源管理器 文件中Visual Studio。](media/vs-2019/csharp-aspnet-choose-index-cshtml.png)

 1. 查看代码编辑器中的“Index.cshtml.cs”文件  。

     ![屏幕截图显示索引点 c s h t m l .cs 文件在Visual Studio编辑器中打开。](media/vs-2019/csharp-aspnet-index-cshtml-editing.png)

 1. 该项目包含一个 wwwroot  文件夹，它是网站的根。 展开文件夹以查看其内容。

     ![屏幕截图显示了在 解决方案资源管理器 中选择了 w 根Visual Studio。](media/csharp-aspnet-razor-solution-explorer-wwwroot.png)

    可将静态站点内容&mdash;如 CSS、图像和 JavaScript 库&mdash;直接放在所需的路径中。

 1. 该项目还包含在运行时管理 Web 应用的配置文件。 默认应用程序[配置](/aspnet/core/fundamentals/configuration)存储在 appsettings.json  中。 但是，可使用 appsettings.Development.json 替代这些设置  。 展开 appsettings.json 文件以查看 appsettings.Development.json 文件   。

     ![屏幕截图显示已选择 appsettings dot j，在 解决方案资源管理器 中展开Visual Studio。](media/csharp-aspnet-razor-solution-explorer-appsettingsjson.png)

## <a name="run-debug-and-make-changes"></a>运行、调试和更改

1. 选择工具栏 **IIS Express** 按钮，以在调试模式下生成并运行应用。 或者，按 **F5**，或者从菜单栏转到"**调试** > "**"开始调试**"。

     ![屏幕截图显示工具栏中突出显示的"IS Express"Visual Studio。](media/csharp-aspnet-razor-iisexpress.png)

     > [!NOTE]
     > 如果收到错误消息"无法连接到 Web 服务器"IIS Express **"**，请关闭Visual Studio，然后以管理员角色重新启动程序。 为此，可以右键单击"开始Visual Studio图标，然后从上下文菜单中选择"以管理员方式运行"选项。
     >
     > 系统可能会向你发送一条消息，询问你是否接受 IIS SSL Express 证书。 若要在 Web 浏览器中查看代码，请选择"是"，如果收到后续安全警告消息，请选择"是"。

1. Visual Studio 启动浏览器窗口。 然后，**应会看到菜单****栏中的**"主页"和"隐私"页。

1. 从 **菜单栏中** 选择"隐私"。 浏览器中的“隐私”页呈现 Privacy.cshtml 文件中设置的文本   。

   ![屏幕截图显示了"MyCoreApp 隐私"页，其文本如下：使用此页详细说明站点的隐私策略。](media/vs-2019/csharp-aspnet-browser-page-privacy.png)

1. 返回到Visual Studio，然后按 **Shift+F5** 停止调试。 此操作在浏览器窗口中关闭项目。

1. 在 Visual Studio 中，打开要编辑的“Privacy.cshtml”  。 接下来，删除句子 _"使用此__@ViewData_ 页详细说明站点的隐私策略"，并将其替换为从 ["TimeStamp"] 开始正在构造的此页面。

    ![屏幕截图显示"隐私"点 c s h t m l 文件在Visual Studio编辑器中打开，并包含更新的文本。](media/vs-2019/csharp-aspnet-privacy-cshtml-code-changed.png)

1. 现在，让我们对代码进行更改。 选择 **Privacy.cshtml.cs**。 接下来，使用 `using` 下列快捷方式清理文件顶部的 指令：

   鼠标悬停在或选择灰出 `using` 指令。 快速 [操作](../../ide/quick-actions.md) 灯泡将出现在点线正下方或左边距中。 选择灯泡，然后选择" **删除不必要的 using"**。

   ![屏幕截图显示了代码编辑器中的 Privacy dot c s h t m l Visual Studio，为灰显 using 指令公开了"快速操作"工具提示。](media/vs-2019/csharp-aspnet-remove-unnecessary-usings.png)

   现在， **选择"预览** 更改"以查看将更改的内容。

   ![屏幕截图显示"预览更改"对话框。 该对话框显示要删除的 指令，并预览删除后的代码更改。](media/vs-2019/csharp-aspnet-preview-changes.png)

   选择“应用”。 Visual Studio 从文件中删除不必要的 `using` 指令。

1. 接下来，在 `OnGet()` 方法中，将主体更改为以下代码：

     ```csharp
     public void OnGet()
     {
        string dateTime = DateTime.Now.ToShortDateString();
        ViewData["TimeStamp"] = dateTime;
     }
    ```

1. 请注意，DateTime 下会出现波浪 **形下划线**。 出现波浪形下划线，因为此类型不在范围内。

   ![屏幕截图以波浪下划线的形式显示代码编辑器中 DateTime 的错误Visual Studio标记。](media/vs-2019/csharp-aspnet-add-new-onget-method.png)

    打开“错误列表”工具栏，查看此处列出的相同错误  。 如果看不到"错误列表 **"工具栏，****请从** > 顶部菜单栏中转到"视图""操作程序列表"。

   ![屏幕截图显示了"错误列表"工具栏Visual Studio列出了 DateTime。](media/vs-2019/csharp-aspnet-error-list.png)

1. 让我们修复此错误。 在代码编辑器中，将光标置于包含错误的行上，然后选择左边距中的"快速操作"灯泡。 然后，从下拉菜单中选择"使用 **系统"** ;将此指令添加到文件顶部并解决错误。

   ![屏幕截图显示其下拉菜单中的"快速操作"选项，使用"系统"打开鼠标悬停。](media/vs-2019/csharp-aspnet-add-usings.png)

1. 按 F5，即可在 Web 浏览器中打开项目  。

1. 在网站顶部，选择 **"隐私"** 以查看所做的更改。

   ![显示更新的“隐私”页的屏幕截图，其中包含你所做的更改。](media/vs-2019/csharp-aspnet-browser-page-privacy-changed.png)

1. 关闭 Web 浏览器，按 **ShiftF5** + 停止调试。

## <a name="change-your-home-page"></a>更改主页

1. 在 **解决方案资源管理器，** 展开 **"Pages** "文件夹，然后选择" **Index.cshtml"**。

   ![屏幕截图显示已选择索引点 c s h t m l，该索引点在"页面"节点下解决方案资源管理器。](media/vs-2019/csharp-aspnet-index-page-cshtml-file.png)

   **Index.cshtml** 文件与 Web 应用中的主页相对应，该页面在 Web 浏览器中运行。

   ![ 屏幕截图显示浏览器窗口中 Web 应用的"主页"。](media/vs-2019/csharp-aspnet-index-page.png)

   在代码编辑器中，你将看到主页上显示的文本的 **HTML 代码。**

   ![屏幕截图显示了代码编辑器中主页的索引点 c s h t m l Visual Studio文件。](media/vs-2019/csharp-aspnet-index-cshtml-page.png)

1. 将" _欢迎"_ 文本替换为 _Hello World！_

   ![屏幕截图显示代码编辑器中的索引点 c s h t m l 文件Visual Studio，"欢迎"文本已更改为Hello World！。](media/vs-2019/csharp-aspnet-index-cshtml-page-hello-world.png)
    
1. 选择“IIS Express”或按 Ctrl+F5 运行此应用，并在 Web 浏览器中打开它  。

   ![屏幕截图显示IIS Express工具栏中突出显示的"Visual Studio"按钮。](media/vs-2019/csharp-aspnet-generic-iis-button.png)

1. 在 Web 浏览器中，你将在主页上 **看到新的更改** 。

   ![屏幕截图显示浏览器窗口中 Web 应用的"主页"。 更新后的文本显示"Hello World！](media/vs-2019/csharp-aspnet-index-page-hello-world.png)

1. 关闭 Web 浏览器，按 **ShiftF5** + 停止调试并保存项目。 现在可以关闭Visual Studio。

::: moniker-end

::: moniker range=">=vs-2022"

## <a name="tour-your-solution"></a>浏览解决方案

 1. 项目模板会创建一个解决方案，其中包含一个名为 MyCoreApp  的 ASP.NET Core 项目。 选择" **解决方案资源管理器** "选项卡以查看其内容。

     :::image type="content" source="media/vs-2022/csharp-aspnet-razor-solution-explorer-mycoreapp.png" alt-text="屏幕截图显示了所选的 MyCoreApp 项目及其在 解决方案资源管理器 中Visual Studio。":::

 1. 展开“页面”文件夹  。

     :::image type="content" source="media/vs-2022/csharp-aspnet-solution-explorer-pages.png" alt-text="屏幕截图显示了&quot;页面&quot;文件夹中页面解决方案资源管理器。":::

 1. 选择 **Index.cshtml** 文件，在代码编辑器中查看。

     :::image type="content" source="media/vs-2022/csharp-aspnet-index-cshtml.png" alt-text="屏幕截图显示 Index.cshtml 文件在Visual Studio编辑器中打开。":::

 1. 每个 .cshtml 文件都具有关联的代码文件。 若要在编辑器中打开代码文件，请展开 解决方案资源管理器 中的 **Index.cshtml** 节点，然后选择 **Index.cshtml.cs** 文件。

     :::image type="content" source="media/vs-2022/csharp-aspnet-choose-index-cshtml.png" alt-text="屏幕截图显示 Index.cshtml 文件在 解决方案资源管理器 Visual Studio。":::

 1. 查看代码编辑器中的“Index.cshtml.cs”文件  。

     :::image type="content" source="media/vs-2022/csharp-aspnet-index-cshtml-editing.png" alt-text="屏幕截图显示 Index.cshtml.cs 文件在Visual Studio编辑器中打开。":::

 1. 该项目包含一个 wwwroot  文件夹，它是网站的根。 展开文件夹以查看其内容。

     :::image type="content" source="media/vs-2022/csharp-aspnet-razor-solution-explorer-wwwroot.png" alt-text="屏幕截图显示了在 解决方案资源管理器 中选择了 w 根Visual Studio。":::

    可将静态站点内容&mdash;如 CSS、图像和 JavaScript 库&mdash;直接放在所需的路径中。

 1. 该项目还包含在运行时管理 Web 应用的配置文件。 默认应用程序[配置](/aspnet/core/fundamentals/configuration)存储在 appsettings.json  中。 但是，可使用 appsettings.Development.json 替代这些设置  。 展开 appsettings.json 文件以查看 appsettings.Development.json 文件   。

     :::image type="content" source="media/vs-2022/csharp-aspnet-razor-solution-explorer-appsettingsjson.png" alt-text="屏幕截图显示已选择并展开 appsettings.json，其中公开了 appsettings。Development.json，解决方案资源管理器 Visual Studio。":::

## <a name="run-debug-and-make-changes"></a>运行、调试和更改

1. 选择工具栏 **IIS Express** 按钮，以在调试模式下生成并运行应用。 或者，按 **F5**，或者从菜单栏转到"**调试** > "**"开始调试**"。

     :::image type="content" source="media/vs-2022/csharp-aspnet-razor-iis-express.png" alt-text="屏幕截图显示工具栏中突出显示的&quot;IS Express&quot;按钮Visual Studio。":::

     > [!NOTE]
     > 如果收到错误消息"无法连接到 Web 服务器"IIS Express **"**，请关闭Visual Studio，然后以管理员角色重新启动程序。 为此，可以右键单击"开始Visual Studio图标，然后从上下文菜单中选择"以管理员方式运行"选项。
     >
     > 系统可能会向你发送一条消息，询问你是否接受 IIS SSL Express 证书。 若要在 Web 浏览器中查看代码，请选择"是"，如果收到后续安全警告消息，请选择"是"。

1. Visual Studio 启动浏览器窗口。 然后，**应会看到菜单****栏中的**"主页"和"隐私"页。

1. 从 **菜单栏中** 选择"隐私"。 浏览器中的“隐私”页呈现 Privacy.cshtml 文件中设置的文本   。

   :::image type="content" source="media/vs-2022/csharp-aspnet-browser-page-privacy.png" alt-text="屏幕截图显示了&quot;MyCoreApp 隐私&quot;页，其文本如下：使用此页详细说明站点的隐私策略。":::

1. 返回到Visual Studio，然后按 **Shift+F5** 停止调试。 此操作在浏览器窗口中关闭项目。

1. 在 Visual Studio 中，打开要编辑的“Privacy.cshtml”  。 接下来，删除句子 _"使用此__@ViewData_ 页详细说明站点的隐私策略"，并将其替换为从 ["TimeStamp"] 开始正在构造的此页面。

   :::image type="content" source="media/vs-2022/csharp-aspnet-privacy-cshtml-code-changed.png" alt-text="屏幕截图显示了在代码编辑器中打开的 Privacy.cshtml Visual Studio更新的文本。":::

1. 现在，让我们对代码进行更改。 选择 **Privacy.cshtml.cs**。 然后，选择以下快捷方式清理文件顶部的 `using` 指令：

   鼠标悬停在或选择灰出 `using` 指令。 快速 [操作](../../ide/quick-actions.md) 灯泡将出现在点线正下方或左边距中。 选择灯泡，然后选择" **删除不必要的 using"**。

   :::image type="content" source="media/vs-2022/csharp-aspnet-remove-unnecessary-usings.png" alt-text="屏幕截图显示了代码编辑器中的 Privacy.cshtml Visual Studio，并突出显示了&quot;快速操作&quot;工具提示和预览更改。":::

   现在， **选择"预览** 更改"以查看将更改的内容。

   :::image type="content" source="media/vs-2022/csharp-aspnet-preview-changes.png" border="false" alt-text="屏幕截图显示&quot;预览更改&quot;对话框。该对话框显示要删除的 指令，并预览删除后的代码更改。":::

   选择“应用”。 Visual Studio 从文件中删除不必要的 `using` 指令。

1. 接下来，使用 [DateTime.ToString](xref:System.DateTime.ToString%2A) 方法为针对区域性或区域设置格式的当前日期创建字符串。

   - 方法的第一个参数指定如何显示日期。 此示例使用格式说明符 (`d`) 指示短日期格式。
   - 第二个参数是 [CultureInfo](/dotnet/api/system.globalization.cultureinfo) 对象，该对象指定日期的区域性或区域。 第二个参数确定日期中任意单词的语言以及所使用的分隔符类型等。

将 `OnGet()` 方法的主体更改为以下代码：

   ```csharp
   public void OnGet()
   {
      string dateTime = DateTime.Now.ToString("d", new CultureInfo("en-US"));
      ViewData["TimeStamp"] = dateTime;
   }
   ```

1. 请注意，" **CultureInfo"下会出现波浪形下划线**。 出现波浪形下划线，因为此类型不在范围内。

   :::image type="content" source="media/vs-2022/csharp-aspnet-add-new-onget-method.png" alt-text="屏幕截图以波浪下划线的形式显示代码编辑器中 CultureInfo 的错误Visual Studio标记。":::

    打开" **错误列表"** 工具栏，查看列出的相同错误。 如果看不到"错误列表 **"工具栏，****请从** > 顶部菜单栏中转到"视图""操作程序列表"。

   :::image type="content" source="media/vs-2022/csharp-aspnet-error-list.png" alt-text="屏幕截图显示&quot;错误列表&quot;工具栏Visual Studio列出了 CultureInfo，并且缺少 using 指令。":::

1. 让我们修复此错误。 在代码编辑器中，将光标置于包含错误的行上，然后选择左边距中的"快速操作"灯泡。 然后，从下拉菜单中选择"使用 **System.Globalization** ";将此指令添加到文件顶部并解决错误。

   :::image type="content" source="media/vs-2022/csharp-aspnet-add-usings.png" alt-text="屏幕截图显示其下拉菜单中的&quot;快速操作&quot;选项，并显示了 System.Globalization 指令上的鼠标悬停。":::

1. 按 F5，即可在 Web 浏览器中打开项目  。

1. 在网站顶部，选择 **"隐私"** 以查看所做的更改。

   :::image type="content" source="media/vs-2022/csharp-aspnet-browser-page-privacy-changed.png" alt-text="显示 MyCoreApp 的“隐私”页的屏幕截图，其中包括添加日期所做的更改。":::

1. 关闭 Web 浏览器，按 **ShiftF5** + 停止调试。

## <a name="change-your-home-page"></a>更改主页

1. 在 **解决方案资源管理器，** 展开 **"Pages** "文件夹，然后选择" **Index.cshtml"**。

   :::image type="content" source="media/vs-2022/csharp-aspnet-index-page-cshtml-file.png" alt-text="屏幕截图显示 Index.cshtml 在&quot;页面&quot;节点下选择了解决方案资源管理器。":::

   **Index.cshtml** 文件与 Web 应用中的主页相对应，该页面在 Web 浏览器中运行。

   :::image type="content" source="media/vs-2022/csharp-aspnet-index-page.png" alt-text="屏幕截图显示浏览器窗口中 Web 应用的&quot;主页&quot;。":::

   在代码编辑器中，你将看到主页上显示的文本的 **HTML 代码。**

   :::image type="content" source="media/vs-2022/csharp-aspnet-index-cshtml-hello.png" alt-text="屏幕截图显示了代码编辑器中主页的 Index.cshtml Visual Studio文件。":::

1. 将" _欢迎"_ 文本替换为 _Hello World！_

   :::image type="content" source="media/vs-2022/csharp-aspnet-index-cshtml-page-hello-world.png" alt-text="屏幕截图显示代码编辑器中的 Index.cshtml Visual Studio，&quot;Welcome&quot;文本已更改为&quot;Hello World！&quot;。":::
    
1. 选择“IIS Express”或按 Ctrl+F5 运行此应用，并在 Web 浏览器中打开它  。

   :::image type="content" source="media/vs-2022/csharp-aspnet-generic-iis-button.png" alt-text="屏幕截图显示IIS Express工具栏中突出显示的&quot;Visual Studio&quot;按钮。":::

1. 在 Web 浏览器中，你将在主页上 **看到新的更改** 。

   :::image type="content" source="media/vs-2022/csharp-aspnet-index-page-hello-world.png" alt-text="屏幕截图显示浏览器窗口中 Web 应用的&quot;主页&quot;。更新后的文本显示&quot;Hello World！&quot;。":::

1. 关闭 Web 浏览器，按 **ShiftF5** + 停止调试并保存项目。 现在可以关闭Visual Studio。

::: moniker-end

## <a name="next-steps"></a>后续步骤

恭喜你完成本教程！ 我们希望你喜欢了解 C#、ASP.NET Core和 Visual Studio IDE。 要详细了解如何使用 C# 和 ASP.NET 创建 Web 应用或网站，请继续学习以下教程：

> [!div class="nextstepaction"]
> [使用 ASP.NET Core 创建 Razor 页面 Web 应用](/aspnet/core/tutorials/razor-pages/?view=aspnetcore-2.1&preserve-view=true)

或者，了解如何使用 Docker 容器化 Web 应用：

> [!div class="nextstepaction"]
> [Visual Studio 中的容器工具](../../containers/overview.md)

## <a name="see-also"></a>另请参阅

[使用 Visual Studio 将 Web 应用发布到 Azure App Service](../../deployment/quickstart-deploy-aspnet-web-app.md)

---
title: 教程：使用 F# 创建 ASP.NET Core Web 服务
description: 在本教程中，了解如何在 Visual Studio 中使用 F# 创建 ASP.NET Core Web 服务。
author: anandmeg
ms.author: meghaanand
ms.topic: tutorial
ms.date: 01/28/2022
ms.custom: vs-acquisition
ms.technology: vs-ide-general
dev_langs:
- FSharp
ms.workload:
- aspnet
- dotnetcore
ms.openlocfilehash: f1e26b2f9d9b6d5cd98b3ab8450c600e5fe49f41
ms.sourcegitcommit: aaa209e485d49c2ad9cf85ba5282c04b892a1626
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/06/2022
ms.locfileid: "138063386"
---
# <a name="tutorial-create-an-aspnet-core-web-service-in-f"></a>教程：使用 F# 创建 ASP.NET Core Web 服务

Visual Studio 集成开发环境 (IDE) 对多个产品类型支持 F#。
可轻松创建完整的 Web 服务应用。

有关使用 F# 编码的详细信息，请参阅[什么是 F#](/dotnet/fsharp/what-is-fsharp)。
若要创建 Hello World 控制台应用，请参阅 [Visual Studio 中的 F# 入门](/dotnet/fsharp/get-started/get-started-visual-studio)。

在本教程中，你将了解如何执行以下操作：

> [!div class="checklist"]
> - 创建 ASP.NET Core Web 服务。
> - 使用 F# 向 HttpGet 成员添加内容。
> - 构建程序并运行。

## <a name="prerequisites"></a>先决条件

::: moniker range="vs-2017"
若要完成本教程，必须具有 Visual Studio。
请访问 [Visual Studio 下载页](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)获取免费版本。
::: moniker-end
::: moniker range="vs-2019"
若要完成本教程，必须具有 Visual Studio。
请访问 [Visual Studio 下载页](https://visualstudio.microsoft.com/vs/)获取免费版本。
::: moniker-end
::: moniker range=">=vs-2022"
若要完成本教程，必须具有 Visual Studio。
请访问 [Visual Studio 下载页](https://visualstudio.microsoft.com/downloads)获取免费版本。
::: moniker-end

确保已安装必要的组件：

1. 选择 Windows 图标“开始”并键入“Visual Studio 安装程序”。
1. 选择“修改”，查看安装的工作负载。
1. 确保已选择“ASP.NET 和 Web 开发”，或添加它。

   ![屏幕截图显示了在 Visual Studio 安装程序中修改工作负载。](./media/tutorial-fsharp-web-app/modify-visual-studio-workload.png)

1. 如果进行了任何更改，请选择“修改”以安装组件。

## <a name="create-an-aspnet-core-web-service"></a>创建 ASP.NET Core Web 服务

在此部分，创建一个 ASP.NET Core Web API 项目。
即使尚未添加任何内容，项目类型随附的模板文件里也包含一个功能性 Web 服务。

::: moniker range="vs-2017"
1. 启动 Visual Studio 2017。 从顶部菜单栏中选择“文件” > “新建” > “项目”。

1. 在“新建项目”对话框的左窗格中，展开“Visual F#”，然后选择“Web”。 在中间窗格中，选择“ASP.NET Core Web 应用程序”。

1. 对于“名称”，键入“FSharpTutorial”，然后选择“确定”。

1. 在“新建 ASP.NET Core Web 应用程序”对话框中，选择默认版本。

   > [!NOTE]
   > 不再支持 ASP.NET Core 2.1。
   > 建议不要对生产环境使用不受支持的选项。

1. 在“解决方案资源管理器”中，展开“控制器”文件夹，然后选择“ValuesController.fs”，在编辑器中将其打开  。

   ![屏幕截图显示了 F# Web API 项目中“值控制器”呈展开状态的“解决方案资源管理器”。](./media/tutorial-fsharp-web-app/values-controller-fsharp-solution-explorer.png)

1. 接下来，修改现有 `Get()` 成员示例，使其与以下代码相匹配：

   ```fsharp
   [<HttpGet>]
   member this.Get() =
       let values = [|"Hello"; "World"; "First F#/ASP.NET Core web API!"|]
       ActionResult<string[]>(values)
   ```

   此代码包含一个 F# 值数组，这些值绑定到 `values` 名称。
   它将这些值作为 `ActionResult` 传递到 ASP.NET Core 模型-视图-控制器框架。
   ASP.NET Core 会完成其余部分。

1. 选择“F5”键以运行项目。
   此时将打开一个浏览器窗口以显示 Hello World 消息。

::: moniker-end
::: moniker range=">=vs-2019"
1. 启动 Visual Studio。

1. 在“开始”窗口中，选择“创建新项目”。

1. 在“创建新项目”页上，在搜索框中键入“F# Web” 。 选择“ASP.NET Core Web API”项目模板，然后选择“下一步” 。

1. 在“配置新项目”对话框中，对于“项目名称”，输入“FSharpTutorial” 。

1. 在“其他信息”对话框中，接受“框架”的默认版本 。

   选择“创建”时，Visual Studio 创建新的 F# 项目。 可在“解决方案资源管理器”窗口中查看项目组件。
   Visual Studio 显示“概述”页。

1. 在“解决方案资源管理器”工具栏中，展开“控制器”文件夹，然后选择“WeatherForecastController.fs”控制器以在编辑器中打开代码文件  。

   ![屏幕截图显示了 F# Web API 项目中“天气预报控制器”呈展开状态的“解决方案资源管理器”。](./media/tutorial-fsharp-web-app/forecast-controller-fsharp-solution-explorer.png)

1. 接下来，将 `Get()` 成员修改为以下代码：

   ```fsharp
   [<HttpGet>]
   member this.Get() =
       let values = [|"Hello"; "World"; "First F#/ASP.NET Core web API!"|]
       ActionResult<string[]>(values)
   ```

   此代码包含一个 F# 值数组，这些值绑定到 `values` 名称。
   它将这些值作为 `ActionResult` 传递到 ASP.NET Core 模型-视图-控制器框架。
   ASP.NET Core 会完成其余部分。

1. 选择“F5”键以运行项目。
   此时将打开一个浏览器窗口以显示 Hello World 消息。

::: moniker-end

> [!NOTE]
> 如果收到询问你是否接受 IIS SSL Express 证书的消息，请选择“是”以在 Web 浏览器中查看代码，如果收到后续的安全警告消息，也请选择“是”。

## <a name="next-steps"></a>后续步骤

查看 [F# 教程](/dotnet/fsharp/tour)（如果你尚未查看）。
本教程介绍 F# 语言的核心功能。
它概述了 F# 的一些功能以及你可运行的代码示例。

> [!div class="nextstepaction"]
> [F# 教程](/dotnet/fsharp/tour)

## <a name="see-also"></a>另请参阅

- [F# 语言参考](/dotnet/fsharp/language-reference/index)
- [类型推理](/dotnet/fsharp/language-reference/type-inference)
- [符号和运算符参考](/dotnet/fsharp/language-reference/symbol-and-operator-reference/index)

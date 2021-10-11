---
title: 创建您的第一个 Node.js 应用程序
ms.custom:
- vs-acquisition
- SEO-VS-2020
description: 本快速入门中，将在 Visual Studio 中创建 Node.js 应用
ms.date: 09/14/2021
ms.technology: vs-javascript
ms.topic: quickstart
ms.devlang: javascript
ms.assetid: b0e4ebed-1a01-41ef-aad1-4d8465ce5322
author: mikejo5000
ms.author: mikejo
manager: jmartens
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: fceecc9110a0ae15edf4d702e5c4db19cf129905
ms.sourcegitcommit: 8e74969ff61b609c89b3139434dff5a742c18ff4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2021
ms.locfileid: "128430135"
---
# <a name="quickstart-create-your-first-nodejs-app-with-visual-studio"></a>快速入门：使用 Visual Studio 创建你的第一个 Node.js 应用

在这篇为时 5-10 分钟的 Visual Studio 集成开发环境 (IDE) 简介中，你将创建一个简单的 Node.js Web 应用。

## <a name="prerequisites"></a>先决条件

在开始之前，请安装 Visual Studio 并设置 Node.js 环境。

::: moniker range=">=vs-2022"
### <a name="install-visual-studio-and-the-nodejs-workload"></a>安装 Visual Studio 和 Node.js 工作负载

如果尚未安装 Visual Studio，请执行以下操作：

1. 转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页免费安装 Visual Studio 2022。

1. 在 Visual Studio 安装程序中，选择“Node.js 开发”工作负载，然后选择“安装”。

   ![显示 Visual Studio 安装程序中选择的 Node.js 工作负载的屏幕截图。](../ide/media/quickstart-nodejs-workload.png)

如果已安装 Visual Studio：

1. 在 Visual Studio 中，转到“工具”>“获取工具和功能” 。

1. 在 Visual Studio 安装程序中，选择“Node.js 开发”工作负载，然后选择“修改”以下载并安装工作负载。

### <a name="set-up-your-nodejs-environment"></a>设置 Node.js 环境

[安装 Node.js 运行时的 LTS 版本](https://nodejs.org/en/download/)。 LTS 版本可以实现与外部框架和库的最佳兼容性。

虽然 Node.js 是为 32 位和 64 位体系结构生成的，但 Node.js 安装程序每次仅支持一个版本。

Visual Studio 通常会检测到已安装的运行时，如果未检测到，你可以将项目配置为引用已安装的运行时：

   1. [创建项目](#create-your-app-project)后，右键单击项目节点。

   1. 选择“属性”并设置“Node.exe 路径” 。 可以使用全局 Node.js 安装，或者为任何 Node.js 项目指定本地解释器的路径。

:::moniker-end
::: moniker range="vs-2019"
### <a name="install-visual-studio"></a>安装 Visual Studio

如果尚未安装 Visual Studio 2019，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页免费安装。
::: moniker-end
::: moniker range="vs-2017"
### <a name="install-visual-studio"></a>安装 Visual Studio

如果尚未安装 Visual Studio 2017，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)页免费安装。
::: moniker-end

::: moniker range="<=vs-2019"
### <a name="set-up-your-nodejs-environment"></a>设置 Node.js 环境

Visual Studio 可以帮助设置环境，包括安装 Node.js 开发常用的工具。

1. 在 Visual Studio 中，转到“工具”>“获取工具和功能” 。

1. 在 Visual Studio 安装程序中，选择“Node.js 开发”工作负载，然后选择“修改”以下载并安装工作负载 。

    ![显示 Visual Studio 安装程序中选择的 Node.js 工作负载的屏幕截图。](../ide/media/quickstart-nodejs-workload.png)

1. 安装 [Node.js 运行时](https://nodejs.org/en/download/)的 LTS 版本。 建议使用 LTS 版本，以实现与外部框架和库的最佳兼容性。

    虽然 Node.js 是为 32 位和 64 位体系结构构建的，但 Node.js 安装程序一次仅支持安装一个版本。

1. 如果 Visual Studio 没有检测到已安装的运行时（通常会检测到），请将项目配置为引用已安装的运行时：

   1. [创建项目](#create-your-app-project)后，右键单击项目节点。

   1. 选择“属性”并设置“Node.exe 路径” 。 可以使用 Node.js 的全局安装，或者在每个 Node.js 项目中指定本地解释器的路径。

::: moniker-end
## <a name="create-your-app-project"></a>创建应用项目

在 Visual Studio 中，创建一个新的 Node.js 项目。

::: moniker range=">=vs-2022"

1. 启动 Visual Studio，然后按 Esc 关闭开始窗口。

1. 按 Ctrl+Q，然后在搜索框中键入“node.js” 。

1. 选择“空白 Node.js Web 应用程序”。

1. 在对话框中，选择“创建”。

::: moniker-end

::: moniker range="vs-2019"

1. 按 Esc 关闭启动窗口  。

1. 按 Ctrl + Q 打开搜索框，然后键入“Node.js” 。

1. 选择“空 Node.js Web 应用程序(JavaScript)”。 在对话框中，选择“创建”。

::: moniker-end

::: moniker range="vs-2017"
1. 从顶部菜单栏中选择“文件”>“新建”>“项目”    。

1. 在“新建项目”对话框的左侧窗格中，展开“JavaScript”，然后选择“Node.js”  。

1. 在中间窗格中，选择“空 Node.js Web 应用程序”，然后选择“确定” 。

::: moniker-end
此时，Visual Studio 将创建并打开项目。 项目的 server.js 文件将在编辑器中打开。

如果未看到“空白 Node.js Web 应用程序”项目模板，则需要添加“Node.js 开发”工作负载 。 有关说明，请参阅[先决条件](#prerequisites)。

## <a name="explore-the-ide"></a>探索 IDE

::: moniker range=">=vs-2022"
Visual Studio 可以帮助设置环境，包括安装 Node.js 开发常用的工具。

1. 在右侧窗格中，查看“解决方案资源管理器”。
   
   - 顶层是解决方案，默认情况下它与项目同名。 解决方案在磁盘上由 .sln 文件表示，是一个或多个相关项目的容器  。
   - 项目（具有你在设置它时使用的名称）以粗体突出显示。 在磁盘上，项目由项目文件夹中的 .njsproj 文件表示。
   - npm 节点显示已安装的 npm 包。 可以右键单击“npm”节点以搜索 npm 包，并使用对话框安装 npm 包。

   ![显示“解决方案资源管理器”窗格的屏幕截图。](../ide/media/vs-2022/quickstart-nodejs-solution-explorer.png)

1. 若要从命令提示符安装 npm 包或 Node.js 命令，请右键单击项目节点，然后选择“在此处打开命令提示符”。

   ![显示项目上下文菜单中“在此处打开命令提示符”的屏幕截图。](../ide/media/vs-2022/quickstart-nodejs-command-prompt.png)

1. 若要测试导航到源代码，请在打开的 server.js 文件中选择 `createServer` 并按 F12，或者右键单击 `createServer` 并从上下文菜单中选择“转到定义” 。 此命令将转到 http.d.ts 中 `createServer` 函数的定义。

   ![显示 createServer 上下文菜单中“转到定义”的屏幕截图。](../ide/media/vs-2022/quickstart-nodejs-go-to-definition.png)

1. 返回 server.js，找到代码行 `res.end('Hello World\n');`，并将其修改为：

   `res.end('Hello World\n' + res.connection.`

   当你键入 `connection.` 时，IntelliSense 会提供用于自动完成代码输入的选项。

   ![显示 IntelliSense 自动完成选项的屏幕截图。](../ide/media/vs-2022/quickstart-nodejs-intellisense.png)

1. 选择 `localPort`，并键入 `);` 以完成语句：

    `res.end('Hello World\n' + res.connection.localPort);`

::: moniker-end

::: moniker range="<=vs-2019"
1. 在右侧窗格中，查看“解决方案资源管理器”。
   
   - 顶层是解决方案，默认情况下它与项目同名。 解决方案在磁盘上由 .sln 文件表示，是一个或多个相关项目的容器  。
   - 项目（具有你在设置它时使用的名称）以粗体突出显示。 在磁盘上，项目由项目文件夹中的 .njsproj 文件表示。
   - npm 节点显示已安装的 npm 包。 可以右键单击“npm”节点以搜索 npm 包，并使用对话框安装 npm 包。

   ![显示“解决方案资源管理器”窗格的屏幕截图。](../ide/media/quickstart-nodejs-solution-explorer.png)

1. 若要从命令提示符安装 npm 包或 Node.js 命令，请右键单击项目节点，然后从上下文菜单中选择“在此处打开命令提示符”。

   ![显示项目上下文菜单中“在此处打开命令提示符”的屏幕截图。](../ide/media/quickstart-nodejs-command-prompt.png)

1. 若要测试导航到源代码，请在打开的 server.js 文件中选择“http.createServer”并按 F12，或者从右键单击上下文菜单中选择“转到定义”  。 此命令将转到 http.d.ts 中 `createServer` 函数的定义。

   ![显示 createServer 上下文菜单中“转到定义”的屏幕截图。](../ide/media/quickstart-nodejs-gotodefinition.png)

1. 返回 server.js，找到代码行 `res.end('Hello World\n');`，并将其修改为：

   `res.end('Hello World\n' + res.connection.`

   当你键入“connection.”时，IntelliSense 会提供用于自动完成代码输入的选项。

   ![显示 IntelliSense 自动完成选项的屏幕截图。](../ide/media/quickstart-nodejs-intellisense.png)

1. 选择“localPort”，并键入 `);` 以完成语句：

    `res.end('Hello World\n' + res.connection.localPort);`
:::moniker-end

## <a name="run-the-app"></a>运行应用

1. 按 Ctrl+F5 或选择“调试” > “开始执行(不调试)”以运行应用   。
 
   应用将在浏览器中打开。

1. 在浏览器中，验证是否看到了“Hello World”消息和本地端口号。

恭喜！ 你使用 Visual Studio 创建了一个简单的 Node.js 应用。 若要了解更深入的信息，请继续阅读目录中的“教程”部分。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [将应用部署到 Linux 应用服务](../javascript/publish-nodejs-app-azure.md)

> [!div class="nextstepaction"]
> [Node.js 和 Express 教程](../javascript/tutorial-nodejs.md)

> [!div class="nextstepaction"]
> [Node.js 和 React 教程](../javascript/tutorial-nodejs-with-react-and-jsx.md)


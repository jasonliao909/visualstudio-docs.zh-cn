---
title: 创建您的第一个 Node.js 应用程序
ms.custom:
- vs-acquisition
- SEO-VS-2020
description: 本快速入门中，将在 Visual Studio 中创建 Node.js 应用
ms.date: 03/25/2021
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
ms.openlocfilehash: 0c44bfcfe1e7f07f83ca2b7dbb8b0604f5efe5f1
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2021
ms.locfileid: "112386158"
---
# <a name="quickstart-create-your-first-nodejs-app-with-visual-studio"></a>快速入门：使用 Visual Studio 创建你的第一个 Node.js 应用

在这个对 Visual Studio 集成开发环境 (IDE) 的 5-10 分钟简介中，可以创建简单的 Node.js Web 应用。

## <a name="prerequisites"></a>先决条件

在开始之前，请安装 Visual Studio 并设置 Node.js 环境。

### <a name="install-visual-studio"></a>安装 Visual Studio

::: moniker range=">=vs-2019"
如果尚未安装 Visual Studio 2019，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页免费安装。
::: moniker-end
::: moniker range="vs-2017"
如果尚未安装 Visual Studio 2017，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)页免费安装。
::: moniker-end

### <a name="set-up-your-nodejs-environment"></a>设置 Node.js 环境

Visual Studio 可以帮助设置环境，包括安装 Node.js 开发常用的工具。

1. 在 Visual Studio 中，转至“工具” > “获取工具和功能” 。

1. 在 Visual Studio 安装程序中，选择“Node.js 开发”工作负载，然后选择“修改”以下载并安装工作负载 。

    ![Visual Studio 安装程序中的 Node.js 工作负载](../ide/media/quickstart-nodejs-workload.png)

1. 安装 [Node.js 运行时](https://nodejs.org/en/download/)的 LTS 版本。 建议使用 LTS 版本，以实现与外部框架和库的最佳兼容性。

    虽然 Node.js 是为 32 位和 64 位体系结构构建的，但 Node.js 安装程序一次仅支持安装一个版本。

1. 如果 Visual Studio 没有检测到已安装的运行时（通常会检测到），请将项目配置为引用已安装的运行时：

   1. [创建项目](#create-your-app-project)后，右键单击项目节点。

   1. 选择“属性”并设置“Node.exe 路径” 。 可以使用 Node.js 的全局安装，或者在每个 Node.js 项目中指定本地解释器的路径。

## <a name="create-your-app-project"></a>创建应用项目

1. 如果尚未安装，请安装 [Node.js 运行时](https://nodejs.org/en/download/)的 LTS 版本。 有关详细信息，请参阅[先决条件](#prerequisites)。

1. 打开 Visual Studio。

1. 创建新项目。

    ::: moniker range=">=vs-2019"

    1. 按 Esc 关闭启动窗口  。

    1. 按 Ctrl + Q 打开搜索框，然后键入“Node.js” 。

    1. 选择“空 Node.js Web 应用程序(JavaScript)”。 在对话框中，选择“创建”。

    ::: moniker-end

    ::: moniker range="vs-2017"
    1. 从顶部菜单栏中选择“文件”>“新建”>“项目”    。

    1. 在“新建项目”对话框的左侧窗格中，展开“JavaScript”，然后选择“Node.js”  。

    1. 在中间窗格中，选择“空 Node.js Web 应用程序”，然后选择“确定” 。

    ::: moniker-end
    
    如果没有看到“空白 Node.js Web 应用程序”项目模板，必须添加 Node.js 开发工作负载。 有关详细说明，请参阅[先决条件](#prerequisites)。

    此时，Visual Studio 将创建并打开项目。 项目的 server.js 文件会在左侧编辑器中打开。

## <a name="explore-the-ide"></a>探索 IDE

1. 在右侧窗格中，查看“解决方案资源管理器”。

   ![解决方案资源管理器](../ide/media/quickstart-nodejs-solution-explorer.png)

   - 项目以粗体突出显示，其名称是在设置项目时提供的名称。 在磁盘上，此项目由项目文件夹中的 .njsproj 文件表示。

   - 顶层是一个解决方案，它与项目默认同名。 解决方案在磁盘上由 .sln 文件表示，是一个或多个相关项目的容器  。

   - npm 节点显示已安装的 npm 包。 可以右键单击 npm 节点搜索 npm 包，并使用对话框安装 npm 包。

1. 如果想要从命令提示符安装 npm 包或 Node.js 命令，请右键单击项目节点，然后选择“在此处打开命令提示符”。

   ![Node.js 命令提示符](../ide/media/quickstart-nodejs-command-prompt.png)

1. 如果要测试到源代码的导航，请从打开的 server.js 文件中选择 http.createServer 并按 F12，或从上下文（右键单击）菜单中选择“转到定义”  。 此命令将转到 http.d.ts 中 `createServer` 函数的定义。

   ![转到定义上下文菜单](../ide/media/quickstart-nodejs-gotodefinition.png)

1. 返回 server.js 并找到以下代码行：`res.end('Hello World\n');`。 按照如下修改代码：

    `res.end('Hello World\n' + res.connection.`

    键入“connection.”时，IntelliSense 会提供用于自动完成代码输入的选项。

   ![IntelliSense 自动完成](../ide/media/quickstart-nodejs-intellisense.png)

1. 选择“localPort”并键入“);”以完成语句 ：

    `res.end('Hello World\n' + res.connection.localPort);`

## <a name="run-the-app"></a>运行应用

1. 按 Ctrl + F5（或“调试” > “启动(不调试)”）运行应用  。 
 
   应用将在浏览器中打开。

1. 在浏览器中，验证是否看到“Hello World”消息和本地端口号。

恭喜！ 你使用 Visual Studio 创建了一个简单的 Node.js 应用。 要深入研究，请继续阅读目录的“教程”部分。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [将应用部署到 Linux 应用服务](../javascript/publish-nodejs-app-azure.md)

> [!div class="nextstepaction"]
> [Node.js 和 Express 教程](../javascript/tutorial-nodejs.md)

> [!div class="nextstepaction"]
> [Node.js 和 React 教程](../javascript/tutorial-nodejs-with-react-and-jsx.md)

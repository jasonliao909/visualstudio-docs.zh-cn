---
title: 创建 Node.js 和 React 应用
description: 了解如何从 Visual Studio 模板创建 Node.js Web 应用程序项目。
ms.custom: vs-acquisition
ms.date: 09/14/2021
ms.topic: tutorial
ms.devlang: javascript
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-javascript
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: 71ce14b60b3c935b06a4ea3fbdc1b7765ba3bc0b
ms.sourcegitcommit: da19ed1e48259b219c61c4cb9e98b006004a5766
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/21/2021
ms.locfileid: "128052867"
---
# <a name="tutorial-create-a-nodejs-and-react-app-in-visual-studio"></a>教程：在 Visual Studio 中创建 Node.js 和 React 应用

通过 Visual Studio 可以轻松创建 Node.js 项目并使用 IntelliSense 和其他支持 Node.js 的内置功能。 在本教程中，从 Visual Studio 模板创建 Node.js Web 应用项目。 然后，使用 React 创建一个简单的应用程序。

在本教程中，你将了解：
> [!div class="checklist"]
> * 创建 Node.js 项目
> * 添加 npm 包
> * 将 React 代码添加到应用
> * 转译 JSX
> * 附加调试器

在开始之前，下面是一个快速 FAQ，介绍一些关键概念：

- **什么是 Node.js？**
  
  Node.js 是执行 JavaScript 代码的服务器端 JavaScript 运行时环境。

- **什么是 npm？**
  
  Node.js 的默认包管理器是 npm。 包管理器使其易于发布和共享 Node.js 源代码库。 npm 包管理器可简化库的安装、更新和卸载。

- **什么是 React？**
  
  React 是用于创建用户界面 (UI) 的前端框架。

- **什么是 JSX？**
  
  JSX 是一个 JavaScript 语法扩展，通常用于 React 以描述 UI 元素。 必须将 JSX 代码转译为普通 JavaScript 方可在浏览器中运行。

- **什么是 webpack？**

  webpack 绑定 JavaScript 文件，使其可以在浏览器中运行，还可以转换或打包其他资源和资产。 Webpack 可以指定编译器（如 Babel 或 TypeScript），以将 JSX 或 TypeScript 代码转译为普通 JavaScript。

## <a name="prerequisites"></a>先决条件

本教程需要满足以下前提条件：

- 已安装 Node.js 开发工作负载的 Visual Studio。
  
  如果尚未安装 Visual Studio，请执行以下操作：
  
  1. 转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页，进行免费安装。
     
  1. 在 Visual Studio 安装程序中，选择“Node.js 开发”工作负载，然后选择“安装”。
     
     ![显示 Visual Studio 安装程序中选择的 Node.js 工作负载的屏幕截图。](media/quickstart-nodejs-workload.png)
  
  如果已安装 Visual Studio，但需要 Node.js 工作负载，请执行以下操作：
  
  1. 在 Visual Studio 中，转至“工具” > “获取工具和功能” 。
     
  1. 在 Visual Studio 安装程序中，选择“Node.js 开发”工作负载，然后选择“修改”以下载并安装工作负载。
  
- 安装的 Node.js 运行时：
  
  如果尚未安装 Node.js 运行时，请[从 Node.js 网站安装 LTS 版本](https://nodejs.org/en/download/)。 LTS 版本可以实现与外部框架和库的最佳兼容性。
  
  Visual Studio Node.js 工作负载中的 Node.js 工具同时支持 Node.js 32 位和 64 位体系结构版本。 Visual Studio 只需一个版本，并且 Node.js 安装程序一次只支持一个版本。
  
  Visual Studio 通常会自动检测已安装的 Node.js 运行时。 如果没有，则可配置项目来引用已安装的运行时：
  
  1. 创建项目后，右键单击项目节点并选择“属性”。
     
  1. 在“属性”窗格中，将“Node.exe 路径”设置为引用 Node.js 的全局或本地安装。 可以在每个 Node.js 项目中指定本地解释器的路径。

::: moniker range=">=vs-2022"
本教程已使用 Node.js 14.17.5 进行测试。
::: moniker-end
::: moniker range="<=vs-2019"
本教程已使用 Node.js 12.6.2 进行测试。
::: moniker-end

## <a name="create-a-project"></a>创建一个项目

首先，创建一个 Node.js Web 应用项目。

::: moniker range=">=vs-2022"
1. 打开 Visual Studio，然后按 Esc 关闭启动窗口。
   
1. 按 Ctrl+Q，在搜索框中键入 node.js，然后从下拉列表中选择“空白 Node.js Web 应用程序 - JavaScript”。
   
   尽管本教程使用的是 TypeScript 编译器，但这些步骤需要从 JavaScript 模板开始。
   
   如果未看到“空白 Node.js Web 应用程序”选项，则需要安装 Node.js 开发工作负载。 有关说明，请参阅[先决条件](#prerequisites)。
   
1. 在“配置新项目”对话框中，选择“创建”。
   
   Visual Studio 创建新的解决方案和项目并在右窗格中打开项目。 在左窗格的编辑器中打开 server.js 项目文件。
   
1. 查看右窗格的“解决方案资源管理器”中的项目结构。
   
   ![显示解决方案资源管理器中的 Node.js 项目结构的屏幕截图。](media/vs-2022/tutorial-nodejs-react-project-structure.png)
   
   - 顶层是一个解决方案 (1)，它与项目默认同名。 解决方案在磁盘上由 .sln 文件表示，是一个或多个相关项目的容器  。
   
   - 项目 (2)（使用你在“配置新项目”对话框中指定的名称）以粗体突出显示。 在文件系统中，此项目是项目文件夹中的 .njsproj 文件。
     
     若要查看和设置项目属性和环境变量，请按 Alt+Enter，或右键单击相应项目，然后从上下文菜单中选择“属性”。 可以使用其他开发工具，因为项目文件不对 Node.js 项目源做出自定义更改。
   
   - npm 节点 (3) 显示任何已安装的 npm 包。
   
     右键单击 npm 节点搜索 npm 包，并安装 npm 包。 可使用 package.json 中的设置来安装和更新包，并右键单击 npm 节点中的选项。
   
   - npm 使用 package.json 文件 (4) 管理本地安装包的依赖关系和版本。 有关详细信息，请参阅[管理 npm 包](npm-package-management.md)。
   
   - 项目文件 (5) 显示在项目节点下。 项目启动文件 server.js  以粗体显示。
     
     可设置启动文件，方法是右键单击项目中的文件并选择“设置为 Node.js 启动文件”  。
::: moniker-end
::: moniker range="vs-2019"
1. 打开 Visual Studio。

1. 创建新项目。

    按 Esc 关闭启动窗口  。 键入 Ctrl+Q  以打开搜索框，键入“Node.js”  ，然后选择“空白 Node.js Web 应用程序 - JavaScript”  。 （尽管本教程使用的是 TypeScript 编译器，但这些步骤需要从 JavaScript  模板开始。）
    
    在出现的对话框中，选择“创建”  。

    如果没有看到“空白 Node.js Web 应用程序”项目模板，  必须添加 Node.js 开发工作负载  。 有关详细说明，请参阅[先决条件](#prerequisites)。

    Visual Studio 创建新的解决方案并打开项目。

    ![显示解决方案资源管理器中的 Node.js 项目的屏幕截图](media/tutorial-nodejs-react-project-structure.png)

    (1) 粗体突出显示的是项目，其名称是在“新建项目”对话框中指定的名称   。 在文件系统中，此项目由项目文件夹中的 .njsproj 文件表示  。 可以通过右键单击项目并选择“属性”（或按 Alt + Enter），设置与项目关联的属性和环境变量。 可以使用其他开发工具执行往返，因为项目文件不对 Node.js 项目源做出自定义更改。

    (2) 顶层是一个解决方案，它与项目默认同名。 解决方案在磁盘上由 .sln 文件表示，是一个或多个相关项目的容器  。

    (3) Npm 节点显示任何已安装的 npm 包。 可右键单击 npm 节点以使用对话框搜索并安装 npm 包，也可使用 package.json 中的设置来安装和更新包，并右键单击 npm 节点中的选项  。

    (4) package.json 是 npm 用于管理本地安装包的包依赖关系和包版本的文件。 有关详细信息，请参阅[管理 npm 包](../javascript/npm-package-management.md)。

    (5) 项目文件（例如 server.js）显示在项目节点下  。 server.js 是项目启动文件，因此它以粗体形式显示   。 可设置启动文件，方法是右键单击项目中的文件并选择“设置为 Node.js 启动文件”  。
::: moniker-end
::: moniker range="vs-2017"
1. 打开 Visual Studio。

1. 创建新项目。

    从顶部菜单栏中选择“文件”   > “新建”   > “项目”  。 在“新建项目”对话框的左窗格中，展开“JavaScript”，然后选择“Node.js”    。 在中间窗格中，选择“空白 Node.js Web 应用程序”  ，键入名称“NodejsWebAppBlank”  ，然后选择“确定”  。

    如果没有看到“空白 Node.js Web 应用程序”项目模板，  必须添加 Node.js 开发工作负载  。 有关详细说明，请参阅[先决条件](#prerequisites)。

    Visual Studio 创建新的解决方案并打开项目。

    ![显示解决方案资源管理器中的 Node.js 项目的屏幕截图](media/tutorial-nodejs-react-project-structure.png)

    (1) 粗体突出显示的是项目，其名称是在“新建项目”对话框中指定的名称   。 在文件系统中，此项目由项目文件夹中的 .njsproj 文件表示  。 可以通过右键单击项目并选择“属性”（或按 Alt + Enter），设置与项目关联的属性和环境变量。 可以使用其他开发工具执行往返，因为项目文件不对 Node.js 项目源做出自定义更改。

    (2) 顶层是一个解决方案，它与项目默认同名。 解决方案在磁盘上由 .sln 文件表示，是一个或多个相关项目的容器  。

    (3) Npm 节点显示任何已安装的 npm 包。 可右键单击 npm 节点以使用对话框搜索并安装 npm 包，也可使用 package.json 中的设置来安装和更新包，并右键单击 npm 节点中的选项  。

    (4) package.json 是 npm 用于管理本地安装包的包依赖关系和包版本的文件。 有关详细信息，请参阅[管理 npm 包](../javascript/npm-package-management.md)。

    (5) 项目文件（例如 server.js）显示在项目节点下  。 server.js 是项目启动文件，因此它以粗体形式显示   。 可设置启动文件，方法是右键单击项目中的文件并选择“设置为 Node.js 启动文件”  。
::: moniker-end

## <a name="add-npm-packages"></a>添加 npm 包

此应用需要以下 npm 模块才能正常运行：

- react
- react-dom
- express
- path
- ts-loader
- typescript
- webpack
- webpack-cli

若要安装包，请执行以下操作：

1. 在“解决方案资源管理器”中，右键单击“npm”节点并选择“安装新的 npm 包”。
   
1. 在“安装新的 npm 包”对话框中，搜索 react 包并选择“安装包”进行安装。

    ::: moniker range=">=vs-2022"
    ![显示安装 npm 包的屏幕截图。](media/vs-2022/tutorial-nodejs-react-install-package.png)
    ::: moniker-end
    ::: moniker range="<=vs-2019"
    ![显示安装 npm 包的屏幕截图。](media/tutorial-nodejs-react-install-package.png)
    ::: moniker-end

    在“安装新的 npm 包”对话框中，可以选择安装最新的包版本，或者指定版本。 如果选择安装当前版本，但是之后发生意外错误，请尝试安装下一步中列出的包版本。

    Visual Studio 下部窗格中的“输出”窗口显示包安装进度。 通过选择“视图” > “输出”或按 Ctrl+Alt+O 来打开“输出”窗口。 在“输出”窗口的“显示输出来源”字段中，选择“Npm”。

    安装后，react 包会显示在“解决方案资源管理器”中的“npm”节点下。
    
    项目的 package.json 文件中的信息更新为新的包信息（包括包版本）。

将所需的包代码粘贴到 package.json，而不用使用 UI 一个一个搜索并添加其余的包。
    
1. 在“解决方案资源管理器”中，打开 Visual Studio 编辑器中的 package.json。 在文件末尾之前添加以下 `dependencies` 部分：

    ```json
    "dependencies": {
      "express": "~4.17.1",
      "path": "~0.12.7",
      "react": "~16.13.1",
      "react-dom": "~16.13.1",
      "ts-loader": "~7.0.1",
      "typescript": "~3.8.3",
      "webpack": "~4.42.1",
      "webpack-cli": "~3.3.11"
    }
    ```

    如果文件已有 `dependencies` 部分，请将其替换为前面的 JSON 代码。 有关使用 package.json 文件的详细信息，请参阅 [package.json 配置](configure-packages-with-package-json.md)。

1. 按 Ctrl+S 或选择“文件” > “保存 package.json”以保存更改。

1. 在“解决方案资源管理器”中，右键单击项目中的“npm”节点并选择“安装 npm 包”。

    此命令直接运行 npm 安装命令以安装 package.json 中列出的所有包。

    选择下部窗格中的“输出”窗口以查看安装进度。 安装可能需要几分钟时间，可能无法立即看到结果。 请确保在“输出”窗口的“显示输出来源”字段中选择“Npm”。

    安装后，npm 模块会显示在“解决方案资源管理器”的“npm”节点中。

    ::: moniker range=">=vs-2022"
    ![显示安装 npm 包的屏幕截图。](media/vs-2022/tutorial-nodejs-react-npm-modules-installed.png)
    ::: moniker-end
    ::: moniker range="<=vs-2019"
    ![显示安装 npm 包的屏幕截图。](media/tutorial-nodejs-react-npm-modules-installed.png)
    ::: moniker-end

    > [!NOTE]
    > 还可以使用命令行安装 npm 包。 在“解决方案资源管理器”中，右键单击项目名称，并选择“在此处打开命令提示符”。 使用标准的 Node.js 命令安装包。

## <a name="add-project-files"></a>添加项目文件

接下来，为项目添加四个新文件。

- *app.tsx*
- *webpack-config.js*
- index.html 
- *tsconfig.json*

对于此简单应用，将新建项目文件添加到项目根中。 对于大多数应用，将文件添加到子文件夹并相应调整相对路径引用。

1. 在“解决方案资源管理器”中，选择项目名称并按 Ctrl+Shift+A，或右键单击项目名称并选择“添加” > “新建项”。

1. 在“添加新项”对话框中，选择“TypeScript JSX 文件”，键入名称“app.tsx”，然后选择“添加”或“确定”。

1. 重复上述步骤，添加一个名为 webpack-config.js 的 JavaScript 文件。

1. 重复上述步骤，添加一个名为 index.html 的 HTML 文件。

1. 重复上述步骤，添加一个名为 tsconfig.json 的 TypeScript JSON 配置文件。

## <a name="add-app-code"></a>添加应用代码

1. 在“解决方案资源管理器”中，打开 server.js 并将现有代码替换为以下代码：

    ```javascript
    'use strict';
    var path = require('path');
    var express = require('express');

    var app = express();

    var staticPath = path.join(__dirname, '/');
    app.use(express.static(staticPath));

    // Allows you to set port in the project properties.
    app.set('port', process.env.PORT || 3000);

    var server = app.listen(app.get('port'), function() {
        console.log('listening');
    });
    ```

   前面的代码使用 Express 启动 Node.js 作为 Web 应用程序服务器。 此代码将端口设置为在项目属性中配置的端口号（默认为 1337）。 如果需要打开项目属性，请右键单击“解决方案资源管理器”中的项目名称，然后选择“属性”。

1. 打开 app.tsx 并添加以下代码  ：

    ```javascript
    declare var require: any

    var React = require('react');
    var ReactDOM = require('react-dom');

    export class Hello extends React.Component {
        render() {
            return (
                <h1>Welcome to React!!</h1>
            );
        }
    }

    ReactDOM.render(<Hello />, document.getElementById('root'));
    ```

    前面的代码使用 JSX 语法和 React 显示消息。

1. 打开 index.html 并将 `body` 部分替换为以下代码：

    ```html
    <body>
        <div id="root"></div>
        <!-- scripts -->
        <script src="./dist/app-bundle.js"></script>
    </body>
    ```

    此 HTML 页加载 app-bundle.js，其中包含转译为纯文本 JavaScript 的 JSX 和 React 代码  。 目前，app-bundle.js 是一个空文件  。 在下一部分中，将配置选项以转译代码。

## <a name="configure-webpack-and-typescript-compiler-options"></a>配置 webpack 和 TypeScript 编译器选项

接下来，将 webpack 配置代码添加到 webpack-config.js。 将添加一个简单的 webpack 配置，以指定输入文件 app.tsx 和输出文件 app-bundle.js，用于捆绑 JSX 并将其转译为纯文本 JavaScript。 为进行转译，还要配置某些 TypeScript 编译器选项。 此基本配置代码是有关 webpack 和 TypeScript 编译器的简介。

1. 在“解决方案资源管理器”中，打开 webpack-config.js 并添加以下代码。

    ```json
    module.exports = {
        devtool: 'source-map',
        entry: "./app.tsx",
        mode: "development",
        output: {
            filename: "./app-bundle.js"
        },
        resolve: {
            extensions: ['.Webpack.js', '.web.js', '.ts', '.js', '.jsx', '.tsx']
        },
        module: {
            rules: [
                {
                    test: /\.tsx$/,
                    exclude: /(node_modules|bower_components)/,
                    use: {
                        loader: 'ts-loader'
                    }
                }
            ]
        }
    }
    ```

    webpack 配置代码指示 webpack 使用 TypeScript 加载程序转译 JSX。

1. 打开 tsconfig.json 并使用以下代码替换内容，以下代码指定 TypeScript 编译器选项：

    ```json
    {
      "compilerOptions": {
        "noImplicitAny": false,
        "module": "commonjs",
        "noEmitOnError": true,
        "removeComments": false,
        "sourceMap": true,
        "target": "es5",
        "jsx": "react"
      },
      "exclude": [
        "node_modules"
      ],
      "files": [
        "app.tsx"
      ]
    }
    ```

    该代码将 app.tsx 指定为源文件。

1. 按 Ctrl+Shift+S 或选择“文件” > “全部保存”以保存所有更改。

## <a name="transpile-the-jsx"></a>转译 JSX

1. 在“解决方案资源管理器”中，右键单击项目名称，并选择“在此处打开命令提示符”。

1. 在命令提示符下，输入以下 webpack 命令：

    `node_modules\.bin\webpack ./app.tsx --config webpack-config.js`

    命令提示符窗口显示结果。

    ![显示运行 webpack 命令的结果的屏幕截图。](media/tutorial-nodejs-react-run-webpack-cmd.png)

    如果看到错误而不是前面的输出，则必须在应用开始运行之前解决这些错误。 如果 npm 包版本不是本教程指定的版本，则可能引发错误。 修复错误的一种方法是使用前面步骤中使用的版本。
    
    此外，如果一个或多个包版本是已弃用的版本，并导致发生错误，则可能需要安装较新版本以消除错误。 有关使用 package.json  控制 npm 包版本的信息，请参阅 [package.json 配置](../javascript/configure-packages-with-package-json.md)。

1. 在“解决方案资源管理器”中，右键单击项目节点并选择“添加” > “现有文件夹”。

1. 选择 dist 文件夹，然后选择“选择文件夹”。

    Visual Studio 将 dist 文件夹添加到项目中，其中包含 app-bundle.js 和 app-bundle.js.map。

1. 打开 app-bundle.js，查看转译的 JavaScript 代码  。

1. 如果系统提示是否从外部重新加载已修改的文件，请选择“全是”。

    ![显示是否加载已修改文件的提示的屏幕截图。](media/tutorial-nodejs-react-reload-files.png)

每次对 app.tsx 进行更改时，必须重新运行 webpack 命令。 若要自动执行此步骤，可以添加一个生成脚本来转译 JSX。

### <a name="add-a-build-script-to-transpile-the-jsx"></a>添加用于转译 JSX 的生成脚本

从 Visual Studio 2019 开始的 Visual Studio 版本需要生成脚本。 不是在命令行转译 JSX（如上一节所示），而是在使用 Visual Studio 生成时转译 JSX。

1. 打开 package.json  并在 `dependencies` 部分后添加以下部分：

   ```json
   "scripts": {
    "build": "webpack-cli ./app.tsx --config webpack-config.js"
   }
   ```

1. 保存所做更改。

## <a name="run-the-app"></a>运行应用

1. 在“调试”工具栏中，选择“Web 服务器(Microsoft Edge)”或“Web 服务器(Google Chrome)”作为调试目标。

    ::: moniker range=">=vs-2022"
    ![显示选择“Microsoft Edge”作为调试目标的屏幕截图。](media/vs-2022/tutorial-nodejs-react-debug-target.png)
    ::: moniker-end
    ::: moniker range="=vs-2019"
    ![显示选择“Chrome”作为调试目标的屏幕截图。](media/vs-2019/tutorial-nodejs-react-debug-target.png)
    ::: moniker-end
    ::: moniker range="vs-2017"
    ![显示选择“Chrome”作为调试目标的屏幕截图。](media/tutorial-nodejs-react-debug-target.png)
    ::: moniker-end

    如果你知道计算机上有首选调试目标，但未显示为选项，请从调试目标下拉列表中选择“浏览方式”。 在列表中选择默认浏览器目标，然后选择“设为默认值”。

1. 若要运行应用，请按 F5，选择绿色箭头按钮，或选择“调试” > “开始调试”。

    此时 Node.js 控制台窗口打开，并显示调试器正在侦听的端口。

    Visual Studio 通过启动启动文件 server.js 来启动应用  。

    ![显示在浏览器中运行 React 的屏幕截图。](media/tutorial-nodejs-react-running-react.png)

1. 关闭浏览器和控制台窗口。

## <a name="set-a-breakpoint-and-run-the-app"></a>设置断点并运行应用

断点是可靠调试的最基本和最重要的功能。 断点指示 Visual Studio 应在哪个位置挂起你的运行代码。 你便可以查看变量的值或内存的行为，或确定代码的分支是否运行。

1. 在 server.js 中，单击 `staticPath` 声明左侧的滚动条槽以设置断点  ：

    ::: moniker range=">=vs-2022"
    ![显示为 server.js 中 staticPath 声明设置的断点的屏幕截图。](media/vs-2022/tutorial-nodejs-react-set-breakpoint.png)
    ::: moniker-end
    ::: moniker range="<=vs-2019"
    ![显示为 server.js 中 staticPath 声明设置的断点的屏幕截图。](media/tutorial-nodejs-react-set-breakpoint.png)
    ::: moniker-end

1. 若要运行应用，请按 F5 或选择“调试” > “启动调试”。

    调试器将在设置的断点处暂停（当前语句突出显示）。 现在，可使用调试程序窗口（例如“局部变量”和“监视”窗口），通过将鼠标悬停在当前范围内的变量上来检查应用的状态 。

1. 若要继续运行应用，请按 F5，在“调试”工具栏中选择“继续”，或选择“调试” > “继续”。

   如果想要使用 Chrome 开发人员工具或 Microsoft Edge 的 F12 工具，请按“F12”  。 可使用这些工具检查 DOM 并与使用 JavaScript 控制台的应用进行交互。

1. 关闭浏览器和控制台窗口。

## <a name="set-and-hit-a-breakpoint-in-the-client-side-react-code"></a>设置并命中客户端 React 代码中的断点

在前面的部分中，已将调试器附加到服务器端 Node.js 代码。 若要在客户端 React 代码中附加并命中断点，必须将调试器附加到正确的进程。 下面是启用浏览器并附加用于调试的进程的一种方法。

### <a name="enable-the-browser-for-debugging"></a>启用浏览器以进行调试

::: moniker range=">=vs-2019"
可以使用 Microsoft Edge 或 Google Chrome。 关闭目标浏览器的所有窗口。 对于 Microsoft Edge，还需要关闭所有 Chrome 实例。 由于两个浏览器共享 Chromium 基本代码，因此关闭两个浏览器可获得最佳结果。

其他浏览器实例可能会阻止打开浏览器并阻止调试。 浏览器扩展可能阻止完整的调试模式。 可能需要使用任务管理器查找并结束所有正在运行的 Chrome 实例。

若要在启动浏览器时同时启用调试，请执行以下操作：

1. 从“调试”工具栏的下拉列表中选择“浏览方式”。 
   
1. 在“浏览方式”屏幕（突出显示了首选浏览器）上，选择“添加”。
   
1. 在“参数”字段中输入“--remote-debugging-port=9222”标志。
   
1. 为浏览器指定新的易记名称（如“带有调试功能的 Edge”或“带有调试功能的 Chrome”），然后选择“确定”。
   
1. 在“浏览方式”屏幕上，选择“浏览”。

    ![显示创建启用了调试功能的 Edge 浏览器的屏幕截图。](media/tutorial-nodejs-react-edge-with-debugging.png)

- 或者，可以通过右键单击 Windows“启动”按钮来打开“运行”命令，然后输入：
  
  `msedge --remote-debugging-port=9222`
  
  或
  
  `chrome.exe --remote-debugging-port=9222`
::: moniker-end

::: moniker range="vs-2017"
对于此方案，请选择 Chrome。

1. 关闭所有 Chrome 浏览器窗口。

   其他浏览器实例可能会阻止打开浏览器并阻止调试。 浏览器扩展可能阻止完整的调试模式。 可能需要打开任务管理器来查找所有正在运行的 Chrome 实例。

2. 启动浏览器并启用调试。

    从 Windows“启动”按钮打开“运行”命令（右键单击并选择“运行”），然后输入以下命令  ：

    `chrome.exe --remote-debugging-port=9222`
::: moniker-end

启动浏览器并启用调试。 应用尚未运行，因此浏览器页面为空。

### <a name="attach-the-debugger-to-client-side-script"></a>将调试器附加到客户端脚本

1. 在 Visual Studio 编辑器中，在 app-bundle.js 或 app.tsx 源代码中设置断点。

    - 对于 app-bundle.js，在 `render()` 函数中设置断点。 若要查找 app-bundle.js文件中的 `render()` 函数，请按 Ctrl+F 或选择“编辑” > “查找和替换” > “快速查找”，然后在搜索字段中输入“render”。

      ::: moniker range=">=vs-2022"
      ![显示在 app-bundle.js 的 render 函数中设置的断点的屏幕截图。](media/vs-2022/tutorial-nodejs-react-set-breakpoint-client-code.png)
      ::: moniker-end
      ::: moniker range="<=vs-2019"
      ![显示在 app-bundle.js 的 render 函数中设置的断点的屏幕截图。](media/tutorial-nodejs-react-set-breakpoint-client-code.png)
      ::: moniker-end

    - 对于 app.tsx  ，在 `return` 语句上的 `render()` 函数中设置断点。

      ::: moniker range=">=vs-2022"
      ![显示在 app.tsx 中 render 函数的 return 语句上设置的断点的屏幕截图。](media/vs-2022/tutorial-nodejs-react-set-breakpoint-tsx-file.png)
      ::: moniker-end
      ::: moniker range="<=vs-2019"
      ![显示在 app.tsx 中 render 函数的 return 语句上设置的断点的屏幕截图。](media/tutorial-nodejs-react-set-breakpoint-in-tsx-file.png)
      ::: moniker-end

      如果在 app.tsx 中设置断点，则还需要更新 webpack-config.js 以替换以下代码，并保存所做的更改。

      替换此代码：

      ```javascript
      output: {
          filename: "./app-bundle.js",
      },
      ```

      替换为以下代码：

      ```javascript
      output: {
          filename: "./app-bundle.js",
          devtoolModuleFilenameTemplate: '[resource-path]'  // removes the webpack:/// prefix
      },
      ```

      此设置仅用于开发，可在 Visual Studio 中启用调试。 默认情况下，源映射文件中的 webpack 引用包括 webpack:/// 前缀，该前缀会阻止 Visual Studio 查找源文件 app.tsx。 通过此设置可以在生成应用时覆盖源映射文件 app-bundle.js.map 中生成的引用。 具体而言，此设置将对源文件的引用从 webpack:///./app.tsx 更改为 ./app.tsx，这将启用调试。

1. 选择目标浏览器作为 Visual Studio 中的调试目标，然后按 Ctrl+F5，或选择“调试” > “启动时不调试”以在浏览器中运行应用。

    ::: moniker range=">=vs-2019"
    如果创建了已启用调试且具有易记名称的浏览器配置，请选择该浏览器作为调试目标。
    ::: moniker-end

    应用随即在新的浏览器选项卡中打开。

1. 依次选择“调试” > “附加到进程”，或按 Ctrl+Alt+P。

    > [!TIP]
    > 首次附加到进程后，可选择“调试” > “重新附加到进程”或按 Shift+Alt+P，快速重新附加到同一进程。

1. 在“附加到进程”对话框中，获取可附加到的浏览器实例的筛选列表。

    ::: moniker range=">=vs-2019"
    请确保目标浏览器 JavaScript (Chrome) 或 JavaScript (Microsoft Edge - Chromium) 的正确调试器显示在“附加到”字段中。 在“筛选器”框中键入“chrome”或“edge”以筛选结果。
    ::: moniker-end
    ::: moniker range="vs-2017"
    在 Visual Studio 2017 中，选择“附加到”字段中的“WebKit 代码”。  在“筛选器”框中键入“chrome”以筛选搜索结果。
    ::: moniker-end

1. 使用正确的主机端口（此例中为 localhost）选择浏览器进程。 端口 1337 或 localhost 也可能出现在“标题”字段中，以帮助你选择正确的进程。

1. 选择“附加”。

    ::: moniker range=">=vs-2019"
    以下示例显示 Microsoft Edge 浏览器的“附加到进程”窗口。

    ![显示“附加到进程”对话框的屏幕截图。](../javascript/media/tutorial-nodejs-react-attach-to-process-edge.png)
    ::: moniker-end
    ::: moniker range="vs-2017"
    ![显示“附加到进程”对话框的屏幕截图。](../javascript/media/tutorial-nodejs-react-attach-to-process.png)

    当正确附加调试器时，表明 DOM 资源管理器和 JavaScript 控制台在 Visual Studio 中打开。 这些调试工具类似于 Chrome 开发人员工具和 Microsoft Edge 的 F12 工具。
    ::: moniker-end

    > [!TIP]
    > 如果未附加调试器，并且看到消息“无法附加到进程。操作在当前状态中是非法的。”，则在调试模式中启用浏览器前，先使用任务管理器关闭所有目标浏览器实例。 浏览器扩展可能正在运行并阻止完整的调试模式。

1. 由于已执行有断点的代码，因此要刷新浏览器页面以命中断点。

    可能会在 app-bundle.js 中或在 app.tsx 中断点的映射位置处命中断点，具体取决于环境、浏览器状态以及之前执行的步骤。 无论在哪里命中，均可单步执行代码并检查变量。

    暂停调试器时，可以通过在变量上悬停光标并使用调试器窗口，检查应用状态。 若要单步执行代码，请按 F11 或选择“调试” > “单步执行”，或者按 F10 或选择“调试” > “单步跳过”。 若要继续运行代码，请按 F5 或选择“继续”。 有关基本调试功能的详细信息，请参阅[初探调试器](../debugger/debugger-feature-tour.md)。

   - 如果无法中断 app.tsx 中的代码，请按照之前所述的步骤，使用“附加到进程”来附加调试器。 请确保已正确设置环境：

      - 使用任务管理器关闭所有浏览器实例，包括 Chrome 扩展。 请确保在调试模式下启动浏览器。

      - 请确保源映射文件包括对 ./app.tsx 的引用（而不包括 webpack:///./app.tsx），该引用会阻止 Visual Studio 调试器查找 app.tsx。

     或者，尝试使用 app.tsx 中的 `debugger;` 语句或改为在 Chrome 开发人员工具（或 Microsoft Edge 的 F12 工具）中设置断点。

   - 如果无法中断 app-bundle.js 中的代码，请删除 sourcemap 文件 app-bundle.js.map。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [将应用部署到 Linux 应用服务](../javascript/publish-nodejs-app-azure.md)

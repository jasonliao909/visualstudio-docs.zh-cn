---
title: 创建 Node.js 和 Express 应用
description: 在本教程中，了解如何在 Visual Studio 中使用 Express Web 应用程序框架创建简单的 Node.js 应用程序。
ms.date: 09/14/2021
ms.custom: vs-acquisition
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
ms.openlocfilehash: 0dbd5b8cd41e3839c7b3c34521bc537b12b5143b
ms.sourcegitcommit: 8e74969ff61b609c89b3139434dff5a742c18ff4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2021
ms.locfileid: "128430316"
---
# <a name="tutorial-create-a-nodejs-and-express-app-in-visual-studio"></a>教程：在 Visual Studio 中创建 Node.js 和 Express 应用

本 Visual Studio 开发教程使用 Node.js 和 Express。 在本教程中，你将创建一个简单的 Node.js Web 应用，添加一些代码，探索 IDE 的某些功能，然后运行该应用。 

在本教程中，你将了解：

> [!div class="checklist"]
> * 创建 Node.js 项目
> * 添加一些代码
> * 使用 IntelliSense 编辑代码
> * 运行应用
> * 命中调试程序中的断点

在开始之前，下面是一个快速 FAQ，介绍一些关键概念：

- **什么是 Node.js？**
  
  Node.js 是执行 JavaScript 代码的服务器端 JavaScript 运行时环境。

- **什么是 npm？**
  
  包管理器使其易于发布和共享 Node.js 源代码库。 Node.js 的默认包管理器是 npm。 npm 包管理器可简化库的安装、更新和卸载。

- Express 是什么？
  
  Express 是一个服务器 Web 应用程序框架，Node.js 使用它来生成 Web 应用。 借助 Express，可以使用不同的前端框架创建用户界面。 本教程使用 Pug（以前称为 Jade）作为前端框架。

## <a name="prerequisites"></a>先决条件

本教程需要满足以下前提条件：

- 已安装 Node.js 开发工作负载的 Visual Studio。
  
  如果尚未安装 Visual Studio，请执行以下操作：
  
  1. 转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页，进行免费安装。
     
  1. 在 Visual Studio 安装程序中，选择“Node.js 开发”工作负载，然后选择“安装”。
     
     ![显示 Visual Studio 安装程序中选择的 Node.js 工作负载的屏幕截图。](media/quickstart-nodejs-workload.png)
  
  如果已安装 Visual Studio：
  
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
本教程已使用 Node.js 8.10.0 进行测试。
::: moniker-end

## <a name="create-a-new-nodejs-project"></a>创建新的 Node.js 项目

Visual Studio 管理项目中的单个应用程序的文件  。 该项目包括源代码、资源和配置文件。

在本教程中，你将从一个包含 Node.js 和 Express 应用代码的简单项目开始。

::: moniker range=">=vs-2022"
1. 打开 Visual Studio，然后按 Esc 关闭启动窗口。
   
1. 按 Ctrl+Q，在搜索框中键入“node.js”，然后从下拉列表中选择“基本 Azure Node.js Express 4 应用程序 - JavaScript” 。
   
   如果未看到“基本 Azure Node.js Express 4 应用程序”选项，则需要安装“Node.js 开发”工作负载。 有关说明，请参阅[先决条件](#prerequisites)。
   
1. 在“配置新项目”对话框中，选择“创建”。
   
   Visual Studio 创建新的解决方案和项目并在右窗格中打开项目。 app.js 项目文件将在左侧窗格的编辑器中打开。
   
1. 查看右窗格的“解决方案资源管理器”中的项目结构。
   
   ![显示解决方案资源管理器中的项目结构的屏幕截图。](media/vs-2022/tutorial-project-structure.png)
   
   - 顶层是一个解决方案 (1)，它与项目默认同名。 解决方案在磁盘上由 .sln 文件表示，是一个或多个相关项目的容器  。
   
   - 项目 (2)（使用你在“配置新项目”对话框中指定的名称）以粗体突出显示。 在文件系统中，此项目是项目文件夹中的 .njsproj 文件。
     
     可以右键单击该项目并从上下文菜单中选择“属性”，来查看和设置项目属性与环境变量。 可以使用其他开发工具，因为项目文件不对 Node.js 项目源做出自定义更改。
   
   - npm 节点 (3) 显示任何已安装的 npm 包。 可以右键单击 npm 节点以搜索 npm 包，并使用对话框安装 npm 包。
     
     可使用 package.json 中的设置来安装和更新包，并右键单击 npm 节点中的选项。
   
   - 项目文件 (4) 将显示在项目节点下。 项目启动文件 app.js 以粗体显示。
     
     可设置启动文件，方法是右键单击项目中的文件并选择“设置为 Node.js 启动文件”  。

   - npm 使用 package.json 文件 (5) 来管理本地安装的包的依赖项和版本 。 有关详细信息，请参阅[管理 npm 包](npm-package-management.md)。
   
1. 打开“npm”节点，确保其中存在所有必需的 npm 包。
   
   如果有任何包显示为“(缺少)”，请右键单击“npm”节点并选择“安装 npm 包”，然后安装缺少的包  。
:::moniker-end
:::moniker range="vs-2019"
1. 打开 Visual Studio。

1. 创建新项目。

    按 Esc 关闭启动窗口  。 键入 Ctrl+Q 以打开搜索框，键入“Node.js”，然后选择“创建新的基本 Azure Node.js Express 4 应用程序”(JavaScript)    。 在出现的对话框中，选择“创建”  。
    
    如果未看到“基本 Azure Node.js Express 4 应用程序”项目模板，必须添加 Node.js 开发工作负载   。 有关说明，请参阅[先决条件](#prerequisites)。

    Visual Studio 创建新的解决方案并在右窗格中打开项目。 在编辑器（左窗格）中打开 App.js  项目文件。

    ![显示解决方案资源管理器中的项目结构的屏幕截图。](../javascript/media/tutorial-project-structure.png)

    (1) 粗体突出显示的是项目，其名称是在“新建项目”对话框中指定的名称   。 在文件系统中，此项目由项目文件夹中的 .njsproj 文件表示  。 可以右键单击项目并选择“属性”，设置与项目相关的属性和环境变量  。 可以使用其他开发工具执行往返，因为项目文件不对 Node.js 项目源做出自定义更改。

    (2) 顶层是一个解决方案，它与项目默认同名。 解决方案在磁盘上由 .sln 文件表示，是一个或多个相关项目的容器  。

    (3) Npm 节点显示任何已安装的 npm 包。 可右键单击 npm 节点以使用对话框搜索并安装 npm 包，也可使用 package.json 中的设置来安装和更新包，并右键单击 npm 节点中的选项  。

    (4) package.json 是 npm 用于管理本地安装包的包依赖关系和包版本的文件。 有关详细信息，请参阅[管理 npm 包](../javascript/npm-package-management.md)。

    (5) 项目文件（例如 app.js）显示在项目节点下  。 app.js 是项目启动文件，因此它以粗体形式显示   。 可设置启动文件，方法是右键单击项目中的文件并选择“设置为 Node.js 启动文件”  。

1. 打开“npm”节点，确保其中存在所有必需的 npm 包  。

    如果缺少任何包（感叹号图标），可右键单击“npm”节点并选择“安装 npm 包”   。
:::moniker-end
:::moniker range="vs-2017"
1. 打开 Visual Studio。

1. 创建新项目。

    从顶部菜单栏中选择“文件”   > “新建”   > “项目”  。 在“新建项目”对话框的左窗格中，展开“JavaScript”，然后选择“Node.js”    。 在中间窗格中，选择“基本 Azure Node.js Express 4 应用程序”，然后选择“确定”   。
    
    如果未看到“基本 Azure Node.js Express 4 应用程序”项目模板，必须添加 Node.js 开发工作负载   。 有关说明，请参阅[先决条件](#prerequisites)。

    Visual Studio 创建新的解决方案并在右窗格中打开项目。 在编辑器（左窗格）中打开 App.js  项目文件。

    ![显示解决方案资源管理器中的项目结构的屏幕截图。](../javascript/media/tutorial-project-structure.png)

    (1) 粗体突出显示的是项目，其名称是在“新建项目”对话框中指定的名称   。 在文件系统中，此项目由项目文件夹中的 .njsproj 文件表示  。 可以右键单击项目并选择“属性”，设置与项目相关的属性和环境变量  。 可以使用其他开发工具执行往返，因为项目文件不对 Node.js 项目源做出自定义更改。

    (2) 顶层是一个解决方案，它与项目默认同名。 解决方案在磁盘上由 .sln 文件表示，是一个或多个相关项目的容器  。

    (3) Npm 节点显示任何已安装的 npm 包。 可右键单击 npm 节点以使用对话框搜索并安装 npm 包，也可使用 package.json 中的设置来安装和更新包，并右键单击 npm 节点中的选项  。

    (4) package.json 是 npm 用于管理本地安装包的包依赖关系和包版本的文件。 有关详细信息，请参阅[管理 npm 包](../javascript/npm-package-management.md)。

    (5) 项目文件（例如 app.js）显示在项目节点下  。 app.js 是项目启动文件，因此它以粗体形式显示   。 可设置启动文件，方法是右键单击项目中的文件并选择“设置为 Node.js 启动文件”  。

1. 打开“npm”节点，确保其中存在所有必需的 npm 包  。

    如果缺少任何包（感叹号图标），可右键单击“npm”节点并选择“安装 npm 包”   。
    ::: moniker-end

## <a name="add-some-code"></a>添加一些代码

该应用程序将 Pug 用于前端 JavaScript 框架。 Pug 使用编译为 HTML 的简单标记代码。

在 app.js 中使用代码 `app.set('view engine', 'pug');` 将 Pug 设置为视图引擎。

1. 在“解决方案资源管理器”中打开“views”文件夹，然后选择“index.pug”打开该文件  。

1. 将文件内容替换为以下标记。

    ```js
    extends layout

    block content
      h1= title
      p Welcome to #{title}
      script.
        var f1 = function() { document.getElementById('myImage').src='#{data.item1}' }
      script.
        var f2 = function() { document.getElementById('myImage').src='#{data.item2}' }
      script.
        var f3 = function() { document.getElementById('myImage').src='#{data.item3}' }

      button(onclick='f1()') One!
      button(onclick='f2()') Two!
      button(onclick='f3()') Three!
      p
      a: img(id='myImage' height='300' width='300' src='')
    ```

    上面的代码会动态生成包含标题和欢迎消息的 HTML 页面。 该页面还包含代码，用于显示每当按一个按钮时就会更改的图像。

1. 在“routes”文件夹中打开“index.js” 。

1. 在 `router.get` 函数调用的前面添加以下代码：

    ```js
    var getData = function () {
        var data = {
            'item1': 'https://images.unsplash.com/photo-1563422156298-c778a278f9a5',
            'item2': 'https://images.unsplash.com/photo-1620173834206-c029bf322dba',
            'item3': 'https://images.unsplash.com/photo-1602491673980-73aa38de027a'
        }
        return data;
    }
    ````

    此代码创建一个数据对象，将其传递给动态生成的 HTML 页面。

1. 使用以下代码替换 `router.get` 函数调用：

    ```js
    router.get('/', function (req, res) {
        res.render('index', { title: 'Express', "data" });
    });
    ```

    之前的代码使用 Express 路由器对象设置当前页并呈现该页，将标题和数据对象传递给页面。 该代码将 index.pug 文件指定为运行 index.js 时要加载的页面 。 app.js 代码（此处未显示）将 index.js 配置为默认路由 。

    为了演示 Visual Studio 的几项功能，我们特意让一个错误存在于包含 `res.render` 的代码行中。 在下一部分，IntelliSense 可帮助你修复该错误，使应用能够运行。

## <a name="use-intellisense"></a>使用 IntelliSense

IntelliSense 是可以帮助你编写代码的 Visual Studio 工具。

1. 在 Visual Studio 代码编辑器内的 index.js 中，转到包含 `res.render` 的代码行。

1. 将光标置于 `"data"` 字符串和 `: get` 类型后面。 IntelliSense 将显示你先前在代码中定义的 `getData` 函数。 选择 `getData`。

    ::: moniker range=">=vs-2022"
    ![显示如何使用 IntelliSense 的屏幕截图。](media/vs-2022/tutorial-nodejs-intellisense.png)
    ::: moniker-end
    ::: moniker range="<=vs-2019"
    ![显示如何使用 IntelliSense 的屏幕截图。](../javascript/media/tutorial-nodejs-intellisense.png)
    ::: moniker-end

1. 添加括号，使代码成为函数调用：`getData()`。

1. 删除 `"data"` 前面的逗号。 表达式中将以绿色突出显示语法。 将鼠标悬停在语法突出显示上。

    ::: moniker range=">=vs-2022"
    ![显示 IntelliSense 中的语法错误的屏幕截图。](media/vs-2022/tutorial-nodejs-syntax-checking.png)
    ::: moniker-end
    ::: moniker range="<=vs-2019"
    ![显示 IntelliSense 中的语法错误的屏幕截图。](../javascript/media/tutorial-nodejs-syntax-checking.png)
    ::: moniker-end

    消息的最后一行告知，JavaScript 解释器需要一个逗号。

1. 在下方的窗格中，选择“错误列表”选项卡，然后从下拉列表中为报告的问题类型选择“生成 + IntelliSense” 。

    窗格中会显示警告和说明，以及文件名和行号。

    ::: moniker range=">=vs-2022"
    ![显示“错误列表”窗格的屏幕截图，其中列出了错误。](media/vs-2022/tutorial-nodejs-error-list.png)
    ::: moniker-end
    ::: moniker range="<=vs-2019"
    ![显示“错误列表”窗格的屏幕截图，其中列出了错误。](../javascript/media/tutorial-nodejs-error-list.png)
    ::: moniker-end

1. 在 `"data"` 前面添加逗号以修复代码。

    更正后的代码行应如下所示：`res.render('index', { title: 'Express', "data": getData() });`

## <a name="run-the-app"></a>运行应用

接下来，在附加了 Visual Studio 调试器的情况下运行应用。 在执行该操作之前，需要设置断点。

### <a name="set-a-breakpoint"></a>设置断点

断点是可靠调试的最基本和最重要的功能。 断点指示 Visual Studio 应在哪个位置挂起你的运行代码。 你便可以查看变量的值或内存的行为，或确定代码的分支是否运行。

- 若要设置断点，请在 index.js 中单击以下代码行前面的左装订线：

  `res.render('index', { title: 'Express', "data": getData() });`

  ::: moniker range=">=vs-2022"
  ![显示如何设置断点的屏幕截图。](media/vs-2022/tutorial-nodejs-set-breakpoint.png)
  ::: moniker-end
  ::: moniker range="<=vs-2019"
  ![显示如何设置断点的屏幕截图。](../javascript/media/tutorial-nodejs-set-breakpoint.png)
  ::: moniker-end

### <a name="run-the-app-in-debug-mode"></a>在调试模式下运行应用

1. 在“调试”工具栏中选择调试目标，例如“Web 服务器(Google Chrome)”或“Web 服务器(Microsoft Edge)”  。

    ::: moniker range=">=vs-2022"
    ![显示如何选择调试目标的屏幕截图。](media/vs-2022/tutorial-nodejs-deploy-target.png)
    ::: moniker-end
    ::: moniker range="vs-2019"
    ![显示如何选择调试目标的屏幕截图。](../javascript/media/vs-2019/tutorial-nodejs-deploy-target.png)
    ::: moniker-end
    ::: moniker range="vs-2017"
    ![显示如何选择调试目标的屏幕截图。](../javascript/media/tutorial-nodejs-deploy-target.png)
    ::: moniker-end

    如果你知道计算机上有首选调试目标，但未显示为选项，请从调试目标下拉列表中选择“浏览方式”。 在列表中选择默认浏览器目标，然后选择“设为默认值”。

1. 按 F5 或选择“调试” > “开始调试”以运行应用  。

    调试器将在设置的断点处暂停，因此你可以检查应用状态。

1. 将鼠标悬停在 `getData` 上，在数据提示中查看其属性：

    ::: moniker range=">=vs-2022"
    [![显示如何在调试期间检查变量的屏幕截图。](media/vs-2022/tutorial-nodejs-inspect-variables.png)](media/vs-2022/tutorial-nodejs-inspect-variables.png#lightbox)
    ::: moniker-end
    ::: moniker range="<=vs-2019"
    ![显示如何在调试期间检查变量的屏幕截图。](../javascript/media/tutorial-nodejs-inspect-variables.png)
    ::: moniker-end

1. 按 F5 或选择“调试” > “继续”以继续运行应用  。

    应用将在浏览器中打开。 在浏览器窗口中，应会看到标题为“Express”，第一个段落为“Welcome to Express” 。

1. 选择“One!”、“Two!”和“Three!”   按钮以显示不同的图像。

    ![显示浏览器中运行的应用的屏幕截图。](../javascript/media/tutorial-nodejs-running-in-browser.png)

1. 关闭 Web 浏览器。

## <a name="publish-to-azure-app-service-optional"></a>发布到 Azure 应用服务（可选）

::: moniker range=">=vs-2022"
1. **在“解决方案资源管理器”** 中，右键单击该项目并选择“发布”。 
   
   - 如果出现提示，请选择“添加发布配置文件”。
   - 如果系统提示你安装 Azure WebJob Tools，请选择“安装”。
   
1. 在第一个“发布”屏幕上选择“Azure”，然后选择“下一步”  。
   
   ![显示“发布”对话框的屏幕截图，其中选择了“Azure”。](media/vs-2022/tutorial-nodejs-publish-azure.png)
   
   
1. 在第二个“发布”屏幕上选择“Azure 应用服务(Windows)”，然后选择“下一步”  。
   
   ![显示“发布”对话框的屏幕截图，其中选择了“Azure 应用服务”。](media/vs-2022/tutorial-nodejs-publish-azure-app.png)
   
1. 在下一个屏幕上，根据需要登录到 Azure。 选择要发布到的 Azure 订阅、资源组和应用服务，然后选择“完成”。

   - 如果你没有 Azure 订阅、资源组或应用服务，可以按照此屏幕上的提示创建。
   
   ![显示“发布”对话框的屏幕截图，其中选择了“Azure Web 应用”。](media/vs-2022/tutorial-nodejs-publish-web-app.png)
   
   有关更详细的说明，请参阅 [Publish to Azure Website using Web Deploy](https://github.com/Microsoft/nodejstools/wiki/Publish-to-Azure-Website-using-Web-Deploy)（使用 Web 部署发布到 Azure 网站）。
   
1. 检查发布配置，然后选择“发布”。

   ![显示 Visual Studio 中的“发布”配置和按钮的屏幕截图。](media/vs-2022/tutorial-nodejs-publish-ready.png)
   
   Visual Studio 的“输出”窗口将显示 Azure 部署进度。
   
1. 成功部署后，应用将在 Azure 应用服务中运行的浏览器中打开。 选择按钮可显示图像。
   
   ![显示在 Azure 应用服务的浏览器中运行的 Web 应用屏幕截图。](media/vs-2022/tutorial-nodejs-running-in-azure.png)

::: moniker-end
::: moniker range="<=vs-2019"
1. 在解决方案资源管理器中，右键单击项目，选择“发布”  。

   ![显示“发布到 Azure 应用服务”的屏幕截图。](../javascript/media/tutorial-nodejs-publish-to-azure.png)

1. 选择“Microsoft Azure 应用服务”  。

    在“应用服务”  对话框中，可登录 Azure 帐户并连接到现有的 Azure 订阅。

1. 按其余步骤来选择订阅、选择或创建资源组、选择或创建应用服务计划，然后在系统提示发布到 Azure 时按照步骤操作。 有关更详细的说明，请参阅 [Publish to Azure Website using Web Deploy](https://github.com/Microsoft/nodejstools/wiki/Publish-to-Azure-Website-using-Web-Deploy)（使用 Web 部署发布到 Azure 网站）。

1. “输出”  窗口显示部署到 Azure 的进度。

    成功部署后，应用将在 Azure 应用服务中运行的浏览器中打开。 单击按钮可显示图像。

   ![显示在 Azure 应用服务的浏览器中运行的 Web 应用屏幕截图。](../javascript/media/tutorial-nodejs-running-in-azure.png)
::: moniker-end
恭喜你完成本教程！

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [将应用部署到 Linux 应用服务](../javascript/publish-nodejs-app-azure.md)

> [!div class="nextstepaction"]
> [AngularJS 语言服务扩展](https://devblogs.microsoft.com/visualstudio/angular-language-service-for-visual-studio)

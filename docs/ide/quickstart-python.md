---
title: 快速入门：使用 Visual Studio 创建 Python Web 应用
titleSuffix: ''
description: 在此快速入门教程中，利用 Visual Studio 和 Flask 框架在 Python 中生成简单的 Web 应用。
ms.date: 09/14/2021
ms.technology: vs-python
ms.topic: quickstart
author: rjmolyneaux
ms.author: rmolyneaux
manager: jmartens
ms.custom:
- vs-acquisition
ms.workload:
- python
- data-science
ms.openlocfilehash: beb86c395735c2015eae64866aaf36aefbf9a507
ms.sourcegitcommit: 8fae163333e22a673fd119e1d2da8a1ebfe0e51a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2021
ms.locfileid: "129971616"
---
# <a name="quickstart-create-your-first-python-web-app-using-visual-studio"></a>快速入门：使用 Visual Studio 创建第一个 Python Web 应用

在 5-10 分钟介绍“用作 Python IDE 的 Visual Studio”的简介中，你将基于 Flask 框架创建一个简单的 Python Web 应用程序。 你将通过介绍 Visual Studio 基本功能的单独步骤创建项目。

::: moniker range="vs-2017"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)页免费安装。 在安装程序中，请确保选择“Python 开发”工作负荷  。

::: moniker-end

::: moniker range="vs-2019"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页免费安装。 在安装程序中，请确保选择“Python 开发”工作负荷  。

::: moniker-end

::: moniker range=">=vs-2022"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页免费安装。 在 Visual Studio 安装程序中选择“Python 开发”工作负载，并在安装详细信息中选择“Python Web 支持” 。

![Visual Studio 安装程序的屏幕截图，其中选择了“Python 开发”工作负载和“Python Web 支持”。](media/vs-2022/python-web.png)

::: moniker-end

## <a name="create-the-project"></a>创建项目

以下步骤创建一个作为应用程序容器的空项目：

::: moniker range="vs-2017"
1. 打开 Visual Studio 2017。

2. 从顶部菜单栏中选择“文件”>“新建”>“项目”  。

3. 在“新建项目”对话框右上角的搜索字段中输入“Python Web 项目”，在中间的列表中选择“Web 项目”，为项目命名（如“HelloPython”），然后选择“确定”    。

    ![新建项目对话框，其中选择了 Python Web 项目](media/quickstart-python-00-web-project.png)

    如果找不到 Python 项目模板，请运行 Visual Studio 安装程序，选择“更多”>“修改”，选择“Python 开发”工作负载，然后选择“修改”      。

    ![Visual Studio 安装程序中的 Python 开发工作负载](../python/media/installation-python-workload.png)

4. 新项目在“解决方案资源管理器”  的右窗格中打开。 项目此时已为空，因为它不含其他文件。

    ![显示新创建的空项目的解决方案资源管理器](media/quickstart-python-01-empty-project.png)
::: moniker-end

::: moniker range="vs-2019"
1. 打开 Visual Studio 2019。
2. 在开始屏幕上，选择“创建新项目”  。
3. 在“创建新项目”对话框中，在顶部的搜索字段中输入“Python web”，在中间列表中选择“Web 项目”，然后选择“下一步”    ：

    ![“创建新项目”屏幕，其中选择了“Python Web 项目”](media/quickstart-python-00-web-project-2019a.png) 如果未看到 Python 项目模板，请运行“Visual Studio 安装程序”，选择“更多”>“修改”，选择“Python 开发”工作负载，然后选择“修改”    。

    ![Visual Studio 安装程序中的 Python 开发工作负载](../python/media/installation-python-workload.png)

4. 在接下来的“配置新项目”对话框中，输入“HelloPython”作为项目名称，指定一个位置，然后选择“创建”    。 （解决方案名称自动设置为匹配项目名称。   ）

    ![“配置新项目”对话框](media/quickstart-python-00-web-project-2019b.png)

5. 新项目在“解决方案资源管理器”  的右窗格中打开。 项目此时已为空，因为它不含其他文件。

    ![显示解决方案资源管理器中新建的空项目的屏幕截图。](media/quickstart-python-01-empty-project-2019.png)

::: moniker-end

::: moniker range=">=vs-2022"
1. 打开 Visual Studio 2022。
1. 在开始屏幕上，选择“创建新项目”  。
1. 在“创建新项目”对话框顶部的搜索字段中输入“Python web”。 从列表中选择“Web 项目”，然后选择“下一步” ：
   
   ![显示“创建新项目”屏幕（其中选择了“Python Web 项目”）的屏幕截图。](media/vs-2022/python-web-project.png)
   
   如果未看到 Python Web 项目模板，请选择“工具” > “获取工具和功能”以运行 Visual Studio 安装程序 。 在安装程序中选择“Python 开发”工作负载，并在“安装详细信息”下选择“Python Web 支持”  。 然后选择“修改”。

1. 在“配置新项目”对话框中输入“HelloPython”作为项目名称，指定一个位置，然后选择“创建”  。 “解决方案名称”会自动更新，以便与“项目名称”匹配 。

   ![显示“配置新项目”对话框的屏幕截图。](media/vs-2022/configure-project.png)

新项目在“解决方案资源管理器”  的右窗格中打开。 项目此时已为空，因为它不含其他文件。

![显示解决方案资源管理器（其中包含新建的空项目）的屏幕截图。](media/vs-2022/solution-explorer.png)
::: moniker-end

**问：在 Visual Studio 中为 Python 应用程序创建项目有何优势？**

答：通常只使用文件夹和文件来定义 Python 应用程序，但随着应用程序变大，这种简单的结构可能会变得难于负担。 应用程序可能涉及到自动生成的文件、适用于 Web 应用程序的 JavaScript 和其他组件。 Visual Studio 项目帮助管理复杂性问题。

项目（一个 .rxproj 文件）可以识别与项目关联的所有源文件和内容文件。 该 .pyproj 文件还包含每个文件的生成信息，会维护要与源代码管理系统集成的信息，并且帮助你将应用程序组织成逻辑组件。

**问：解决方案资源管理器中显示的“解决方案”是指什么？**

答：Visual Studio 解决方案是一个容器，可帮助你将一个或多个相关项目作为一个组进行管理。 该解决方案将存储不特定于某一项目的配置设置。 解决方案中的项目还可相互引用。 例如，运行一个 Python 应用项目可自动生成另一个项目，例如 Python 应用使用的 C++ 扩展。

## <a name="install-the-flask-library"></a>安装 Flask 库

Python 中的 Web 应用几乎总是使用众多可用 Python 库中的一个来处理低级别详细信息，如路由 Web 请求和调整响应。 Visual Studio 为 Web 应用提供许多模板。 稍后你将在本快速入门中使用其中的一个模板。

使用以下步骤将 Flask 库安装到 Visual Studio 用于此项目的默认全局环境。

::: moniker range="vs-2017"
1. 展开项目中的“Python 环境”  节点，查看项目的默认环境。

    ![显示默认环境的解决方案资源管理器](media/quickstart-python-02-default-environment.png)

2. 右键单击环境并选择“安装 Python 包”  。 此命令将打开“包”  选项卡上的“Python 环境”  窗口。

3. 在搜索字段中输入“flask”，再选择 [PyPI 中的“pip install flask”]  。 接受任何管理员权限提示，查看 Visual Studio 中的“输出”  窗口了解进度。 （当全局环境的包文件夹位于类似于 C:\Program Files  这样的受保护区域时，会出现提升提示。）

    ![使用 pip 安装，安装 Flask 库](media/quickstart-python-03-install-package.png)
::: moniker-end
::: moniker range="vs-2019"
1. 展开项目中的“Python 环境”  节点，查看项目的默认环境。

    ![显示默认环境的解决方案资源管理器](media/quickstart-python-02-default-environment-2019.png)

2. 右键单击环境并选择“管理 Python 包...”  。此命令将打开“包 (PyPI)”选项卡上的“Python 环境”窗口   。

3. 在搜索字段中输入"flask"。 如果 Flask 出现在搜索框下方，可跳过此步骤  。 否则选择“运行命令: pip install flask”  。 接受任何管理员权限提示，查看 Visual Studio 中的“输出”  窗口了解进度。 （当全局环境的包文件夹位于类似于 C:\Program Files  这样的受保护区域时，会出现提升提示。）

    ![使用 pip 安装，安装 Flask 库](media/quickstart-python-03-install-package-2019.png)
::: moniker-end

::: moniker range=">=vs-2022"
1. 展开项目中的“Python 环境”  节点，查看项目的默认环境。

    ![显示解决方案资源管理器中的默认环境的屏幕截图。](media/vs-2022/python-environment.png)

1. 右键单击该环境并选择“管理 Python 包”。 此命令将打开“包 (PyPI)”选项卡上的“Python 环境”窗口。

1. 在搜索字段中输入"flask"。 如果 Flask 出现在搜索框下方，可跳过此步骤  。 否则请选择“运行命令: pip install flask”。

    ![显示使用 pip install 安装 Flask 库的屏幕截图。](media/vs-2022/install-flask.png)

    如果全局环境包文件夹位于受保护区域（例如 C:\Program Files）中，则会出现权限提升的提示。 接受任何有关管理员权限的提示。 在 Visual Studio 的“输出”窗口中观察进度。

::: moniker-end

安装完成后，该库将显示在“解决方案资源管理器”的环境中，这意味着可以在 Python 代码中使用它。

::: moniker range="vs-2017"
![已安装 Flask 库并在解决方案资源管理器中显示](media/quickstart-python-04-package-installed.png)
::: moniker-end
::: moniker range="vs-2019"
![已安装 Flask 库并在解决方案资源管理器中显示](media/quickstart-python-04-package-installed-2019.png)
::: moniker-end
::: moniker range=">=vs-2022"
![显示 Flask 库已安装并显示在解决方案资源管理器中的屏幕截图。](media/vs-2022/flask-installed.png)
::: moniker-end

> [!Note]
> 开发人员通常会创建一个虚拟环境用于安装特定项目的库，而不是在全局环境中安装库。 Visual Studio 模板通常会提供此选项，如[快速入门 - 使用模板创建 Python 项目](../python/quickstart-02-python-in-visual-studio-project-from-template.md)中所述。

**问：我可在何处深入了解其他可用的 Python 包？**

**答**：请访问 [Python 包索引](https://pypi.org/)。

## <a name="add-a-code-file"></a>添加代码文件

现已准备好添加一点 Python 代码来实现最小的 Web 应用。

::: moniker range="<=vs-2019"
1. 在“解决方案资源管理器”中右键单击该项目，然后选择“添加”>“新建项”  。

1. 在出现的对话框中，选择“空 Python 文件”  ，将其命名为 app.py  ，然后选择“添加”  。 Visual Studio 会自动在编辑器窗口中打开该文件。

1. 复制以下代码，并将其粘贴到 app.py  ：

    ```python
    from flask import Flask

    # Create an instance of the Flask class that is the WSGI application.
    # The first argument is the name of the application module or package,
    # typically __name__ when using a single module.
    app = Flask(__name__)

    # Flask route decorators map / and /hello to the hello function.
    # To add other resources, create functions that generate the page contents
    # and add decorators to define the appropriate resource locators for them.

    @app.route('/')
    @app.route('/hello')
    def hello():
        # Render the page
        return "Hello Python!"

    if __name__ == '__main__':
        # Run the app server on localhost:4449
        app.run('localhost', 4449)
    ```
::: moniker-end
::: moniker range=">= vs-2022"

1. 在“解决方案资源管理器”中右键单击该项目，然后选择“添加”>“新建项”  。

1. 在出现的对话框中选择“空白”。 输入“app.py”作为“名称”，然后选择“添加”。 Visual Studio 会自动在编辑器窗口中打开该文件。

1. 复制以下代码，并将其粘贴到 app.py  ：

    ```python
    from flask import Flask

    # Create an instance of the Flask class that is the WSGI application.
    # The first argument is the name of the application module or package,
    # typically __name__ when using a single module.
    app = Flask(__name__)

    # Flask route decorators map / and /hello to the hello function.
    # To add other resources, create functions that generate the page contents
    # and add decorators to define the appropriate resource locators for them.

    @app.route('/')
    @app.route('/hello')
    def hello():
        # Render the page
        return "Hello Python!"

    if __name__ == '__main__':
        # Run the app server on localhost:4449
        app.run('localhost', 4449)
    ```
::: moniker-end

你可能已注意到，“添加” > “新建项”对话框显示了很多可添加到 Python 项目的其他类型的文件，例如 Python 类、Python 包、Python 单元测试和 web.config 文件等 。 一般情况下，这些项模板非常适合用于通过有用的样板代码快速创建文件。

**问：我可在何处了解 Flask 的详细信息？**

**答**：请参阅 Flask 文档，首先是 [Flask 快速入门](https://flask.palletsprojects.com/quickstart/#quickstart)。

## <a name="run-the-application"></a>运行此应用程序

1. 在“解决方案资源管理器”中右键单击“app.py”，然后从下拉菜单中选择“设置为启动文件”。 此命令可标识运行应用时要在 Python 中启动的代码文件。

    ::: moniker range="vs-2017"
    ![在解决方案资源管理器中设置项目的启动文件](media/quickstart-python-05-set-as-startup-file.png)
    ::: moniker-end
    ::: moniker range="vs-2019"
    ![在解决方案资源管理器中设置项目的启动文件](media/quickstart-python-05-set-as-startup-file-2019.png)
    ::: moniker-end
    ::: moniker range=">=vs-2022"
    ![显示在解决方案资源管理器中为项目设置启动文件的屏幕截图。](media/vs-2022/set-startup-file.png)
    ::: moniker-end

2. 右键单击“解决方案资源管理器”中的项目，再选择“属性” 。 从“属性”菜单中选择“调试”选项卡，将“端口号”属性设置为 `4449`  。 此设置可确保 Visual Studio 通过 `localhost:4449` 启动浏览器，以匹配代码中的 `app.run` 参数。

3. 选择“调试” > “开始执行(不调试)”或按 Ctrl+F5，这会将更改保存到文件并运行应用   。

4. 此时会出现一个命令窗口，其中显示了消息“在 https:\//localhost:4449 中运行”。 浏览器窗口中会打开 `localhost:4449` 并显示消息“Hello, Python!” 状态为 `200` 的 `GET` 请求也会显示在命令窗口中。

    如果浏览器未自动打开，请启动你选择的浏览器并导航到 `localhost:4449`。

    如果只在命令窗口中看到 Python 交互式 shell，或者该窗口在屏幕上短暂闪现，请确保已将 app.py 设置为启动文件。

5. 导航到 `localhost:4449/hello`，测试确保 `/hello` 资源的修饰器也正常运行。 同样，状态为 `200` 的 `GET` 请求会显示在命令窗口中。 尝试其他一些 URL，查看它们是否在命令窗口中显示 `404` 状态代码。

6. 关闭命令窗口以停止应用，然后关闭浏览器窗口。

问：“开始执行(不调试)”命令和“开始调试”命令有何区别？

答：使用“开始调试”会在 [Visual Studio 调试器](../python/debugging-python-in-visual-studio.md)的上下文中运行应用 。 使用调试器可以设置断点、检查变量和逐行单步执行代码。 由于用于实现调试的挂钩，应用在调试器中的运行速度可能会较慢。

“开始执行(不调试)”则是直接运行应用（就像从命令行运行应用一样），而不是使用调试上下文。 “开始执行(不调试)”还会自动启动浏览器，并导航到项目属性的“调试”选项卡中指定的 URL 。

## <a name="next-steps"></a>后续步骤

祝贺你从 Visual Studio 运行了第一个 Python 应用。 你已初步了解如何将 Visual Studio 用作 Python IDE！

> [!div class="nextstepaction"]
> [将应用部署到 Azure 应用服务](../python/publishing-python-web-applications-to-azure-from-visual-studio.md)

此快速入门中的步骤比较笼统，你可能已猜到它们可以且应当自动执行。 此类自动化由 Visual Studio 项目模板执行。 浏览[快速入门 - 使用模板创建 Python 项目](../python/quickstart-02-python-in-visual-studio-project-from-template.md)，通过更少的步骤创建一个与本文中的 Web 应用类似的 Web 应用。

若要继续在 Visual Studio 中了解更完整的 Python 教程（包括使用交互式窗口、调试、数据可视化效果以及使用 Git），请参阅[教程：Visual Studio 中的 Python 入门](../python/tutorial-working-with-python-in-visual-studio-step-01-create-project.md)。

若要了解更多 Visual Studio 产品，请选择以下链接。

- 了解 [Visual Studio 中的 Python Web 应用模板](../python/python-web-application-project-templates.md)。
- 了解 [Python 调试](../python/debugging-python-in-visual-studio.md)
- 总括性地了解 [Visual Studio IDE](../get-started/visual-studio-ide.md) 的详细信息。

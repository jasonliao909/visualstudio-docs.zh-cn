---
title: 学习 Visual Studio 中的 Flask 教程的第 2 步，视图和模板
titleSuffix: ''
description: Visual Studio 项目上下文中 Flask 基础知识的演练，具体介绍了创建应用以及使用视图和模板的步骤。
ms.custom: devdivchpfy22
ms.date: 02/04/2022
ms.topic: tutorial
author: rjmolyneaux
ms.author: rmolyneaux
manager: jmartens
ms.technology: vs-python
ms.workload:
- python
- data-science
ms.openlocfilehash: 57a9e650dc061c53445500eab612cf9ef126474e
ms.sourcegitcommit: edf8137cd90c67b6078a02c93094f7e1c3bf8930
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2022
ms.locfileid: "139552450"
---
# <a name="step-2-create-a-flask-app-with-views-and-page-templates"></a>步骤 2：使用视图和页面模板创建 Flask 应用

**上一步：[创建 Visual Studio 项目和解决方案](learn-flask-visual-studio-step-01-project-solution.md)**

在本教程的步骤 1 中，你创建了一个 Flask 应用，该应用包含一个页面和单个文件的所有代码。 为了将来进行开发，最好重构代码并创建页面模板的结构。 尤其建议将应用视图代码与启动代码等其他特性分离。

在此步骤中，可以了解如何：

> [!div class="checklist"]
>
> - 重构应用代码，以便从启动代码分离视图（步骤 2-1）
> - 使用页面模板呈现视图（步骤 2-2）

## <a name="step-2-1-refactor-the-project-to-support-further-development"></a>步骤 2-1：重构项目以支持进一步开发

在“空白 Flask Web 项目”模板创建的代码中，有个单一 app.py 文件，它包含启动代码及单一视图  。 若要进一步开发具有多个视图和模板的应用，最好分离这些问题。

1. 在项目文件夹中，创建名为 `HelloFlask` 的应用文件夹（右键单击解决方案资源管理器中的项目并选择“添加” > “新建文件夹”    。）

2. 在 HelloFlask 文件夹中，创建名为 \_\_init\_\_.py 的文件，包含创建 `Flask` 实例并加载应用视图（下一步中创建）的以下内容   ：

    ```python
    from flask import Flask
    app = Flask(__name__)

    import HelloFlask.views
    ```

3. 在 HelloFlask 文件夹中，创建名为 views.py 的文件，包含以下内容   。 名称 *views.py* 很重要`import HelloFlask.views`*\_\_，因为是在 init.py\_\_* 中使用的;如果名称不匹配，则在运行时会看到错误。

    ```python
    from flask import Flask
    from HelloFlask import app

    @app.route('/')
    @app.route('/home')
    def home():
        return "Hello Flask!"
    ```

    除了将函数和路由重命名为 `home`，此代码包含 app.py 的页面呈现代码并导入 \_\_init\_\_.py 中声明的 `app` 对象   。

4. 在 HelloFlask 中创建名为 templates 的子文件夹，目前为空   。

5. 在项目的根文件夹中，将 app.py 重命名为 runserver.py，并使内容匹配以下代码   ：

    ```python
    import os
    from HelloFlask import app    # Imports the code from HelloFlask/__init__.py

    if __name__ == '__main__':
        HOST = os.environ.get('SERVER_HOST', 'localhost')

        try:
            PORT = int(os.environ.get('SERVER_PORT', '5555'))
        except ValueError:
            PORT = 5555

        app.run(HOST, PORT)
    ```

6. 项目结构应如下图所示：

    ![重构代码后的项目结构](media/flask/step-02-project-structure.png)

7. 选择 **"** > 调试""开始 **调试 (** **F5**) 或使用工具栏上的"**Web** 服务器"按钮 (你看到的浏览器可能会) 启动应用并打开浏览器。 同时尝试 / 和 /home URL 路由。

8. 还可以在代码的不同部分设置断点，并且重新启动应用，跟随启动顺序。 例如，对 runserver.py  和 HelloFlask\_init_.py   的第一行设置断点，并对 views.py  中的 `return "Hello Flask!"` 行设置断点。 然后，重启应用 (**DebugRestart** > 、**CtrlShiftF5**++ 或下面显示的工具栏按钮) 并单步执行 (**F10**) 代码，或者使用 **F5** 从每个断点运行。

    ![Visual Studio 中调试工具栏上的重启按钮](media/debugging-restart-toolbar-button.png)

9. 完成后，停止应用。

### <a name="commit-to-source-control"></a>提交到源代码管理

成功对代码进行更改和测试后，你可以查看所做的更改，并提交到源代码管理。 在稍后的步骤中，当本教程提醒你再次提交源代码管理时，可以参考本部分。

1. 选择下面圆圈为 Visual Studio (底部的"更改") ，以导航到 **团队资源管理器。**

    ![Visual Studio 状态栏上的源代码管理更改按钮](media/flask/step-02-source-control-changes-button.png)

1. 在“团队资源管理器”中，输入“重构代码”等提交消息，然后选择“全部提交”   。 提交完成后，将看到一条消息“已在本地创建提交 \<hash> **。** 同步后与服务器共享你的更改。” 如果要将更改推送到远程存储库，请选择“同步”  ，然后选择“传出提交”  下的“推送”  。 在推送至远程存储库之前，还可以累积多个本地提交。

    ![将提交推送到团队资源管理器中的远程存储库](media/flask/step-02-source-control-push-to-remote.png)

### <a name="question-how-frequently-should-one-commit-to-source-control"></a>问：应多久提交到源代码管理一次？

答：将更改提交到源代码会在更改日志中创建一个记录以及一个可以将存储库还原到的点（如需）。 也可以针对特定更改检查每个提交。 由于 Git 提交成本较低，最好执行频繁提交，而不是将大量更改积累到单个提交中。 无需将每个小更改提交到单个文件。 通常，在添加功能、更改结构（如此步骤中完成）或重构某些代码时提交。 此外，与团队其他人检查最适合每个人的提交粒度。

提交的频率和将提交推送到远程存储库的频率是两个不同的问题。 在本地存储库中累积多个提交，然后再将其推送到远程存储库。 提交频率取决于团队希望如何管理存储库。

## <a name="step-2-2-use-a-template-to-render-a-page"></a>步骤 2-2：使用模板呈现页面

到目前为止，你在 views.py 中所拥有的 `home` 函数只会针对页面生成一个纯文本 HTTP 响应  。 但是，大多数真实 Web 页面都使用丰富的 HTML 页面进行响应，这些页面通常包含实时数据。 使用函数定义视图的主要原因是动态生成内容。

由于视图的返回值只是一个字符串，所以可以使用动态内容在字符串中生成任何喜欢的 HTML。 但是，由于最好将标记与数据分开，因此最好将标记放在模板中，并保留代码中的数据。

1. 首先，编辑 views.py 以包含以下代码，该代码针对有动态内容的页面使用内联 HTML  ：

    ```python
    from datetime import datetime
    from flask import render_template
    from HelloFlask import app

    @app.route('/')
    @app.route('/home')
    def home():
        now = datetime.now()
        formatted_now = now.strftime("%A, %d %B, %Y at %X")

        html_content = "<html><head><title>Hello Flask</title></head><body>"
        html_content += "<strong>Hello Flask!</strong> on " + formatted_now
        html_content += "</body></html>"

        return html_content
    ```

1. 运行应用并刷新几次页面，查看日期/时间是否更新。 完成后，停止应用。

1. 要将页面呈现转换为使用模板，请使用以下内容在 templates 文件夹中创建名为 index.html 的文件，其中 `{{ content }}` 是在代码中为其提供值的占位符或者替换令牌（也称为模板变量）    ：

    ```html
    <html>
        <head><title>Hello Flask</title></head>

        <body>
            {{ content }}
        </body>
    </html>
    ```

1. 修改 `home` 函数以使用 `render_template` 加载模板并为“内容”提供值，这通过使用匹配占位符名称的命名参数完成。 Flask 在 templates 文件夹中自动查找模板，因此模板路径与该文件夹是相对的  ：

    ```python
    def home():
        now = datetime.now()
        formatted_now = now.strftime("%A, %d %B, %Y at %X")

        return render_template(
            "index.html",
            content = "<strong>Hello, Flask!</strong> on " + formatted_now)
    ```

1. 运行应用并查看结果。 请注意，值中的内联 `content` *HTML 不会* 呈现为 HTML，因为模板化引擎 (Jinja) 自动转义 HTML 内容。 自动转义可防止意外漏洞受到注入攻击。 开发人员通常从一个页面收集输入，并通过模板占位符将输入用作另一页中的值。 转义还提醒你最好将 HTML 排除在代码中。

    相应地，评审 templates\index.html 以包含用于标记中每个数据段的不同占位符  ：

    ```html
    <html>
        <head>
            <title>{{ title }}</title>
        </head>
        <body>
            <strong>{{ message }}</strong>{{ content }}
        </body>
    </html>
    ```

    然后，更新 `home` 函数为所有占位符提供值：

    ```python
    def home():
        now = datetime.now()
        formatted_now = now.strftime("%A, %d %B, %Y at %X")

        return render_template(
            "index.html",
            title = "Hello Flask",
            message = "Hello, Flask!",
            content = " on " + formatted_now)
    ```

1. 再次运行应用，并查看正确呈现的输出。

    ![使用模板运行应用](media/flask/step-02-result.png)

1. 可以将更改提交到源代码管理并更新远程存储库。 有关详细信息，请参阅步骤 [2-1](#commit-to-source-control)。

### <a name="question-do-page-templates-have-to-be-in-a-separate-file"></a>问：页面模板必须在一个单独的文件中吗？

答：尽管模板通常会保留在单独的 HTML 文件中，但也可以使用内联模板。 建议使用单独的文件来保持标记和代码之间的干净分离。

### <a name="question-must-templates-use-the-html-file-extension"></a>问：模板必须使用 .html 文件扩展名吗？

答： *.html* 模板文件的扩展名是完全可选的，因为始终可以在函数的第一个参数中标识文件的确切相对 `render_template` 路径。 但是，Visual Studio (编辑器) 通常提供代码完成和.html文件的 *语法着色等* 功能，这超过了页面模板不是 HTML 这一事实。

使用 Flask 项目时，Visual Studio自动检测正在编辑的 HTML 文件何时实际上是 Flask 模板，并提供某些自动完成功能。 例如，在开始键入 Flask 页面模板注释 `{#` 时，Visual Studio 会自动提供右边的 `#}` 字符。 “注释选定内容”  和“取消注释选定内容”  命令（在“编辑”   > “高级”  菜单上和工具栏上）也使用模板注释，而不是 HTML 注释。

### <a name="question-can-templates-be-organized-into-further-subfolders"></a>问：模板是否可以整理到下级子文件夹中？

答：是，可以使用子文件夹，然后在对 `render_template` 的调用中指代 templates 下的相对路径  。 执行此操作是有效创建模板命名空间的好办法。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [为静态文件提供服务、添加页面和使用模板继承](learn-flask-visual-studio-step-03-serve-static-files-add-pages.md)

## <a name="go-deeper"></a>深入了解

- [Flask 快速入门 - 呈现模板](https://flask.palletsprojects.com/en/1.0.x/quickstart/#rendering-templates) (flask.pocoo.org)
- GitHub 上的教程源代码：[Microsoft/python-sample-vs-learning-flask](https://github.com/Microsoft/python-sample-vs-learning-flask)

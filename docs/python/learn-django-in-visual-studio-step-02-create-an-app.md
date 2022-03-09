---
title: 了解 Visual Studio 中的 Django 教程步骤 2，视图和页面模板
titleSuffix: ''
description: Visual Studio 项目上下文中 Django 基础知识的演练，具体介绍了创建应用以及使用视图和模板的步骤。
ms.date: 02/03/2022
ms.custom: devdivchpfy22
ms.topic: tutorial
author: rjmolyneaux
ms.author: rmolyneaux
manager: jmartens
ms.technology: vs-python
ms.workload:
- python
- data-science
ms.openlocfilehash: 66c300d16e51e22f36f0ae475e71bdfe7035f488
ms.sourcegitcommit: edf8137cd90c67b6078a02c93094f7e1c3bf8930
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2022
ms.locfileid: "139551483"
---
# <a name="step-2-create-a-django-app-with-views-and-page-templates"></a>步骤 2：使用视图和页面模板创建 Django 应用

**上一步：[创建 Visual Studio 项目和解决方案](learn-django-in-visual-studio-step-01-project-and-solution.md)**

在 Visual Studio 项目中，你现在只有 Django *项目* 的站点级组件，它可以运行一个或多个 Django *应用*。 下一步是在单个页面中创建你的第一个应用。

在此步骤中，你将了解如何：

> [!div class="checklist"]
> - 在单个页面中创建 Django 应用（步骤 2-1）
> - 从 Django 项目运行应用（步骤 2-2）
> - 使用 HTML 呈现视图（步骤 2-3）
> - 使用 Django 页面模板呈现视图（步骤 2-4）

## <a name="step-2-1-create-an-app-with-a-default-structure"></a>步骤 2-1：创建具有默认结构的应用

Django 应用是一个单独的 Python 包，其中包含一组用于特定用途的相关文件。 一个 Django 项目可以包含许多应用，这些应用可帮助 web 主机提供单个域名提供的多个不同入口点。 例如，像 contoso.com 这样的域的 Django 项目可能包含一个面向 `www.contoso.com` 的应用、一个面向 support.contoso.com 的应用以及一个面向 docs.contoso.com 的应用。 在这种情况下，Django 项目会在其 *urls.py* 和 *settings.py* 文件) 中处理站点级 URL 路由和设置 (。 每个应用程序都具有其内部路由、视图、模型、静态文件和管理界面的独特的样式和行为。

Django 应用通常以一组标准文件开头。 Visual Studio 提供模板，用于在 Django 项目中初始化 Django 应用，以及用于实现相同目的的集成菜单命令：

- 模板：在“解决方案资源管理器”中，右键单击项目，然后选择“添加” > “新项”    。 在 " **添加新项** " 对话框中，选择 " **Django 1.9 应用程序** " 模板，在 " **名称** " 字段中指定应用程序名称，然后选择 " **添加**"。

:::image type="content" source="media/django/step02-new-item.png" alt-text="解决方案资源管理器的屏幕截图。":::

:::image type="content" source="media/django/step02-add-new-item.png" alt-text="&quot;添加新项&quot; 窗口的屏幕截图。":::

- 集成的命令：在“解决方案资源管理器”中，右键单击项目，然后选择“添加” > “Django 应用”    。 此命令会提示你输入名称。 在 " **新应用名称** " 字段中指定应用名称，然后选择 **"确定"**。

    :::image type="content" source="media/django/step02-add-django-app-command.png" alt-text="用于添加 Django 应用的菜单命令。":::

    :::image type="content" source="media/django/step-02-django-app-name.png" alt-text="用于输入 Django 应用名称的菜单命令。":::

使用任一方法创建一个名为“HelloDjangoApp”的应用。 现在，在项目中创建 "HelloDjangoApp" 文件夹。 文件夹包含以下项：

:::image type="content" source="media/django/step02-django-app-in-solution-explorer.png" alt-text="解决方案资源管理器中的 Django 应用程序文件。":::

::: moniker range="vs-2017"
| 项目 | 描述 |
| --- | --- |
| **\_\_init\_\_.py** | 将应用标识为包的文件。 |
| **迁移** | 一个文件夹，Django 在其中存储用于更新数据库以便与模型更改保持一致的脚本。 然后，Django 迁移工具将必要的更改应用到任何以前版本的数据库，以便与当前模型相匹配。 使用迁移，可以将注意力集中在模型上，并让 Django 处理基础数据库架构。 步骤 6 中已对迁移进行了讨论；现在，该文件夹只需包含 \_\_init\_\_.py 文件（指示文件夹定义其自己的 Python 包）  。 |
| **模板** | Django 页面模板文件夹，其中包含与应用名匹配的文件夹中的一个 index.html 文件  。 （在 Visual Studio 2017 15.7 及更早版本中，该文件直接包含在模板中，步骤 2-4 指示你创建子文件夹  。）模板是若干个 HTML 块，视图可以将信息添加到其中并以动态方式呈现页面。 页面模板“变量”（如 index.html 中的 `{{ content }}`）都是动态值占位符，如本文后面所述（步骤 2）  。 通常情况下，Django 应用通过将模板放置在与应用名称匹配的子文件夹中来创建其模板的命名空间。 |
| **admin.py** | 在其中扩展应用管理界面的 Python 文件（请参阅步骤 6），用于对数据库中的数据进行种子设定和编辑。 最初，此文件仅包含语句 `from django.contrib import admin`。 默认情况下，Django 在 Django 项目 settings.py 文件中的条目中包含一个标准的管理界面，可以通过取消评论 urls.py 中的现有条目将其打开   。 |
| **apps.py** | 定义应用配置类的 Python 文件（参见下文，在此表后）。 |
| **models.py** | 模型是由函数识别的数据对象，视图通过模型与应用的基础数据库进行交互（请参阅步骤 6）。 Django 提供数据库连接层，这样应用就无需考虑这些细节。 models.py 文件是用于创建模型的默认位置，最初只包含语句 `from django.db import models`  。 |
| **tests.py** | 包含单元测试基本结构的 Python 文件。 |
| **views.py** | 视图是你通常将其视为网页的对象，它接收 HTTP 请求并返回 HTTP 响应。 视图通常呈现为 Web 浏览器知道如何显示的 HTML，但视图不一定可见（比如中间形式）。 视图由 Python 函数定义，它的职责是呈现 HTML 以发送到浏览器。 views.py 文件是用于创建视图的默认位置，最初只包含语句 `from django.shortcuts import render`  。 |
::: moniker-end

::: moniker range=">=vs-2019"
| 项目 | 描述 |
| --- | --- |
| **迁移** | 一个文件夹，其中 Django 存储更新数据库的脚本，使其与对模型所做的更改保持一致。 然后，Django 的迁移工具对数据库的任何以前版本应用必要的更改，以匹配当前模型。 使用迁移，可以将注意力集中在模型上，并让 Django 处理基础数据库架构。 [Django 文档](https://docs.djangoproject.com/en/3.2/topics/migrations/)中讨论了迁移。 目前，文件夹包含 *\_ \_ \_ \_ py* 文件 (指示该文件夹定义了其自己的 Python 包) 。 |
| **\_\_init\_\_.py** | 将应用标识为包的文件。 |
| **templates** | 包含单个 *index.html* 文件的 Django 页面模板的文件夹。 *index.html* 文件位于名为 "与应用名称相同" 的文件夹中。  (在 Visual Studio 2017 15.7 及更早版本中，该文件将直接置于 *模板* 下，步骤2-4 会指导你创建该子文件夹。 ) 模板是一个 HTML 块，视图可在其中添加信息以动态呈现页面。 页面模板“变量”（如 index.html 中的 `{{ content }}`）都是动态值占位符，如本文后面所述（步骤 2）  。 通常，Django 应用会通过将其放在与应用名称匹配的子文件夹中，为其模板创建命名空间。 |
| **admin.py** | Python 文件，在其中扩展应用程序的管理界面，用于在数据库中查看和编辑数据。 最初，此文件仅包含语句 `from django.contrib import admin`。 默认情况下，Django 包含 Django 项目的 *settings.py* 文件中的条目的标准管理界面。 若要打开接口，可以取消注释 *urls.py* 文件中的现有条目。 |
| **apps.py** | 定义应用配置类的 Python 文件（参见下文，在此表后）。 |
| **models.py** | 模型是由函数识别的数据对象，视图通过模型与应用的基础数据库进行交互。 Django 提供了数据库连接层，因此应用程序不会考虑模型详细信息。 *Models.py* 文件是创建模型时的默认位置。 最初， *models.py* 文件只包含语句， `from django.db import models` 。 |
| **tests.py** | 包含单元测试基本结构的 Python 文件。 |
| **views.py** | 视图类似于网页，后者采用 HTTP 请求并返回 HTTP 响应。 通常，视图以 HTML 格式呈现，而 web 浏览器则知道如何显示，但视图并不一定要 (像中间窗体) 一样可见。 视图由 Python 函数定义，其职责是将 HTML 呈现到浏览器。 *Views.py* 文件是创建视图的默认位置。 最初， *views.py* 文件只包含语句， `from django.shortcuts import render` 。 |
::: moniker-end

使用名称 "HelloDjangoApp" 时， *apps.py* 文件的内容将显示为：

```python
from django.apps import AppConfig

class HelloDjangoAppConfig(AppConfig):
    name = 'HelloDjango'
```

### <a name="question-is-creating-a-django-app-in-visual-studio-any-different-from-creating-an-app-on-the-command-line"></a>问：在 Visual Studio 中创建 Django 应用与在命令行上创建应用有什么不同吗？

答：运行“添加” > “Django 应用”命令或者将“添加” > “新项”与 Django 应用模板结合使用生成的文件与使用 Django 命令 `manage.py startapp <app_name>` 生成的文件相同     。 在 Visual Studio 中创建应用的好处是应用文件夹及其所有文件会自动集成到项目中。 可以使用相同的 Visual Studio 命令在项目中创建任意数量的应用。

## <a name="step-2-2-run-the-app-from-the-django-project"></a>步骤 2-2：从 Django 项目运行应用

此时，如果你使用工具栏按钮或 **调试**  >  **开始调试**) Visual Studio (再次运行该项目，仍将看到默认页面。 不会显示应用内容，因为需要定义一个特定于应用的页面，并将该应用添加到 Django 项目中：

1. 在 *HelloDjangoApp* 文件夹中，修改 *views.py* 文件以定义名为 "index" 的视图：

    ```python
    from django.shortcuts import render
    from django.http import HttpResponse

    def index(request):
        return HttpResponse("Hello, Django!")
    ```

1. 在步骤 1)  (创建的 *BasicProject* 文件夹中，修改 *urls.py* 文件，使其与以下代码相匹配 () 如果需要，可以保留指导注释：

    ```python
    from django.conf.urls import include, url
    import HelloDjangoApp.views

    # Django processes URL patterns in the order they appear in the array
    urlpatterns = [
        url(r'^$', HelloDjangoApp.views.index, name='index'),
        url(r'^home$', HelloDjangoApp.views.index, name='home'),
    ]
    ```

    每个 URL 模式均介绍了 Django 向其路由特定网站对应的 URL 的视图（即“`https://www.domain.com/`”后面的部分）。 `urlPatterns` 中以正则表达式 `^$` 开头的第一个条目是站点根目录“/”的路由。 第二个条目 `^home$` 专门路由“/home”。 可以将多个路由路由到同一个视图。

1. 再次运行该项目并看到消息“Hello, Django!”  与视图定义的一致。 完成后，停止服务器。

### <a name="commit-to-source-control"></a>提交到源代码管理

更改代码并成功测试后，可以查看并提交到源代码管理。 在后面的步骤中，当本教程提醒您再次提交到源代码管理时，您可以参考此部分。

1. 选择下方) 下方 (Visual Studio 下的 "更改" 按钮以导航到 **团队资源管理器**。

    :::image type="content" source="media/django/step02-source-control-changes-button.png" alt-text="Visual Studio 状态栏上的 &quot;源代码管理&quot; 更改按钮。":::

1. 在“团队资源管理器”  中，输入提交消息，如“创建初始 Django 应用”并选择“全部提交”  。 提交完成后，将看到一条消息“已在本地创建提交 \<hash> **。** 同步后与服务器共享你的更改。” 如果要将更改推送到远程存储库，请选择 "**同步**"，然后在 "**传出提交**" 下选择 "**推送**"。 在推送至远程存储库之前，还可以累积多个本地提交。

    :::image type="content" source="media/django/step02-source-control-push-to-remote.png" alt-text="在团队资源管理器中将提交推送到远程存储库。":::

### <a name="question-what-is-the-r-prefix-before-the-routing-strings-for"></a>问：路由字符串前的“r”前缀代表什么？

答：Python 中字符串的“r”前缀表示“raw”，它指示 Python 不转义字符串中的任何字符。 正则表达式使用多个特殊字符。 使用 "r" 前缀可使字符串比转义符 " \\ " 更易于读取。

### <a name="question-what-do-the--and--characters-mean-in-the-url-routing-entries"></a>问：在 URL 路由条目中，^ 和 $ 字符表示什么意思？

答：在定义 URL 模式的正则表达式中，^ 表示 "行首" 和 $ 表示 "行尾"，其中 Url 相对于) 后面 `https://www.domain.com/` 的部分 (网站根目录。 正则表达式 `^$` 有效地表示 "空白" 并匹配完整 URL `https://www.domain.com/` ， (未向站点根) 添加任何内容。 模式 `^home$` 精确匹配 `https://www.domain.com/home/`。 （Django 不在模式匹配中使用尾随 /。）

如果在正则表达式中不使用尾随 $，比如 `^home`，那么 URL 模式匹配任何  以“home”开头的 URL，如“home”、“homework”、“homestead”和“home192837”。

若要尝试使用不同的正则表达式，请尝试使用联机工具，如 [pythex.org](https://www.pythex.org) 中的 [regex101.com](https://regex101.com)。

## <a name="step-2-3-render-a-view-using-html"></a>步骤 2-3：使用 HTML 呈现视图

*Views.py* 文件中包含的 `index` 函数将为该页生成纯文本 HTTP 响应。 大多数实际网页都是通过丰富的 HTML 页面（经常引入实时数据）进行响应。 的确，使用函数定义视图的主要原因是动态生成内容。

作为的参数 `HttpResponse` 只是一个字符串，你可以在字符串中生成你喜欢的任何 HTML。 作为一个简单的示例，请将函数替换 `index` 为以下代码 (使现有 `from` 的语句) 。 然后，该 `index` 函数将使用在每次刷新页面时更新的动态内容生成 HTML 响应。

```python
from datetime import datetime

def index(request):
    now = datetime.now()

    html_content = "<html><head><title>Hello, Django</title></head><body>"
    html_content += "<strong>Hello Django!</strong> on " + now.strftime("%A, %d %B, %Y at %X")
    html_content += "</body></html>"

    return HttpResponse(html_content)
```

现在，再次运行该项目以查看类似于 "**Hello Django！** 2018年4月16:28:10 日。 刷新页面以更新时间并确认通过每个请求生成了内容。 完成后，停止服务器。

> [!Tip]
> 要停止并重启项目，其快捷方式是使用“调试” > “重启”菜单命令 (Ctrl+Shift+F5)，或者使用调试工具栏上的“重启”按钮       ：
>
> :::image type="content" source="media/debugging-restart-toolbar-button.png" alt-text="Visual Studio 中的 &quot;调试&quot; 工具栏上的 &quot;重启&quot; 按钮。":::
>

## <a name="step-2-4-render-a-view-using-a-page-template"></a>步骤 2-4：使用页面模板呈现视图

在代码中生成 HTML 适用于小页面。 但是，随着页面变得更加复杂，您需要维护页面的静态 HTML 部分 (以及对 CSS 和 JavaScript 文件的引用) 为 "页面模板"。 然后，可以将动态生成代码的内容插入页面模板。 在上一节中，只有来自 `now.strftime` 调用的日期和时间是动态的，这意味着所有其他内容都可以放置在页面模板中。

Django 页模板是包含多个称为 "变量" 的替换标记的 HTML 块。 变量由 `{{` 和 `}}` 表示，例如 `{{ content }}` 。 然后，Django 的模板模块会将变量替换为你在代码中提供的动态内容。

下面的步骤演示了如何使用页面模板：

1. 在包含 Django 项目的 *BasicProject* 文件夹下，打开 *settings.py* 文件。 向列表中添加应用名称 "HelloDjangoApp `INSTALLED_APPS` "。 向列表中添加应用程序时，会显示 Django 项目，其中包含一个包含应用的 "HelloDjangoApp" 名称的文件夹：

    ```python
    INSTALLED_APPS = [
        'HelloDjangoApp',
        # Other entries...
    ]
    ```

1. 在 *settings.py* 文件中，确保 `TEMPLATES` 对象包含 (默认包含) 的以下行。 以下代码指示 Django 在已安装的应用的 *模板* 文件夹中查找模板：

    ```json
    'APP_DIRS': True,
    ```

1. 在 HelloDjangoApp 文件夹中，打开 templates/HelloDjangoApp/index.html 页面模板文件（在 VS 2017 15.7 及更早版本中，则为 templates/index.html），查看其是否包含一个变量 `{{ content }}`    ：

    ```html
    <html>
    <head><title></title></head>

    <body>

    {{ content }}

    </body>
    </html>
    ```

1. 在 *HelloDjangoApp* 文件夹中，打开 *views.py* 文件并将函数替换 `index` 为以下使用 `django.shortcuts.render` helper 函数的代码。 `render` 帮助程序为使用页面模板提供了一个简化的界面。 确保保留所有现有 `from` 语句。

    ```python
    from django.shortcuts import render   # Added for this step

    def index(request):
        now = datetime.now()

        return render(
            request,
            "HelloDjangoApp/index.html",  # Relative path from the 'templates' folder to the template file
            # "index.html", # Use this code for VS 2017 15.7 and earlier
            {
                'content': "<strong>Hello Django!</strong> on " + now.strftime("%A, %d %B, %Y at %X")
            }
        )
    ```

    的第一个参数 `render` 是 request 对象，后跟应用的 *templates* 文件夹内模板文件的相对路径。 在适当情况下，将为视图支持的模板文件命名。 `render` 的第三个参数则是模板引用的变量字典。 可以在字典中包含对象，在这种情况下，模板中的变量可以引用 `{{ object.property }}` 。

1. 运行项目并观察输出。 应该会看到类似于步骤2-2 的消息，指示该模板工作正常。

    请注意，在属性中 `content` 使用的 HTML 只呈现为纯文本，因为 `render` 函数会自动对 HTML 进行转义。 自动转义可防止意外漏洞遭受注入攻击。 开发人员通常会从一页收集输入，并通过模板占位符将其用作另一页中的值。 还可以通过转义来提醒您最好将 HTML 保存在页面模板和代码外。 此外，根据需要创建更多的变量很简单。 例如，更改带有 *模板* 的 *index.html* 文件，使其与以下标记相匹配。 以下标记将添加页标题，并保留页模板中的所有格式：

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

    然后，若要为页面模板中的所有变量提供值，请按照此处的说明编写 `index` 视图函数：

    ```python
    def index(request):
        now = datetime.now()

        return render(
            request,
            "HelloDjangoApp/index.html",  # Relative path from the 'templates' folder to the template file
            # "index.html", # Use this code for VS 2017 15.7 and earlier
            {
                'title' : "Hello Django",
                'message' : "Hello Django!",
                'content' : " on " + now.strftime("%A, %d %B, %Y at %X")
            }
        )
    ```

1. 停止服务器并重新启动项目。 确保页面正确呈现：

    :::image type="content" source="media/django/step02-result.png" alt-text="正在使用模板运行应用。":::

1. <a name="template-namespacing"></a>Visual Studio 2017 版本15.7 及更早版本：作为最后一步，将模板移动到与你的应用同名的子文件夹中。 子文件夹将创建一个命名空间，并避免与可能添加到项目中的其他应用程序发生冲突。  (VS 2017 15.8 + 中的模板会自动为你执行此操作。 ) 也就是说，在名为 *HelloDjangoApp* 的 *模板* 中创建一个子文件夹，将 *index.html* 文件移动到该子文件夹，然后修改 `index` view 函数。 `index`View 函数将引用模板的新路径 *HelloDjangoApp/index.html*。 然后运行项目，验证页面是否正确呈现，并停止服务器。

1. 根据 [步骤 2-2](#commit-to-source-control)中所述，根据需要，将更改提交到源控件并更新远程存储库。

### <a name="question-do-page-templates-have-to-be-in-a-separate-file"></a>问：页面模板必须在一个单独的文件中吗？

答：通常，模板保留在单独的 HTML 文件中。 你还可以使用内联模板。 若要保持标记和代码之间的干净分离，建议使用单独的文件。

### <a name="question-templates-must-use-the-html-file-extension"></a>问：模板必须使用 .html 文件扩展名？

答：页面模板文件的 *.html* 扩展是完全可选的，因为在函数的第二个参数 `render` 中标识文件的确切相对路径。 但是，Visual Studio (和其他编辑器) 会提供代码完成和语法着色功能等功能，其中包含 *.html* 文件，这就是页面模板并非严格 HTML 的情况。

事实上，在使用 Django 项目时，Visual Studio 会自动检测具有 Django 模板的 HTML 文件，并提供某些自动完成功能。 例如，在开始键入 Django 页面模板注释 `{#` 时，Visual Studio 会自动提供右边的 `#}` 字符。 编辑 **""** > 添加"菜单 (工具栏上的"注释选择"和"取消注释选择") 也使用模板注释而不是 HTML 注释。

### <a name="question-when-i-run-the-project-i-see-an-error-that-the-template-cant-be-found-whats-wrong"></a>问：运行项目时，看到一个错误，指出找不到模板。 为什么会这样？

答：如果看到找不到模板的错误，请确保将应用添加到 Django 项目 *settings.py 列表中*`INSTALLED_APPS`。 如果没有该条目，Django 将不知道在应用的 *templates 文件夹中要查找* 的内容。

### <a name="question-why-is-template-namespacing-important"></a>问：为什么模板命名空间如此重要？

答：当 Django 查找函数中引用 `render` 的模板时，它使用与相对路径匹配的第一个文件。 如果同一项目中有多个 Django 应用，其模板的文件夹结构相同，则一个应用可能会无意中使用另一个应用中的模板。 若要避免此类错误，请始终在应用的 *templates* 文件夹下创建一个与应用名称匹配的子文件夹，以避免任何重复。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [为静态文件提供服务、添加页面和使用模板继承](learn-django-in-visual-studio-step-03-serve-static-files-and-add-pages.md)

## <a name="go-deeper"></a>深入了解

- [编写你的第一个 Django 应用，第 1 部分 - 视图](https://docs.djangoproject.com/en/2.0/intro/tutorial01/#write-your-first-view) (docs.djangoproject.com)
- 有关 Django 模板的更多功能（如包含和继承），请参阅 [Django 模板语言](https://docs.djangoproject.com/en/2.0/ref/templates/language/) (docs.djangoproject.com)
- [inLearning 上的正则表达式培训](https://www.linkedin.com/learning/topics/regular-expressions) (LinkedIn)
- GitHub 上的教程源代码：[Microsoft/python-sample-vs-learning-django](https://github.com/Microsoft/python-sample-vs-learning-django)
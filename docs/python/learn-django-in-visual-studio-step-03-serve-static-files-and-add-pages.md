---
title: 学习 Visual Studio 中的 Django 教程的第 3 步，静态文件和页面
titleSuffix: ''
description: Visual Studio 项目上下文中的 Django 基础的演练，特别演示如何提供静态文件、向应用程序添加页和使用模板继承。
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
ms.openlocfilehash: db7e9d307ffb90ad1fa55dd8cb34ce9f587a33b5
ms.sourcegitcommit: 169b7b66d13b7e3c86097b42206dd33389cd9166
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2022
ms.locfileid: "138148675"
---
# <a name="step-3-serve-static-files-add-pages-and-use-template-inheritance-with-django-app"></a>步骤 3：通过 Django 应用提供静态文件、添加页面和使用模板继承

**上一步：[使用视图和页面模板创建 Django 应用](learn-django-in-visual-studio-step-02-create-an-app.md)**

在本教程的前面步骤中，已了解如何使用单个 HTML 页面创建最小的 Django 应用。 但是，新式 web 应用包含多个页面。 新式网页使用 CSS 和 JavaScript 文件等共享资源提供一致的样式和行为。

在此步骤中，你将了解如何：

> [!div class="checklist"]
> - 使用 Visual Studio 项模板快速添加具有方便样本代码的不同类型的新文件（步骤 3-1）
> - 将 Django 项目设置为 (步骤3-2 中提供静态文件) 
> - 向应用添加其他页（步骤 3-3）
> - 使用模板继承创建跨页使用的标头和导航栏（步骤 3-4）

## <a name="step-3-1-become-familiar-with-item-templates"></a>步骤 3-1：熟悉项模板

开发 Django 应用程序时，通常会添加多个 Python、HTML、CSS 和 JavaScript 文件。 对于每种文件类型 (可能需要用于部署) 的文件 *web.config* ，Visual Studio 提供了方便入门的 [项模板](python-item-templates.md)。

若要查看可用的模板，请在 **解决方案资源管理器** 中，右键单击要在其中创建项目的文件夹，然后选择 "**添加**  >  **新项**"。

:::image type="content" source="media/django/step03-add-new-item-dialog.png" alt-text="Visual Studio 中的 &quot;添加新项&quot; 对话框。":::

若要使用模板，请选择所需的模板，指定文件的名称，然后选择 " **添加**"。 以这种方式添加项会自动将文件添加到 Visual Studio 项目中，并标记对源代码管理所做的更改。

### <a name="question-how-does-visual-studio-know-which-item-templates-to-offer"></a>问：Visual Studio 如何知道要提供哪些项模板？

答：Visual Studio 项目文件 (.pyproj) 包含一个项目类型标识符，它将其标记为 Python 项目。 Visual Studio 使用类型标识符来仅显示适用于项目类型的项模板。 这样，Visual Studio 可以为许多项目类型提供一组丰富的项模板，而无需每次都对其进行排序。

## <a name="step-3-2-serve-static-files-from-your-app"></a>步骤 3-2：从应用中提供静态文件

在使用 (的任何框架) 使用 Python 生成的 web 应用中，Python 文件始终在 web 主机的服务器上运行。 Python 文件也永远不会传输到用户的计算机。 但其他文件（如 CSS 和 JavaScript）由浏览器独占使用。 因此，只要请求，主机服务器就会按原样传递它们。 此类文件称为“静态”文件，无需你编写任何代码，Django 可以自动交付它们。

默认情况下，Django 项目设置为从应用的 *静态* 文件夹提供静态文件，这要归功于 Django 项目的 *settings.py* 文件中的行：

```python
# Static files (CSS, JavaScript, Images)
# https://docs.djangoproject.com/en/1.9/howto/static-files/

STATIC_URL = '/static/'

STATIC_ROOT = posixpath.join(*(BASE_DIR.split(os.path.sep) + ['static']))
```

你可以使用你喜欢的任何文件夹结构在 *静态* 中组织文件，然后在该文件夹中使用相对路径来引用这些文件。 若要演示此过程，请执行以下步骤，将 CSS 文件添加到应用，然后使用 *index.html* 模板中的样式表：

1. 在解决方案资源管理器中，右键单击 Visual Studio 项目中的“HelloDjangoApp”文件夹，依次选择“添加” > “新文件夹”，并命名文件夹 `static`   。

1. 右键单击 static 文件夹，然后选择“添加” > “新项”  。 在出现的对话框中，选择 **样式表** 模板，命名该文件 `site.css` ，然后选择 " **添加**"。

    :::image type="content" source="media/django/step-03-add-new-item-static-file.png" alt-text="为静态文件添加新项对话框。":::

    site.css 文件出现在项目中，并在编辑器中打开。 文件夹结构应如下图所示：

    :::image type="content" source="media/django/step03-static-file-structure.png" alt-text="静态文件结构，如解决方案资源管理器中所示。":::

1. 将 *web.config* 文件的内容替换为以下代码，并保存该文件：

    ```css
    .message {
        font-weight: 600;
        color: blue;
    }
    ```

1. 将应用的 *templates/HelloDjangoApp/index.html* 文件的内容替换为以下代码。 此代码会将步骤 2 `<span>` 中使用的元素替换 `<strong>` 为引用 `message` 样式类的。 使用样式类，可以更灵活地为元素设置样式。  (如果使用 VS 2017 15.7 和更早版本时未将 *index.html* 文件移入 *模板* 中的子文件夹，请参阅步骤2-4 中的 [模板 namespacing](learn-django-in-visual-studio-step-02-create-an-app.md#template-namespacing) 。 ) 

    ```html
    <html>
        <head>
            <title>{{ title }}</title>
            {% load static %} <!-- Instruct Django to load static files -->
            <link rel="stylesheet" type="text/css" href="{% static 'site.css' %}" />
        </head>
        <body>
            <span class="message">{{ message }}</span>{{ content }}
        </body>
    </html>
    ```

1. 运行项目以观察结果。 完成后，请停止服务器并将所做的更改提交到源控件（如果你喜欢 (如 [步骤 2](learn-django-in-visual-studio-step-02-create-an-app.md#commit-to-source-control)) 中所述）。

### <a name="question-what-is-the-purpose-of-the--load-static--tag"></a>问： {% load static%} 标记的用途是什么？

答：在指示像 `<head>` 和 `<body>` 这样的元素中的静态文件之前，需要使用 `{% load static %}` 行。 在此部分所示的示例中，"静态文件" 是指自定义的 Django 模板标记集，它允许您使用 `{% static %}` 语法来引用静态文件。 如果没有 `{% load static %}`，那么在应用运行时，将看到异常。

### <a name="question-are-there-any-conventions-for-organizing-static-files"></a>问：是否有组织静态文件的任何约定？

答：你可以按所需方式在 *静态* 文件夹中添加其他 CSS、JAVASCRIPT 和 HTML 文件。 组织静态文件的一种典型方法是创建名为 fonts、scripts 和 content 的子文件夹（用于样式表和任何其他文件）    。 在每种情况下，请记住在引用的相对文件路径 `{% static %}` 中包含这些文件夹。

### <a name="question-can-i-complete-the-same-task-without-using-the--load-static--tag"></a>问：是否可以在不使用 {% load static%} 标记的情况下完成相同的任务？

答：可以。

```html
<html>
    <head>
        <title>{{ title }}</title>
        <link rel="stylesheet" type="text/css" href="../../static/site.css" />
    </head>
    <body>
        <span class="message">{{ message }}</span>{{ content }}
    </body>
</html>
```

## <a name="step-3-3-add-a-page-to-the-app"></a>步骤 3-3：向应用添加一个页面

向应用程序添加另一页将：

- 添加用于定义视图的 Python 函数。
- 添加用于页面标记的模板。
- 将必需的路由添加到 Django 项目的 urls.py 文件中。

以下步骤将 "关于" 页添加到 "HelloDjangoApp" 项目，并从主页链接到该页：

1. 在 **解决方案资源管理器** 中，右键单击 **templates/HelloDjangoApp** 文件夹。 选择 "**添加**  >  **新项**"，然后选择 " **HTML 页**" 项模板。 将文件命名为“`about.html`”，并选择“添加”。

    :::image type="content" source="media/django/step-03-add-new-item-about-file.png" alt-text="为文件 &quot;添加新项&quot; 对话框。":::

    > [!Tip]
    > 如果 "**添加**" 菜单中未显示 "**新建项目**" 命令，请确保已停止服务器，以便 Visual Studio 退出调试模式。

1. 将 *about.html* 的内容替换为下面的标记 (将指向主页的显式链接替换为步骤 3-4) 中的简单导航栏：

    ```html
    <html>
        <head>
            <title>{{ title }}</title>
            {% load static %}
            <link rel="stylesheet" type="text/css" href="{% static 'site.css' %}" />
        </head>
        <body>
            <div><a href="home">Home</a></div>
            {{ content }}
        </body>
    </html>
    ```

1. 打开应用的 views.py 文件，并添加使用该模板的名为 `about` 的函数：

    ```python
    def about(request):
        return render(
            request,
            "HelloDjangoApp/about.html",
            {
                'title' : "About HelloDjangoApp",
                'content' : "Example app page for Django."
            }
        )
    ```

1. 打开 Django 项目的 urls.py 文件，将以下行添加到 `urlPatterns` 数组：

    ```python
    url(r'^about$', HelloDjangoApp.views.about, name='about'),
    ```

1. 打开 *templates/HelloDjangoApp/index.html* 文件并在元素下方 `<body>` 添加以下行以链接到 "关于" 页面 (你将在步骤3-4 中将此链接替换为导航栏) ：

    ```html
    <div><a href="about">About</a></div>
    ```

1. 若要保存所有文件，请使用“文件” > “全部保存”菜单命令，或只需按 Ctrl+Shift+S。 （从技术上讲，不需要执行此步骤，因为在 Visual Studio 中运行项目会自动保存文件。 不过，这是一个很好的了解。 ) 

1. 运行该项目以观察结果并检查页面之间的导航。 完成后，关闭服务器。

### <a name="question-i-tried-using-index-for-the-link-to-the-home-page-but-it-didnt-work-why"></a>问：我曾尝试使用“index”来链接到主页，但它不起作用。 为什么？

答案：尽管 *views.py* 文件中的 view 函数命名 `index` 为，Django 项目的 *URLS.PY* 文件中的 URL 路由模式不包含与字符串 "index" 匹配的正则表达式。 若要匹配字符串，需要为模式 `^index$` 添加另一个条目。

如下面部分所示，更好的方法是使用页面模板中的 `{% url '<pattern_name>' %}` 标记来引用模式的 *名称* 。 在这种情况下，Django 将为您创建正确的 URL。 例如，用 `<div><a href="{% url 'index' %}">Home</a></div>` 替换 about.html 中的 `<div><a href="home">Home</a></div>`。 在这里使用“index”会起作用，因为 urls.py 中的第一个 URL 模式实际上被命名为“index”（依据 `name='index'` 参数）。 也可以用“home”来引用第二种模式。

## <a name="step-3-4-use-template-inheritance-to-create-a-header-and-nav-bar"></a>步骤 3-4：使用模板继承创建标头和导航栏

新式 web 应用不会在每个页面上使用显式导航链接，而是使用品牌标头和导航栏。 导航栏提供最重要的页面链接、弹出菜单等。 若要确保所有页面都具有相同的页眉和导航栏，请不要在每个页面模板中重复相同的代码。 相反，你希望在一个位置定义所有页面的公共部分。

Django 的模板系统提供两种方法，用于跨多个模板重复使用特定元素：包括和继承。

- 包含  是可以使用语法 `{% include <template_path> %}` 在引用模板的特定位置插入的另一个页面模板。 如果您想要在代码中动态更改路径，则还可以使用变量。 在页面的正文中使用包含，以将共享模板纳入页面上的特定位置。

- 继承使用页面模板开头的 `{% extends <template_path> %}` 来指定共享基本模板，然后会在此模板上生成引用模板。 继承通常用于定义应用页面的共享布局、导航栏和其他结构，使引用模板只能添加或修改称为 " *块*" 的基本模板的特定区域。

在这两种情况下，`<template_path>` 对应于应用的 templates 文件夹（还允许 `../` 或 `./`）。

基本模板使用 `{% block <block_name> %}` 和 `{% endblock %}` 标记来标示块。 如果引用模板随后使用具有相同块名称的标记，那么它的块内容将替代基本模板的内容。

以下步骤演示继承：

1. 在应用的 *templates/HelloDjangoApp* 文件夹中，创建一个新的 HTML 文件。 右键单击 **templates/HelloDjangoApp** 文件夹，选择 "**添加**  >  **新项**"，然后选择 " **HTML 页**" 项模板。 将文件命名为“`layout.html`”，并选择“添加”。

    :::image type="content" source="media/django/step-03-add-new-item-layout-file.png" alt-text="为布局文件添加新项对话框。":::

1. 将 *layout.html* 文件的内容替换为以下标记。 你可以看到，此模板包含一个名为 "content" 的块，这是所有引用页面都需要替换：

    ```html
    <!DOCTYPE html>
    <html>
    <head>
        <meta charset="utf-8" />
        <title>{{ title }}</title>
        {% load static %}
        <link rel="stylesheet" type="text/css" href="{% static 'site.css' %}" />
    </head>

    <body>
        <div class="navbar">
           <a href="/" class="navbar-brand">Hello Django</a>
           <a href="{% url 'home' %}" class="navbar-item">Home</a>
           <a href="{% url 'about' %}" class="navbar-item">About</a>
        </div>

        <div class="body-content">
    {% block content %}{% endblock %}
            <hr/>
            <footer>
                <p>&copy; 2018</p>
            </footer>
        </div>
    </body>
    </html>
    ```

1. 向应用的 static/site.css 文件添加以下样式（本教程不会尝试在此处演示响应式设计；这些样式仅仅是为了生成一个有趣的结果）  ：

    ```css
    .navbar {
        background-color: lightslategray;
        font-size: 1em;
        font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
        color: white;
        padding: 8px 5px 8px 5px;
    }

    .navbar a {
        text-decoration: none;
        color: inherit;
    }

    .navbar-brand {
        font-size: 1.2em;
        font-weight: 600;
    }

    .navbar-item {
        font-variant: small-caps;
        margin-left: 30px;
    }

    .body-content {
        padding: 5px;
        font-family:'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }
    ```

1. 修改 *templates/HelloDjangoApp/index.html* 文件以引用基本模板并重写内容块。 可以看到，通过使用继承，此模板变得很简单：

    ```html
    {% extends "HelloDjangoApp/layout.html" %}
    {% block content %}
    <span class="message">{{ message }}</span>{{ content }}
    {% endblock %}
    ```

1. 修改 *templates/HelloDjangoApp/about.html* 文件以引用基本模板并重写内容块：

    ```html
    {% extends "HelloDjangoApp/layout.html" %}
    {% block content %}
    {{ content }}
    {% endblock %}
    ```

1. 运行服务器并观察结果。 完成后，关闭服务器。

    :::image type="content" source="media/django/step-03-navigation-bar.png" alt-text="正在运行应用，显示导航栏。":::

1. 你已经对应用进行了大幅更改，现在是[将所做的更改提交到源代码管理](learn-django-in-visual-studio-step-02-create-an-app.md#commit-to-source-control)的好时机。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [使用完整的 Django Web 项目模板](learn-django-in-visual-studio-step-04-full-django-project-template.md)

## <a name="go-deeper"></a>深入了解

- [将 Web 应用部署到 Azure App Service](publishing-python-web-applications-to-azure-from-visual-studio.md)
- [编写你的第一个 Django 应用，第 3 部分（视图）](https://docs.djangoproject.com/en/2.0/intro/tutorial03/) (docs.djangoproject.com)
- 有关 Django 模板的更多功能（如控制流），请参阅 [Django 模板语言](https://docs.djangoproject.com/en/2.0/ref/templates/language/) (docs.djangoproject.com)
- 有关使用 `{% url %}` 标记的完整详细信息，请参阅 [Django 模板的内置模板标记和筛选器参考](https://docs.djangoproject.com/en/2.0/ref/templates/builtins/)中的 [URL](https://docs.djangoproject.com/en/2.0/ref/templates/builtins/#url) (docs.djangoproject.com)
- GitHub 上的教程源代码：[Microsoft/python-sample-vs-learning-django](https://github.com/Microsoft/python-sample-vs-learning-django)

---
title: 了解 Visual Studio 中的 Django 教程的第 5 步，身份验证
titleSuffix: ''
description: Visual Studio 项目上下文中 Django 基础知识的演练，具体介绍了 Django Web 项目模板提供的身份验证功能。
ms.date: 11/19/2018
ms.topic: tutorial
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.technology: vs-python
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 17a6ee7cbf622eb90debd961ba36f159bf7fbc6c
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122156521"
---
# <a name="step-5-authenticate-users-in-django"></a>步骤 5：在 Django 中对用户进行身份验证

**上一步：[使用完整的 Django Web 项目模板](learn-django-in-visual-studio-step-04-full-django-project-template.md)**

::: moniker range="vs-2017"
身份验证是 Web 应用的常见需求，因此“Django Web 项目”模板包含基本的身份验证流。 （本教程步骤 6 中讨论的“投票 Django Web 项目”模板也包括相同的流。）在使用任意 Django 项目模板时，Visual Studio 包含 Django 项目的 settings.py 中身份验证所需的所有模块  。
::: moniker-end

::: moniker range=">=vs-2019"
身份验证是 Web 应用的常见需求，因此“Django Web 项目”模板包含基本的身份验证流。 在使用任意 Django 项目模板时，Visual Studio 包含 Django 项目的 settings.py 中身份验证所需的所有模块。
::: moniker-end

在此步骤中，你将了解：

> [!div class="checklist"]
> - 如何使用 Visual Studio 模板中提供的身份验证流（步骤 5-1）

## <a name="step-5-1-use-the-authentication-flow"></a>步骤 5-1：使用身份验证流

以下步骤执行身份验证流，并介绍所涉及项目的各个部分：

1. 如果尚未遵循项目根目录 readme.html 文件中的说明来创建超级用户（管理员）帐户，请现在执行此操作  。

1. 使用“调试” > “启动调试”(F5)，从 Visual Studio 运行应用    。 当应用出现在浏览器中时，观察“登录”  是否显示在导航栏右上方。

    ![Django Web 项目应用页上的登录控件](media/django/step05-login-control.png)

1. 打开 templates/app/layout.html，并观察 `<div class="navbar ...>` 元素是否包含标记 `{% include app/loginpartial.html %}`  。 `{% include %}` 标记指示 Django 的模板化系统在包含模板中此时所含的文件内容中进行拉取。

1. 打开 templates/app/loginpartial.html 并观察它如何使用条件标记 `{% if user.is_authenticated %}` 与 `{% else %}` 标记来呈现不同的 UI 元素，具体取决于是否已对用户进行身份验证  ：

    ```html
    {% if user.is_authenticated %}
    <form id="logoutForm" action="/logout" method="post" class="navbar-right">
        {% csrf_token %}
        <ul class="nav navbar-nav navbar-right">
            <li><span class="navbar-brand">Hello {{ user.username }}!</span></li>
            <li><a href="javascript:document.getElementById('logoutForm').submit()">Log off</a></li>
        </ul>
    </form>

    {% else %}

    <ul class="nav navbar-nav navbar-right">
        <li><a href="{% url 'login' %}">Log in</a></li>
    </ul>

    {% endif %}
    ```

1. 由于首次启动应用时未对任何用户进行身份验证，因此该模板代码仅呈现指向相对路径“login”的“登录”链接。 正如 urls.py 中所指定的那样（如前一部分所示），该路由映射到 `django.contrib.auth.views.login` 视图  。 该视图将收到以下数据：

    ```python
    {
        'template_name': 'app/login.html',
        'authentication_form': app.forms.BootstrapAuthenticationForm,
        'extra_context':
        {
            'title': 'Log in',
            'year': datetime.now().year,
        }
    }
    ```

    在这里，`template_name` 标识登录页的模板，在本例中为 templates/app/login.html  。 `extra_context` 属性被添加到提供给模板的默认上下文数据中。 最后，`authentication_form` 指定用于登录的窗体类，它在模板中显示为 `form` 对象。 默认值为 `AuthenticationForm`（来自 `django.contrib.auth.views`）；Visual Studio 项目模板改为使用应用 forms.py 文件中定义的窗体  ：

    ```python
    from django import forms
    from django.contrib.auth.forms import AuthenticationForm
    from django.utils.translation import ugettext_lazy as _

    class BootstrapAuthenticationForm(AuthenticationForm):
        """Authentication form which uses boostrap CSS."""
        username = forms.CharField(max_length=254,
                                   widget=forms.TextInput({
                                       'class': 'form-control',
                                       'placeholder': 'User name'}))
        password = forms.CharField(label=_("Password"),
                                   widget=forms.PasswordInput({
                                       'class': 'form-control',
                                       'placeholder':'Password'}))
    ```

    如你所见，此窗体类派生自 `AuthenticationForm` 且专门替代用户名和密码字段来添加占位符文本。 Visual Studio 模板包括此显式代码，前提是你可能需要自定义窗体，比如添加密码强度验证。

1. 导航到登录页时，应用随即会显示 login.html 模板  。 变量 `{{ form.username }}` 和 `{{ form.password }}` 呈现来自 `BootstrapAuthenticationForm` 的 `CharField` 窗体。 还有一个内置部分用于显示验证错误，如果选择添加这些服务，会有一个用于社交登录的现成元素。

    ```html
    {% extends "app/layout.html" %}

    {% block content %}

    <h2>{{ title }}</h2>
    <div class="row">
        <div class="col-md-8">
            <section id="loginForm">
                <form action="." method="post" class="form-horizontal">
                    {% csrf_token %}
                    <h4>Use a local account to log in.</h4>
                    <hr />
                    <div class="form-group">
                        <label for="id_username" class="col-md-2 control-label">User name</label>
                        <div class="col-md-10">
                            {{ form.username }}
                        </div>
                    </div>
                    <div class="form-group">
                        <label for="id_password" class="col-md-2 control-label">Password</label>
                        <div class="col-md-10">
                            {{ form.password }}
                        </div>
                    </div>
                    <div class="form-group">
                        <div class="col-md-offset-2 col-md-10">
                            <input type="hidden" name="next" value="/" />
                            <input type="submit" value="Log in" class="btn btn-default" />
                        </div>
                    </div>
                    {% if form.errors %}
                    <p class="validation-summary-errors">Please enter a correct user name and password.</p>
                    {% endif %}
                </form>
            </section>
        </div>
        <div class="col-md-4">
            <section id="socialLoginForm"></section>
        </div>
    </div>

    {% endblock %}
    ```

1. 提交表单时，Django 会尝试对凭据（如超级用户凭据）进行身份验证。 如果身份验证失败，你将仍处于当前页面，但 `form.errors` 将设置为 true。 如果身份验证成功，Django 将导航到“下一步”字段中的相对 URL `<input type="hidden" name="next" value="/" />`，在本例中为主页 (`/`)。

1. 现在，当主页再次呈现，`user.is_authenticated` 属性会在 loginpartial.html 模板呈现时为“true”  。 因此，将看到“Hello (用户名)”消息和“注销”   。 可以在应用其他部分中使用 `user.is_authenticated` 来检查身份验证。

    ![Django Web 项目应用页上的 Hello 消息和注销控件](media/django/step05-logoff-control.png)

1. 若要确定经过身份验证的用户是否有权访问特定资源，需要从数据库中检索用户特定的权限。 有关详细信息，请参阅[使用 Django 身份验证系统](https://docs.djangoproject.com/en/2.0/topics/auth/default/#permissions-and-authorization)（Django 文档）。

1. 特别需要指出的是，超级用户或管理员有权访问内置 Django 管理员界面，方法是使用相对 URL“/admin/”和“/admin/doc/”。 要启用这些接口，请执行以下操作：

    1. 将 docutils Python 包安装到环境中。 一个不错的办法是将“docutils”添加到 requirements.txt 文件，然后在“解决方案资源管理器”中展开该项目，再展开“Python 环境”节点，然后右键单击正在使用的环境并选择“通过 requirements.txt 安装”     。

    1. 打开 Django 项目的 urls.py 并从下列条目中删除默认注释  ：

        ```python
        from django.conf.urls import include
        from django.contrib import admin
        admin.autodiscover()

        # ...
        urlpatterns = [
            # ...
            url(r'^admin/doc/', include('django.contrib.admindocs.urls')),
            url(r'^admin/', include(admin.site.urls)),
        ]
        ```

    1. 在 Django 项目的 settings.py 文件内，导航到 `INSTALLED_APPS` 集合并添加 `'django.contrib.admindocs'`  。

    1. 重新启动应用时，可以导航到“/admin/”和“/admin/doc/”并执行任务，如创建其他用户帐户。

        ![Django 管理员界面](media/django/step05-administrator-interface.png)

1. 身份验证流的最后一部分是注销。 正如 loginpartial.html 中所示，“注销”链接只需对相对 URL“/login”执行 POST 操作，这由内置视图 `django.contrib.auth.views.logout` 处理   。 此视图不显示任何 UI，只需导航到主页（如“^logout$”模式 urls.py 中所示）  。 若要显示注销页，首先按照下面的方式更改 URL，添加“template_name”属性并删除“next_page”属性：

    ```python
    url(r'^logout$',
        django.contrib.auth.views.logout,
        {
            'template_name': 'app/loggedoff.html',
            # 'next_page': '/',
        },
        name='logout')
    ```

    然后通过以下（最小）内容创建 templates/app/loggedoff.html  ：

    ```html
    {% extends "app/layout.html" %}
    {% block content %}
    <h3>You have been logged off</h3>
    {% endblock %}
    ```

    结果如下所示：

    ![添加的注销页](media/django/step05-logged-off-page.png)

1. 完成所有操作后，停止服务器，并再次将所做的更改提交到源代码管理。

### <a name="question-what-is-the-purpose-of-the--csrf_token--tag-that-appears-in-the-form-elements"></a>问：\<form\> 元素中的 {% csrf_token %} 标记有何用途？

答：`{% csrf_token %}` 标记包含 Django 的内置[跨网站请求伪造 (csrf) 保护](https://docs.djangoproject.com/en/2.0/ref/csrf/)（Django 文档）。 通常将此标记添加到涉及 POST、PUT 或 DELETE 请求方法的任何元素（如窗体）。 然后，模板呈现函数 (`render`) 会插入必要的保护。

## <a name="next-steps"></a>后续步骤

::: moniker range="vs-2017"
- [使用投票 Django Web 项目模板](learn-django-in-visual-studio-step-06-polls-django-web-project-template.md)
::: moniker-end

::: moniker range=">=vs-2019"
> [!Note]
> 如果已在本教程的整个课程中将 Visual Studio 解决方案提交到源代码管理，那么现在是执行另一个提交的好时机。 解决方案应匹配 GitHub 上的教程源代码：[Microsoft/python-sample-vs-learning-django](https://github.com/Microsoft/python-sample-vs-learning-django)。

现在，你已了解 Visual Studio 中“空白 Django Web 项目”和“Django Web 项目”模板的全部内容。 你已了解包括使用视图和模板在内的所有 Django 基础知识，并了解了有关路由、身份验证和使用数据库模型的相关内容。 现在应能够使用任何所需的视图和模型来创建你自己的 Web 应用。

在开发计算机上运行 Web 应用只是使应用可供客户使用的一个步骤。 后续步骤可能包括以下任务：

- 将 Web 应用部署到生产服务器，如 Azure 应用服务。 请参阅[发布到 Azure 应用服务](publishing-python-web-applications-to-azure-from-visual-studio.md)。

- 通过创建一个名为 templates/404.html 的模板来自定义 404 页。 如果存在该模板，Django 会使用此模板而不是其默认模板。 有关详细信息，请参阅 Django 文档中的[错误视图](https://docs.djangoproject.com/en/2.0/ref/views/#error-views)。

- 在 tests.py 中编写单元测试；Visual Studio 项目模板为这些测试提供起始点，若要了解更多信息，可以在 Django 文档的[编写首个 Django 应用，第 5 部分 - 测试](https://docs.djangoproject.com/en/2.0/intro/tutorial05/)和[在 Django 中进行测试](https://docs.djangoproject.com/en/2.0/topics/testing/)中找到。

- 将应用从 SQLite 更改为生产级数据存储，如 PostgreSQL、MySQL 和 SQL Server（它们都可以在 Azure 上托管）。 如[何时使用 SQLite](https://www.sqlite.org/whentouse.html) (sqlite.org) 中所述，SQLite 适用于低到中等规模的流量站点（一天点击量不足 100K），不建议用于高点击量网站。 此外，它还仅限于一台计算机，因此不能在任何多服务器场景中使用，例如负载均衡和异地复制。 有关 Django 对其他数据库的支持的信息，请参阅[数据库设置](https://docs.djangoproject.com/en/2.0/intro/tutorial02/#database-setup)。 另外，还可以使用 [Azure SDK for Python](/azure/python/)，以便使用 Azure 存储服务，如表和 blob。

- 在 Azure DevOps 等服务上设置持续集成/持续部署管道。 除了使用源代码管理（通过 Azure Repos、GitHub 或在其他位置）外，还可以将 Azure DevOps 项目配置为自动运行单元测试作为发布的先决条件，并在部署到生产环境之前，将管道配置为部署到暂存服务器以进行附加测试。 此外，Azure DevOps 还与 App Insights 等监视解决方案集成，并使用敏捷规划工具闭合整个周期。 有关详细信息，请参阅[在 Azure DevOps 项目中为 Python 创建 CI/CD 管道](/azure/devops-project/azure-devops-project-python?view=vsts&preserve-view=true)以及常规 [Azure DevOps 文档](/azure/devops/?view=vsts&preserve-view=true)。
::: moniker-end
## <a name="go-deeper"></a>深入了解

- [Django 中的用户身份验证](https://docs.djangoproject.com/en/2.0/topics/auth/) (docs.djangoproject.com)
- GitHub 上的教程源代码：[Microsoft/python-sample-vs-learning-django](https://github.com/Microsoft/python-sample-vs-learning-django)

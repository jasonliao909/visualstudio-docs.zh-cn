---
title: 学习 Visual Studio 中的 Django 教程的第 6 步，为项目模板投票
titleSuffix: ''
description: Visual Studio 项目上下文中 Django 基础知识的演练，具体介绍了投票 Django Web 项目模板的功能，例如管理自定义。
ms.date: 02/24/2022
ms.custom: devdivchpfy22
ms.topic: tutorial
author: rjmolyneaux
ms.author: rmolyneaux
manager: jmartens
ms.technology: vs-python
monikerRange: vs-2017
ms.workload:
- python
- data-science
ms.openlocfilehash: d2917866fcf589f763b42538df6c23e74940eaff
ms.sourcegitcommit: edf8137cd90c67b6078a02c93094f7e1c3bf8930
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2022
ms.locfileid: "139551360"
---
# <a name="step-6-use-the-polls-django-web-project-template"></a>步骤 6：使用投票 Django Web 项目模板

上一步：[在 Django 中对用户进行身份验证](learn-django-in-visual-studio-step-05-django-authentication.md)

了解Visual Studio"Django Web Project"模板后，现在可以查看第三个 Django 模板"投票 Django Web Project"。 投票 Django Web Project模板基于相同的基本代码生成，并演示如何使用数据库。

在此步骤中，你将了解如何：

> [!div class="checklist"]
> - 从模板创建项目并初始化数据库（步骤 6-1）
> - 了解数据模型（步骤 6-2）
> - 应用迁移（步骤 6-3）
> - 了解由项目模板创建的视图和页面模板（步骤 6-4）
> - 创建自定义管理界面（步骤 6-5）

使用此模板创建的项目类似于按照 Django 文档编写第一个 [Django](https://docs.djangoproject.com/en/2.0/intro/tutorial01/) 应用教程获得的项目。Web 应用包含一个公共站点，可让用户查看投票并投票。 若要管理投票，你还具有自定义管理界面。 接口使用与"Django Web Project"模板相同的身份验证系统。 它还通过实现 Django 模型来利用数据库，如以下部分所述。

## <a name="step-6-1-create-the-project-and-initialize-the-database"></a>步骤 6-1：创建项目并初始化数据库

1. 在Visual Studio，转到解决方案资源管理器，右键单击本教程前面创建的 **LearningDjango** 解决方案。 选择 **"添加** > **""Project**"。  (如果要使用新 >  > 解决方案，请改为选择"文件"**"新建Project**.) 

1. 在"**新建Project**"对话框中，搜索并选择"投票 **Django Web Project** 模板。 将项目称为"DjangoPolls"，然后选择"确定 **"**。

1. 与 Visual Studio 中的其他项目模板一样，"投票 Django Web Project"模板 *包含一requirements.txt* 文件。 Visual Studio会提示安装依赖项的位置。 出现提示时，选择"安装到 **虚拟环境中**"选项，在"添加 **虚拟** 环境"对话框中选择"创建"以接受默认值。

1. Python 完成虚拟环境的设置后，请按照显示的 *readme.html。* 这些说明将帮助你初始化数据库并创建 Django 超级用户 (管理员角色) 。 步骤是首先右键单击 解决方案资源管理器 中的 **DjangoPolls** **项目，然后选择** **PythonDjango**  >  Migrate 命令。 然后，再次右键单击项目，选择 **"Python** > **""Django 创建超级用户"** 命令，然后按照提示操作。  (如果首先尝试创建超级用户，则会看到错误，因为数据库尚未初始化。) 

1. 右键单击 Visual Studio 中的项目并选择"设置为启动"解决方案资源管理器，将 **DjangoPolls** 项目设置为 **Project。** 启动调试器时将运行的启动项目以粗体显示。

1. 选择 **"调试** > ""**开始** (**F5**) 或使用工具栏上的 **"Web 服务器**"按钮运行服务器。

    :::image type="content" source="media/django/run-web-server-toolbar-button.png" alt-text="运行 web 服务器工具栏按钮Visual Studio。":::

1. 模板创建的应用有三个页面，即"主页"、"关于"和"联系人"，你将使用顶部导航栏在页面间导航。 几分钟检查应用的不同部分。  ("关于"和"联系人"页类似于"Django Web Project"，不会进一步讨论。) 

    :::image type="content" source="media/django/step06-full-app-view.png" alt-text="投票 Django Web 应用的完整浏览器Project视图。":::

1. 此外，在导航 **栏中** 选择"管理"链接。 " **管理** "链接显示登录屏幕，以演示仅向经过身份验证的管理员授权管理界面。 使用超级用户凭据，你被路由到"/admin"页面。 使用项目模板时，页面默认启用。

    :::image type="content" source="media/django/step06-polls-administrative-interface.png" alt-text="投票 Django Web 应用管理Project视图。":::

1. 可以在以下各节中使应用保持运行状态。

    如果要停止应用并提交对源代码管理所做的更改 [，](learn-django-in-visual-studio-step-02-create-an-app.md#commit-to-source-control)请首先打开"更改"**页团队资源管理器。** 右键单击虚拟环境文件夹 **(环境)** ，然后选择"忽略 **这些本地项"**。

### <a name="examine-the-project-contents"></a>检查项目内容

从"投票 Django Web Project"模板创建的项目应熟悉项目中的其他项目Visual Studio。 本文的其他步骤汇总了重大更改和新增功能，即数据模型和其他视图。

### <a name="question-what-does-the-django-migrate-command-do"></a>问：Django 迁移命令的作用是什么？

答： **Django Migrate** 命令专门 `manage.py migrate` 运行 命令，该命令运行 *app/migrations* 文件夹中以前未运行的任何脚本。 在这种情况下，此命令运行文件夹中的 0001_initial.py 脚本，以便在数据库中设置必要的架构。

迁移脚本本身由 命令 `manage.py makemigrations` 创建。 迁移脚本扫描应用的 models.py 文件，将其与数据库的当前状态进行比较，然后生成必要的脚本来迁移数据库架构以匹配当前模型。 在一段时间更新和修改模型时，Django 的此功能非常强大。 通过生成和运行迁移，可以轻松地使模型和数据库保持同步。

本文稍后将介绍步骤 6-3 中的迁移。

## <a name="step-6-2-understand-data-models"></a>步骤 6-2：了解数据模型

app/models.py 中定义了名为“投票”和“选择”的应用模型。 每个模型都是派生自 的 Python 类 `django.db.models.Model`。 为了定义模型中的字段并映射到数据库列，模型使用 `models` 类的方法，如 和 `CharField` `IntegerField`。

```python
from django.db import models
from django.db.models import Sum

class Poll(models.Model):
    """A poll object for use in the application views and repository."""
    text = models.CharField(max_length=200)
    pub_date = models.DateTimeField('date published')

    def total_votes(self):
        """Calculates the total number of votes for this poll."""
        return self.choice_set.aggregate(Sum('votes'))['votes__sum']

    def __unicode__(self):
        """Returns a string representation of a poll."""
        return self.text

class Choice(models.Model):
    """A poll choice object for use in the application views and repository."""
    poll = models.ForeignKey(Poll)
    text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)

    def votes_percentage(self):
        """Calculates the percentage of votes for this choice."""
        total = self.poll.total_votes()
        return self.votes / float(total) * 100 if total > 0 else 0

    def __unicode__(self):
        """Returns a string representation of a choice."""
        return self.text
```

如你所见，“投票”保留其 `text` 字段中的说明和 `pub_date` 中的发布日期。 这些字段是数据库中投票所有的唯一字段；`total_votes` 字段在运行时进行计算。

“选择”与通过 `poll` 字段实现的“投票”相关，在 `text` 中包含说明，并在 `votes` 中保留该选择的计数。 该字段 `votes_percentage` 是运行时计算的，在数据库中找不到。

字段类型的完整列表包括 `CharField`（受限文本）、`TextField`（不受限制的文本）、`EmailField`、`URLField`、`DateTimeField`、`IntegerField`、`DecimalField`、`BooleanField`、`ForeignKey`，和 `ManyToMany`。 每个字段都采用一些属性，如 `max_length`。 `blank=True` 属性表示字段是可选的；`null=true` 表示值是可选的。 还有一个 `choices` 属性，该属性将值限制于数据值/显示值元组数组中的值。 （请参阅 Django 文档中的[模型字段引用](https://docs.djangoproject.com/en/2.0/ref/models/fields/)。）

可以通过检查项目中的 *db.sqlite3* 文件来确认数据库中存储的内容。 若要检查文件，可以使用 [SQLite 浏览器等工具](https://sqlitebrowser.org/)。 在数据库中，会看到“选择”模型中像 `poll` 这样的外键字段存储为 `poll_id`；Django 会自动处理映射。

一般来说，在 Django 中使用数据库意味着可以以独占方式通过模型进行工作，使 Django 可以代表你管理基础数据库。

### <a name="seed-the-database-from-samplesjson"></a>从 samples.json 设定数据库种子

最初，数据库不包含任何投票。 可以使用"/admin"URL 中的管理界面手动添加投票。 还可以访问正在运行的站点上的"/seed"页，使用应用的 *samples.json* 文件中定义的投票来添加数据库种子。

Django *项目的 urls.py 文件* 具有一个添加的 URL 模式 `url(r'^seed$', app.views.seed, name='seed'),`。 app/views.py 中的 `seed` 视图加载 samples.json 文件并创建必要的模型对象。 Django 随后会在基础数据库中自动创建匹配记录。

请注意使用 `@login_required` 修饰器来指示视图的授权级别。

```python
@login_required
def seed(request):
    """Seeds the database with sample polls."""
    samples_path = path.join(path.dirname(__file__), 'samples.json')
    with open(samples_path, 'r') as samples_file:
        samples_polls = json.load(samples_file)

    for sample_poll in samples_polls:
        poll = Poll()
        poll.text = sample_poll['text']
        poll.pub_date = timezone.now()
        poll.save()

        for sample_choice in sample_poll['choices']:
            choice = Choice()
            choice.poll = poll
            choice.text = sample_choice
            choice.votes = 0
            choice.save()

    return HttpResponseRedirect(reverse('app:home'))
```

若要查看效果，请首先运行应用，以查看不存在投票。 然后访问“/seed”URL，当应用返回到主页时，应会看到投票已变得可用。 同样，可以随时使用 [SQLite 浏览器](https://sqlitebrowser.org/)之类的工具检查原始 db.sqlite3 文件。

:::image type="content" source="media/django/step06-app-with-seeded-database.png" alt-text="使用种子数据库Project Django Web 应用。":::

### <a name="question-is-it-possible-to-initialize-the-database-using-the-django-administrative-utility"></a>问：是否可以使用 Django 管理实用工具初始化数据库？

答：是的，可以使用 [django-admin loaddata 命令](https://docs.djangoproject.com/en/2.0/ref/django-admin/#loaddata)来完成与应用中的种子设定页相同的任务。 处理完整的 Web 应用时，可以使用这两种方法的组合。 从命令行初始化数据库，然后将此处的种子页转换为 API。 然后，可以发送任何其他任意 JSON，而不是依赖于硬编码文件。

## <a name="step-6-3-use-migrations"></a>步骤 6-3：使用迁移

创建项目`manage.py makemigrations` (使用 Visual Studio) 菜单中的上下文菜单运行命令时，Django 创建了 *app/migrations/0001_initial.py* 文件。 此文件包含用于创建初始数据库表的脚本。

随着时间的推移，你一定会对模型进行更改，Django 使基础数据库架构与模型保持最新变得简单。 一般工作流如下：

1. 对 models.py 文件中的模型进行更改。
1. 在 Visual Studio 中，右键单击“解决方案资源管理器”中的项目，并选择“Python” > “Django 迁移”命令。 如前面所描述，此命令在 app/migrations 中生成脚本，将数据库从当前状态迁移到新状态。
1. 若要将脚本应用到实际数据库，请再次右键单击该项目，然后选择 **"Python** > **""Django Migrate"**。

Django 跟踪已应用于任何给定数据库的迁移。 因此，在运行 "迁移" 命令时，Django 会应用所需的任何迁移。 例如，如果创建一个新的空数据库，则运行 "迁移" 命令将通过应用每个迁移脚本来提供最新的当前模型。 同样，如果在一台开发计算机上更改多个模型并生成迁移，可以通过在生产服务器上运行迁移命令将累积迁移应用到生产数据库。 Django 只会再次应用那些自从生产数据库的最后一次迁移以来生成的迁移脚本。

若要查看更改模型的效果，请尝试执行以下步骤：

1. 通过在 `pub_date` 字段后添加以下行来添加一个可选的 `author` 字段，向 app/models.py 中的投票模型添加可选的作者字段：

    ```python
    author = models.CharField(max_length=100, blank=True)
    ```

1. 保存文件，然后右键单击解决方案资源管理器中的“DjangoPolls”，并选择“Python” > “Django 迁移”命令。
1. 选择“项目” > “显示所有文件”命令来查看 migrations 文件夹中新生成的脚本，其名称以 002_auto_ 开头   。 右键单击该文件，然后选择“包括在项目中”。 然后，可以再次选择“项目” > “显示所有文件”以还原原始视图。 （有关此步骤的详细信息，请参阅下面的第二个问题。）
1. 如果需要，请打开该文件以检查 Django 脚本如何从以前的模型状态变更为新状态。
1. 再次右键单击 Visual Studio 项目并选择“Python” > “Django 迁移”，向数据库应用更改。
1. 如果需要，请在相应查看器中打开该数据库以确认更改。

总体而言，Django 的迁移功能意味着您永远无需手动管理您的数据库架构。 只需对模型进行更改，生成迁移脚本，并通过迁移命令应用它们。

### <a name="question-what-happens-if-i-forget-to-run-the-migrate-command-after-making-changes-to-models"></a>问：如果在对模型进行更改之后忘记运行迁移命令，会发生什么情况？

答：如果模型与数据库中的内容不匹配，则 Django 会在运行时失败，并出现相应的异常。 例如，如果你忘记迁移上一部分中所示的模型更改，你将看到错误 " **没有此类列： app_poll 作者**：

:::image type="content" source="media/django/step06-exception-when-forgetting-to-migrate.png" alt-text="未迁移模型更改时显示的错误。":::

### <a name="question-why-doesnt-solution-explorer-show-newly-generated-scripts-after-running-django-make-migrations"></a>问：为什么在运行 Django 迁移后解决方案资源管理器不显示新生成的脚本？

答：尽管新生成的脚本存在于 app/migrations 文件夹中，并在运行“Django 迁移”命令时应用，但它们不会自动显示在解决方案资源管理器中，因为还没有将它们添加到 Visual Studio 项目中。 若要使其可见，请首先选择“项目” > “显示所有文件”菜单命令或下图所示的工具栏按钮。 " **显示所有文件** " 命令会导致 **解决方案资源管理器** 显示项目文件夹中的所有文件，对尚未添加到项目本身的项使用点式大纲图标。 右键单击要添加的文件并选择“包括在项目中”，在下一次提交时，也会将文件附加到源代码管理中。

:::image type="content" source="media/django/step06-include-migrations-script-in-project.png" alt-text="包含在解决方案资源管理器中 Project 命令。":::

### <a name="question-can-i-see-what-migrations-would-be-applied-before-running-the-migrate-command"></a>问：可在运行迁移命令之前看到要应用的迁移吗？

答：可以，请使用 [django-admin showmigrations 命令](https://docs.djangoproject.com/en/2.0/ref/django-admin/#showmigrations)。

## <a name="step-6-4-understand-the-views-and-page-templates-created-by-the-project-template"></a>步骤 6-4：了解由项目模板创建的视图和页面模板

"轮询 Django web Project" 模板生成的大多数视图（例如 "关于" 和 "联系人" 页的视图）都类似于 "Django Web Project" 模板创建的视图。 投票应用不同于其主页使用模型的方式，因此，有几个附加页面可用于投票和查看轮询结果。

首先， *urls.py* 文件中 Django 项目的 `urlpatterns` 数组中的第一行是一个简单的应用程序视图路由。 相反，它在应用自己的 urls.py 文件中拉取：

```python
from django.conf.urls import url, include
import app.views

urlpatterns = [
    url(r'^', include('app.urls', namespace="app")),
    # ..
]
```

然后，app/urls.py 文件包含一些更有趣的路由代码（添加了说明性注释）：

```python
urlpatterns = [
    # Home page routing
    url(r'^$',
        app.views.PollListView.as_view(
            queryset=Poll.objects.order_by('-pub_date')[:5],
            context_object_name='latest_poll_list',
            template_name='app/index.html',),
        name='home'),

    # Routing for a poll page, which use URLs in the form <poll_id>/,
    # where the id number is captured as a group named "pk".
    url(r'^(?P<pk>\d+)/$',
        app.views.PollDetailView.as_view(
            template_name='app/details.html'),
        name='detail'),

    # Routing for <poll_id>/results pages, again using a capture group
    # named pk.
    url(r'^(?P<pk>\d+)/results/$',
        app.views.PollResultsView.as_view(
            template_name='app/results.html'),
        name='results'),

    # Routing for <poll_id>/vote pages, with the capture group named
    # poll_id this time, which becomes an argument passed to the view.
    url(r'^(?P<poll_id>\d+)/vote/$', app.views.vote, name='vote'),
]
```

如果你不熟悉此处使用的复杂正则表达式，则可以将表达式粘贴到 [regex101.com](https://regex101.com/) 中，以获取明文语言的说明。  (需要通过在前斜杠后面添加反斜杠 `\` 来对正斜杠 `/` 进行转义; 在 Python 中，由于字符串的前缀（即 "raw"），因此 `r` 不需要进行转义。 ) 

在 Django 中，语法 `?P<name>pattern` 创建了一个名为 `name` 的组，它以出现的顺序作为参数传递给视图。 如前面代码所示，`PollsDetailView` 和 `PollsResultsView` 接收名为 `pk` 的参数，`app.views.vote` 接收名为 `poll_id` 的参数。

你还可以看到，大多数视图不直接引用 *应用/视图* 中的视图函数 py。 相反，大多数引用从 `django.views.generic.ListView` 或 `django.views.generic.DetailView` 派生的同一文件中的类。 基类提供 `as_view` 方法，它采用 `template_name` 参数来标识模板。 `ListView`用于主页的基类还需要一个 `queryset` 包含数据的属性和 `context_object_name` 一个属性，该属性具有要在模板中引用数据的变量名称。 在本例中，该值为 `latest_poll_list`。

现在，你可以检查 `PollListView` 主页的，它在 " *应用/视图*" 中定义为以下内容。 py：

```python
class PollListView(ListView):
    """Renders the home page, with a list of all polls."""
    model = Poll

    def get_context_data(self, **kwargs):
        context = super(PollListView, self).get_context_data(**kwargs)
        context['title'] = 'Polls'
        context['year'] = datetime.now().year
        return context
```

此处所做的全部工作就是确定视图处理的模型 (轮询) ，并重写 `get_context_data` 方法以向上下文添加 `title` 和 `year` 值。

模板的核心 (templates/app/index.html) 如下所示：

```html
{% if latest_poll_list %}
<table class="table table-hover">
    <tbody>
        {% for poll in latest_poll_list %}
        <tr>
            <td>
                <a href="{% url 'app:detail' poll.id %}">{{poll.text}}</a>
            </td>
        </tr>
        {% endfor %}
    </tbody>
</table>
{% else %}
<!-- ... other content omitted ... -->
{% endif %}
```

简单地说，模板在中 `latest_poll_list` 接收轮询对象列表，然后循环访问该列表以创建一个表行，其中包含使用轮询 `text` 值的每个投票的链接。 在 `{% url %}` 标签中，“app:detail”指的是 app/urls.py 中命名为“detail”的 URL 模式，使用 `poll.id` 作为参数。 此操作的效果是 Django 使用相应模式创建一个 URL，并将其用于链接。 这位未来的校对是指您可以随时更改 URL 模式，生成的链接会自动更新以匹配。

app/views.py 中的 `PollDetailView` 和 `PollResultsView` 类（此处未显示）看起来几乎与 `PollListView` 完全相同，只不过它们是派生自 `DetailView`。 然后它们各自的模板（即 app/templates/details.html 和 app/templates/results.html）在各种 HTML 控件中通过模型放置相应的字段。 *details.html* 中的一个独特之处在于，轮询的选择包含在 HTML 窗体中。 提交后，它会向/vote URL 进行 POST。 如前文所述，URL 模式将路由到 `app.views.vote` ，该模式按以下方式实现 (注意 `poll_id` 参数，该参数在此视图的路由中使用的正则表达式中的命名组) ：

```python
def vote(request, poll_id):
    """Handles voting. Validates input and updates the repository."""
    poll = get_object_or_404(Poll, pk=poll_id)
    try:
        selected_choice = poll.choice_set.get(pk=request.POST['choice'])
    except (KeyError, Choice.DoesNotExist):
        return render(request, 'app/details.html', {
            'title': 'Poll',
            'year': datetime.now().year,
            'poll': poll,
            'error_message': "Please make a selection.",
    })
    else:
        selected_choice.votes += 1
        selected_choice.save()
        return HttpResponseRedirect(reverse('app:results', args=(poll.id,)))
```

此处，视图没有自己对应的模板，就像其他页面一样。 相反，它会验证所选投票，如果投票不存在，则显示 404（以防他人输入类似于“vote/1a2b3c”的 URL）。 然后，它将确保投票选项对于投票有效。 否则，`except` 块只会再次呈现包含错误消息的详细信息页。 如果选择有效，该视图将统计投票，并会重定向到结果页。

## <a name="step-6-5-create-a-custom-administration-interface"></a>步骤 6-5：创建自定义管理界面

如前面的步骤6-1 所示，"轮询 Django Web Project" 模板的最后几部分是对默认 Django 管理界面的自定义扩展。 默认接口适用于用户和组管理。 投票项目模板还添加可用于管理投票的功能。

首先，Django 项目 urls.py 中的 URL 模式默认包含 `url(r'^admin/', include(admin.site.urls)),`；还包含注释掉的“admin/doc”模式。

然后，应用程序将包含文件 *admin.py*，当你访问管理界面时，Django 会自动运行该文件。 感谢包含 `django.contrib.admin` 在 *settings.py* 的数组中 `INSTALLED_APPS` 。 该文件中的代码（正如项目模板所提供的）如下所示：

```python
from django.contrib import admin
from app.models import Choice, Poll

class ChoiceInline(admin.TabularInline):
    """Choice objects can be edited inline in the Poll editor."""
    model = Choice
    extra = 3

class PollAdmin(admin.ModelAdmin):
    """Definition of the Poll editor."""
    fieldsets = [
        (None, {'fields': ['text']}),
        ('Date information', {'fields': ['pub_date']}),
    ]
    inlines = [ChoiceInline]
    list_display = ('text', 'pub_date')
    list_filter = ['pub_date']
    search_fields = ['text']
    date_hierarchy = 'pub_date'

admin.site.register(Poll, PollAdmin)
```

如您所见， `PollAdmin` 该类派生自 `django.contrib.admin.ModelAdmin` ，并使用其管理的模型中的名称 `Poll` 自定义其许多字段。 在 Django 文档的 [ModelAdmin 选项](https://docs.djangoproject.com/en/2.0/ref/contrib/admin/#modeladmin-options)上对这些字段进行了说明。

然后，对 `admin.site.register` 的调用将此类连接到模型 (`Poll`) 并将其包含在管理界面上。 总体结果如下所示：

:::image type="content" source="media/django/step06-polls-administrative-interface.png" alt-text="轮询 Django Web Project 应用的管理视图。":::

## <a name="next-steps"></a>后续步骤

> [!Note]
> 如果已在本教程的整个课程中将 Visual Studio 解决方案提交到源代码管理，那么现在是执行另一个提交的好时机。 解决方案应匹配 GitHub 上的教程源代码：[Microsoft/python-sample-vs-learning-django](https://github.com/Microsoft/python-sample-vs-learning-django)。

你现在已在 Visual Studio 中探讨了 "空白 Django web Project"、"Django web Project" 和 "轮询 Django web Project" 模板。 你已经了解了 Django 的所有基本知识，例如使用视图和模板。 还介绍了路由、身份验证和使用的数据库模型。 现在应能够使用任何所需的视图和模型来创建你自己的 Web 应用。

在开发计算机上运行 Web 应用只是使应用可供客户使用的一个步骤。 后续步骤可能包括以下任务：

- 将 Web 应用部署到生产服务器，如 Azure 应用服务。 请参阅[发布到 Azure 应用服务](publishing-python-web-applications-to-azure-from-visual-studio.md)。

- 通过创建一个名为 templates/404.html 的模板来自定义 404 页。 如果存在该模板，Django 会使用此模板而不是其默认模板。 有关详细信息，请参阅 Django 文档中的[错误视图](https://docs.djangoproject.com/en/2.0/ref/views/#error-views)。

- 在 tests.py 中编写单元测试；Visual Studio 项目模板为这些测试提供起始点，若要了解更多信息，可以在 Django 文档的[编写首个 Django 应用，第 5 部分 - 测试](https://docs.djangoproject.com/en/2.0/intro/tutorial05/)和[在 Django 中进行测试](https://docs.djangoproject.com/en/2.0/topics/testing/)中找到。

- 将应用从 SQLite 更改为生产级数据存储，如 PostgreSQL、MySQL 和 SQL Server（它们都可以在 Azure 上托管）。 如 [何时使用 SQLite](https://www.sqlite.org/whentouse.html) (sqlite.org) 的说明，SQLite 适用于少于 100 K 命中/天的低到中等流量站点。 但是，对于较大的卷，不建议使用 SQLite。 它还限于单台计算机，因此不能用于任何多服务器方案，例如负载平衡和异地复制。 有关 Django 对其他数据库的支持的信息，请参阅[数据库设置](https://docs.djangoproject.com/en/2.0/intro/tutorial02/#database-setup)。 另外，还可以使用 [Azure SDK for Python](/azure/python/)，以便使用 Azure 存储服务，如表和 blob。

- 在 Azure DevOps 等服务上设置持续集成/持续部署管道。 除了通过 Azure Repos 或 GitHub 或其他) 地方使用源代码管理 (以外，还可以将 Azure DevOps Project 配置为自动运行单元测试，作为版本的先决条件。 在部署到生产环境之前，你还可以将管道配置为部署到过渡服务器以进行更多测试。 此外，Azure DevOps 还与 App Insights 等监视解决方案集成，并使用敏捷规划工具闭合整个周期。 有关详细信息，请参阅[在 Azure DevOps 项目中为 Python 创建 CI/CD 管道](/azure/devops-project/azure-devops-project-python?view=vsts&preserve-view=true)以及常规 [Azure DevOps 文档](/azure/devops/?view=vsts&preserve-view=true)。

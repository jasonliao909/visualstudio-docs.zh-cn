---
title: 学习 Visual Studio 中的 Django 教程的第 1 步，Django 基础知识
titleSuffix: ''
description: Visual Studio 项目上下文中 Django 基础知识的演练，演示 Visual Studio 如何为 Django 开发提供支持。
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
ms.openlocfilehash: bd3bb5bd5b9ac4864c9eb38f290d34d7cdd7fc1f
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122156612"
---
# <a name="tutorial-get-started-with-the-django-web-framework-in-visual-studio"></a>教程：在 Visual Studio 中开始使用 Django Web 框架

[Django](https://www.djangoproject.com/) 是高级 Python 框架，用于快速、安全及可扩展的 Web 开发。 本教程将在 Visual Studio 提供的项目模板上下文中探讨 Django 框架，以简化基于 Django 的 Web 应用的创建过程。

在本教程中，你将了解：

::: moniker range="vs-2017"
- 使用“空白 Django Web 项目”模板在 Git 存储库中创建一个基本 Django 项目（步骤 1）
- 使用模板创建一个单页 Django 应用，并呈现该页面（步骤 2）
- 为静态文件提供服务、添加页面和使用模板继承（步骤 3）
- 使用 Django Web 项目模板创建包含多个页面和响应式设计的应用（步骤 4）
- 对用户进行身份验证（步骤 5）
- 使用投票 Django Web 项目模板创建使用模型、数据库迁移和管理界面自定义项的应用（步骤 6）
::: moniker-end

::: moniker range=">=vs-2019"
- 使用“空白 Django Web 项目”模板在 Git 存储库中创建一个基本 Django 项目（步骤 1）
- 使用模板创建一个单页 Django 应用，并呈现该页面（步骤 2）
- 为静态文件提供服务、添加页面和使用模板继承（步骤 3）
- 使用 Django Web 项目模板创建包含多个页面和响应式设计的应用（步骤 4）
- 对用户进行身份验证（步骤 5）
::: moniker-end

## <a name="prerequisites"></a>系统必备

- Windows 版 Visual Studio 2017 及以上版本，且具有以下选项：
  - “Python 开发”工作负载（安装程序中的“工作负载”选项卡）   。 有关说明，请参阅[在 Visual Studio 中安装 Python 支持](installing-python-support-in-visual-studio.md)。
  - “代码工具”下“单个组件”选项卡上的“适用于 Windows 的 Git”和“适用于 Visual Studio 的 GitHub 扩展”     。

Django 项目模板也包含在针对 Visual Studio 的 Python 工具的所有早期版本中，尽管细节可能不同于本教程中讨论的内容（特别是不同于早期版本的 Django框架）。

Visual Studio for Mac 当前不支持 Python 开发。 在 Mac 和 Linux 上，使用 [Visual Studio Code 中的 Python 扩展](https://code.visualstudio.com/docs/python/python-tutorial)。

### <a name="visual-studio-projects-and-django-projects"></a>“Visual Studio 项目”和“Django 项目”

在 Django 术语中，“Django 项目”由几个网站级别配置文件和一个或多个“应用”组成，可以将它们部署到 Web 主机，从而创建一个完整的 Web 应用程序。 一个 Django 项目可以包含多个应用，而同一个应用可以存在于多个 Django 项目中。

Visual Studio 项目就其本身而言，可以包含 Django 项目和多个应用。 为简单起见，只要是本教程仅涉及一个“项目”，都指的是 Visual Studio 项目。 如果要表示 Web 应用程序的“Django 项目”部分，则会专门使用“Django 项目”。

本教程将创建一个 Visual Studio 解决方案，其中包含三个独立的 Django 项目，每个项目都包含一个 Django 应用。 通过将项目保留在同一解决方案中，可以轻松地在不同文件之间来回切换以进行比较。

## <a name="step-1-1-create-a-visual-studio-project-and-solution"></a>步骤 1-1：创建 Visual Studio 项目和解决方案

从命令行使用 Django 时，通常会通过运行 `django-admin startproject <project_name>` 命令来启动一个项目。 在 Visual Studio 中，使用“空白 Django Web 项目”模板在 Visual Studio 项目和解决方案中提供相同结构。

1. 在 Visual Studio 中，选择“文件” > “新建” > “项目”，搜索“Django”，然后选择“空白 Django Web 项目”模板。 （还可以在左侧列表的“Python”   > “Web”  中找到模板。）

    ![Visual Studio 中“空白 Django Web 项目”的新建项目对话框](media/django/step01-new-blank-project.png)

1. 在对话框底部的字段中，输入以下信息（如上图所示），然后选择“确定”  ：

    - **名称**：将 Visual Studio 项目的名称设置为“BasicProject”  。 此名称还用于 Django 项目。
    -  位置：指定要在其中创建 Visual Studio 解决方案和项目的位置。
    - **解决方案**：将此控件设置保留为默认“创建新解决方案”选项。
    - **解决方案名称**：设置为“LearningDjango”，适用于本教程中作为多个项目的容器的解决方案。
    -  为解决方案创建目录：保留设置（默认设置）。
    -  创建新的 Git 存储库：选择此选项（默认情况下会清除该选项），以便在 Visual Studio 创建解决方案时创建本地 Git 存储库。 如果未看到此选项，请运行 Visual Studio 安装程序并在“代码工具”下的“单个组件”选项卡上添加“适用于 Windows 的 Git”和“适用于 Visual Studio 的 GitHub 扩展”     。

1. 稍后 Visual Studio 会显示一个对话框，提示“此项目需要外部包”（如下所示）  。 显示此对话框是因为该模板包含引用最新 Django 1.x 包的 requirements.txt 文件。 （选择“显示所需包”  查看确切的依赖项。）

    ![指示项目需要外部包的提示](media/django/step01-requirements-prompt-install-myself.png)

1. 选择选项“我将自行安装”  。 立即创建虚拟环境，确保它会从源代码管理中排除。 （始终可从 requirements.txt 创建该环境  。）

## <a name="step-1-2-examine-the-git-controls-and-publish-to-a-remote-repository"></a>步骤 1-2：检查 Git 控件并发布到远程存储库

由于选择了“新建项目”对话框中的“创建新的 Git 存储库”，在创建过程完成后，项目就已经提交到本地源代码管理。 在此步骤中，你将熟悉 Visual Studio 的 Git 控件和在其中使用源代码管理的“团队资源管理器”  窗口。

1. 在 Visual Studio 主窗口下角处检查 Git 控件。 这些控件从左到右依次显示未推送的提交、未提交的更改、存储库的名称以及当前分支：

    ![Visual Studio 窗口中的 Git 控件](media/django/step01-git-controls.png)

    > [!Note]
    > 如果未选择“新建项目”对话框中的”创建新 Git 存储库“，Git 控件将仅显示用于创建本地存储库的”添加到源代码管理“命令。
    >
    > ![未创建存储库时 Visual Studio 中显示的“添加到源代码管理”](media/django/step01-git-add-to-source-control.png)

1. 选择“更改”按钮，Visual Studio 会在“更改”页上打开“团队资源管理器”窗口。 由于新创建的项目已经自动提交给源代码管理，因此，看不到任何挂起的更改。

    ![“更改”页上的“团队资源管理器”窗口](media/django/step01-team-explorer-changes.png)

1. 在 Visual Studio 状态栏中，选择“未推送的提交”按钮（标有“2”的向上箭头）以打开团队资源管理器中的“同步”页    。 由于你只有一个本地存储库，页面将提供简单的选项将存储库发布到不同的远程存储库。

    ![显示面向源代码管理的可用 Git 存储库选项的“团队资源管理器”窗口](media/django/step01-team-explorer.png)

    可以为自己的项目选择任何所需的服务。 本教程演示了如何使用 GitHub，其中本教程已完成的示例代码保存在 [Microsoft/python-sample-vs-learning-django](https://github.com/Microsoft/python-sample-vs-learning-django) 存储库中。

1. 选择任一“发布”  控件时，“团队资源管理器”  都将提示你输入详细信息。 例如，在发布本教程的示例时，必须首先创建存储库本身，在这种情况下，“推送到远程存储库”  选项将与存储库的 URL 结合使用。

    ![用于推送到现有远程存储库的团队资源管理器窗口](media/django/step01-push-to-github.png)

    如果没有现有存储库，可通过“发布到 GitHub”  和“推送到 Azure DevOps”  选项直接从 Visual Studio 创建一个存储库。

1. 按照本教程执行操作时，请养成定期在 Visual Studio 中使用控件提交和推送更改的习惯。 本教程会在适当时机提醒你。

> [!Tip]
> 要在团队资源管理器中快速导航，请选择标头（上图中显示为“更改”或“推送”）来查看可用页面的弹出菜单    。

### <a name="question-what-are-some-advantages-of-using-source-control-from-the-beginning-of-a-project"></a>问：从项目一开始就使用源代码管理有什么好处？

答：首先，从一开始就使用源代码管理，特别是如果同时还使用远程存储库，就可以提供项目的常规异地备份。 与在本地文件系统上维护项目不同，源代码管理还提供了完整的更改历史记录，用户可以轻松地将单个文件或整个项目还原到以前的状态。 此更改历史记录有助于确定回归的原因（测试失败）。 此外，如果多个人员执行一个项目，则源代码管理必不可少，因为它管理重写并提供冲突解决方案。 最后，源代码管理从根本上来说是一种自动化形式，它为自动化构建、测试和发布管理提供充分准备。 这实际上是将 DevOps 用于项目的第一步，而且由于入门门槛非常低，因此没有理由不从一开始就使用源代码管理。

关于自动化形式的源代码管理的进一步讨论，请参阅 [The Source of Truth: The Role of Repositories in DevOps](/archive/msdn-magazine/2016/september/mobile-devops-the-source-of-truth-the-role-of-repositories-in-devops)（真相之源：DevOps 中的存储库角色），这是 MSDN Magazine 上专为移动应用编写的一篇文章，同样适用于 Web 应用。

### <a name="question-can-i-prevent-visual-studio-from-auto-committing-a-new-project"></a>问：我能否阻止 Visual Studio 自动提交新项目？

答：能。 若要禁用自动提交，请转到“团队资源管理器”中的“设置”页，选择“Git” > “全局设置”，清除标记为“合并后默认提交更改”的选项，然后选择“更新”。

## <a name="step-1-3-create-the-virtual-environment-and-exclude-it-from-source-control"></a>步骤 1-3：创建虚拟环境并从源代码管理中将其排除

你已为项目配置源代码管理，现在可为项目创建包含必需 Django 包的虚拟环境。 然后，可以使用“团队资源管理器”  从源代码管理中排除环境文件夹。

1. 在“解决方案资源管理器”  中，右键单击“Python 环境”  节点并选择“添加虚拟环境”  。

    ![解决方案资源管理器中的“添加虚拟环境”命令](media/django/step01-add-virtual-environment-command.png)

1. 随即出现“添加虚拟环境”对话框，并显示一条消息，指示“已找到 requirements.txt 文件   。” 此消息表示 Visual Studio 使用该文件来配置虚拟环境。

    ![包含 requirements.txt 消息的“添加虚拟环境”对话框](media/django/step01-add-virtual-environment-found-requirements.png)

1. 选择“创建”  以接受默认设置。 （如果你愿意，可以更改虚拟环境名称，这只会更改其子文件夹的名称，但 `env` 是标准约定。）

1. 如果收到提示，同意管理员权限，然后在 Visual Studio 下载和安装包时耐心等待几分钟，对于 Django 来说，这意味着在大约同样数目的子文件夹中展开几千个文件！ 可以在 Visual Studio“输出”  窗口中查看进度。 在等待时，仔细考虑下面的“问题”部分。

1. 在 Visual Studio Git 控件（位于状态栏上）上，选择更改指示器（显示“99&#42;”），这将打开团队资源管理器中的“更改”页    。

    创建虚拟环境带来了数千项更改，但不需要在源代码管理中包含其中任何一项，因为你（或克隆项目的任何人员）始终可从 requirements.txt 重新创建环境。

    要排除虚拟环境，请右键单击 env 文件夹，然后选择“忽略这些本地项”   。

    ![忽略源代码管理更改中的虚拟环境](media/django/step01-ignore-local-items.png)

1. 排除虚拟环境后，剩下的唯一更改是针对项目文件和 .gitignore  。 .gitignore 文件包含虚拟环境文件夹的附加条目  。 可以双击文件查看差异。

1. 输入提交消息，然后选择“全部提交”  按钮，根据需要将提交推送到远程存储库。

### <a name="question-why-do-i-want-to-create-a-virtual-environment"></a>问：为什么需要创建虚拟环境？

答：虚拟环境是隔离应用确切依赖项的好办法。 此类隔离避免了全局 Python 环境中的冲突，有助于进行测试和协作。 随着时间的推移，在开发应用时，总是会引入许多有用的 Python 包。 通过将包保存在特定于项目的虚拟环境中，可以轻松更新项目中介绍该环境的 requirements.txt 文件，该文件包含在源代码管理中  。 如果项目被复制到任何其他计算机（包括生成服务器、部署服务器和其他开发计算机），仅使用 requirements.txt 即可轻松重新创建环境（这就是为什么环境不需要包含在源代码管理中）  。 有关详细信息，请参阅[使用虚拟环境](selecting-a-python-environment-for-a-project.md#use-virtual-environments)。

### <a name="question-how-do-i-remove-a-virtual-environment-thats-already-committed-to-source-control"></a>问：如何删除已经提交给源代码管理的虚拟环境？

答：首先，编辑 .gitignore 文件以排除文件夹：在末尾找到带注释 `# Python Tools for Visual Studio (PTVS)` 的部分，并为虚拟环境文件夹添加一个新行，如 `/BasicProject/env`。 （由于 Visual Studio 不会显示“解决方案资源管理器”  中的文件，请使用“文件”   > “打开”   > “文件”  菜单命令直接打开它。 也可以从团队资源管理器打开文件：在“设置”页上，选择“存储库设置”，转到“忽略和属性文件”部分，然后选择 .gitignore 旁的“编辑”链接。       ）

接下来，打开命令窗口，导航到包含虚拟环境文件夹（如 env）的文件夹（如 BasicProject），然后运行 `git rm -r env`。 然后从命令行 (`git commit -m 'Remove venv'`) 提交这些更改，或从“团队资源管理器”的“更改”页进行提交。

## <a name="step-1-4-examine-the-boilerplate-code"></a>步骤 1-4：检查样本代码

项目创建完成后，检查样本 Django 项目代码（仍与 CLI 命令 `django-admin startproject <project_name>` 生成的代码相同）。

1. 在项目根目录中为 manage.py，即 Visual Studio 自动设置为项目启动文件的 Django 命令行管理实用工具。 可以使用 `python manage.py <command> [options]` 在命令行上运行实用工具。 对于常见的 Django 任务，Visual Studio 提供了方便的菜单命令。 右键单击“解决方案资源管理器”中的项目，然后选择“Python”查看列表。 在本教程中，你将遇到其中的部分命令。

    ![Python 项目上下文菜单上的 Django 命令](media/django/step01-django-commands-menu.png)

2. 在你的项目中是一个与项目名称相同的文件夹。 它包含基本 Django 项目文件：

   - __init.py：告知 Python 此文件夹是 Python 包的空文件。
   - wsgi.py：WSGI 兼容的 Web 服务器执行项目的入口点。 通常将此文件原样保留，因为它为生产 Web 服务器提供挂钩。
   - settings.py：包含在开发 Web 应用的过程中修改的 Django 项目的设置。
   - urls.py：包含同样在开发过程中修改的 Django 项目的内容目录。

     ![解决方案资源管理器中的 Django 项目文件](media/django/step01-django-project-in-solution-explorer.png)

3. 如前文所述，Visual Studio 模板还将 requirements.txt 文件添加到指定 Django 包依赖项的项目中。 该文件旨在邀请你在第一次创建项目时创建虚拟环境。

### <a name="question-can-visual-studio-generate-a-requirementstxt-file-from-a-virtual-environment-after-i-install-other-packages"></a>问：在我安装其他包后，Visual Studio 能否从虚拟环境生成 requirements.txt 文件？

答：能。 展开“Python 环境”  节点，右键单击虚拟环境，并选择“生成 requirements.txt”  命令。 在修改环境，并将对 requirements.txt 所做的更改连同依赖于该环境的任何其他代码更改提交给源代码管理时，建议定期使用此命令  。 如果在生成服务器上设置持续集成，应该在修改环境时生成文件并提交更改。

## <a name="step-1-5-run-the-empty-django-project"></a>步骤 1-5：运行空 Django 项目

1. 在 Visual Studio 中，选择“调试” > “启动调试”(F5) 或使用工具栏上的“Web 服务器”按钮（所看到的浏览器可能会有所不同）：

    ![Visual Studio 中的运行 Web 服务器工具栏按钮](media/django/run-web-server-toolbar-button.png)

1. 运行服务器意味着运行命令 `manage.py runserver <port>`，以启动 Django 内置开发服务器。 如果 Visual Studio 显示“启动调试器失败”并显示无启动文件的相关消息，右键单击解决方案资源管理器中的 manage.py 并选择“设为启动文件”。

1. 在启动服务器时，会看到一个打开的控制台窗口，其中也显示服务器日志。 Visual Studio 将自动打开浏览器并转到 `http://localhost:<port>`。 Django 项目没有任何应用，但是，Django 只显示了一个默认页面，确认目前正常工作：

    ![Django 项目默认视图](media/django/step01-first-run-success.png)

1. 完成后，通过关闭控制台窗口，或使用 Visual Studio 中的“调试”   > “停止调试”  命令来停止服务器。

### <a name="question-is-django-a-web-server-as-well-as-a-framework"></a>问：Django 既是 Web 服务器也是框架吗？

答：是/否。 Django 确实有一个用于开发目的的内置 Web 服务器。 当你在本地运行 Web 应用时（例如在 Visual Studio 中调试时），就会使用此 Web 服务器。 但是在部署到 Web 主机时，Django 会改用主机的 Web 服务器。 Django 项目中的 wsgi.py 模块负责挂接到生产服务器。

### <a name="question-whats-the-difference-between-using-the-debug-menu-commands-and-the-server-commands-on-the-projects-python-submenu"></a>问：在项目 Python 子菜单中使用“调试”菜单命令和服务器命令有何区别？

答：除了“调试”  菜单命令和工具栏按钮之外，还可以使用项目上下文菜单上的“Python”   > “运行服务器”  或“Python”   > “运行调试服务器”  命令来启动服务器。 这两个命令都会打开一个控制台窗口，可以在其中看到运行服务器的本地 URL (localhost:port)。 但是，必须使用该 URL 手动打开浏览器，并且运行调试服务器不会自动启动 Visual Studio 调试器。 如果需要，稍后可以使用“调试”   > “附加到进程”  命令，将调试器附加到正在运行的进程。

## <a name="next-steps"></a>后续步骤

此时，基本 Django 项目不包含任何应用。 在下一步创建一个应用。 因为通常使用的是 Django 应用而不是 Django 项目，因此，暂不需要了解关于样本文件的更多信息。

> [!div class="nextstepaction"]
> [使用视图和页面模板创建 Django 应用](learn-django-in-visual-studio-step-02-create-an-app.md)

## <a name="go-deeper"></a>深入了解

- Django 项目代码：[编写你的第一个 Django 应用，第 1 部分](https://docs.djangoproject.com/en/2.0/intro/tutorial01/) (docs.djangoproject.com)
- 管理实用工具：[django-admin 和 manage.py](https://docs.djangoproject.com/en/2.0/ref/django-admin/) (docs.djangoproject.com)
- GitHub 上的教程源代码：[Microsoft/python-sample-vs-learning-django](https://github.com/Microsoft/python-sample-vs-learning-django)
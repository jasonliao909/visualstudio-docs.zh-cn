---
title: 学习 Visual Studio 中的 Django 教程的第 1 步，Django 基础知识
titleSuffix: ''
description: Visual Studio 项目上下文中 Django 基础知识的演练，演示 Visual Studio 如何为 Django 开发提供支持。
ms.custom: devdivchpfy22
ms.date: 02/03/2022
ms.topic: tutorial
author: rjmolyneaux
ms.author: rmolyneaux
manager: jmartens
ms.technology: vs-python
ms.workload:
- python
- data-science
ms.openlocfilehash: 238e113c0e00deb6ef4592b8bcf1c0c2eec215f7
ms.sourcegitcommit: edf8137cd90c67b6078a02c93094f7e1c3bf8930
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2022
ms.locfileid: "139551739"
---
# <a name="tutorial-get-started-with-the-django-web-framework-in-visual-studio"></a>教程：在 Visual Studio 中开始使用 Django Web 框架

[Django](https://www.djangoproject.com/) 是高级 Python 框架，用于快速、安全及可扩展的 Web 开发。 本教程将在项目模板的上下文中探究 Django framework。 Visual Studio 提供了项目模板，用于简化基于 Django 的 web 应用的创建。

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
- 在 Git 存储库中使用 "空白 Django Web Project" 模板创建一个基本的 Django 项目， (步骤 1) 。
- 创建一个包含一页的 Django 应用，并使用 (步骤 2) 的模板来呈现该页。
- 在步骤 3)  (提供静态文件、添加页和使用模板继承。
- 使用 Django Web Project 模板创建具有多个页面的应用，并 (步骤 4) 创建响应式设计。
-  (步骤 5) 对用户进行身份验证。
::: moniker-end

## <a name="prerequisites"></a>系统必备

::: moniker range="<=vs-2019"
- Windows 版 Visual Studio 2017 及以上版本，且具有以下选项：
  - “Python 开发”工作负载（安装程序中的“工作负载”选项卡）   。 有关说明，请参阅[在 Visual Studio 中安装 Python 支持](installing-python-support-in-visual-studio.md)。
  - “代码工具”下“单个组件”选项卡上的“适用于 Windows 的 Git”和“适用于 Visual Studio 的 GitHub 扩展”     。
::: moniker-end

::: moniker range="vs-2022"
- 具有以下选项的 Windows 上的 Visual Studio 2022：
  - “Python 开发”工作负载（安装程序中的“工作负载”选项卡）   。 有关更多说明，请参阅[在 Visual Studio 中安装 Python 支持](installing-python-support-in-visual-studio.md)。
  - **Git for Windows** 在 "**代码工具**" 下的 "**单个组件**" 选项卡上。
::: moniker-end

Django 项目模板还包括针对 Visual Studio 的 Python 工具的早期版本。 模板详细信息可能与本教程中讨论的详细信息不同 () 的早期版本 Django。

Visual Studio for Mac 目前尚不支持 Python 开发。 在 Mac 和 Linux 上，使用 [Visual Studio Code 中的 Python 扩展](https://code.visualstudio.com/docs/python/python-tutorial)。

### <a name="visual-studio-projects-and-django-projects"></a>“Visual Studio 项目”和“Django 项目”

在 Django 术语中，"Django 项目" 包含多个站点级配置文件以及一个或多个 "应用"。 若要创建完整的 web 应用程序，你可以将这些应用部署到 web 主机。 一个 Django 项目可以包含多个应用，而同一个应用可以存在于多个 Django 项目中。

Visual Studio 项目可以包含 Django 项目和多个应用。 只要本教程只引用一个 "项目"，就会引用 Visual Studio 项目。 当它引用 web 应用程序的 "Django 项目" 部分时，它会专门引用 "Django 项目"。

在本教程中，你将创建单个 Visual Studio 解决方案，其中包含三个单独的 Django 项目。 每个项目都包含一个 Django 应用。 您可以通过将项目保持在同一个解决方案中，轻松地在不同文件之间进行转换以进行比较。

## <a name="step-1-1-create-a-visual-studio-project-and-solution"></a>步骤 1-1：创建 Visual Studio 项目和解决方案

在从命令行使用 Django 时，通常通过运行 `django-admin startproject <project_name>` 命令来启动项目。 在 Visual Studio 中，"空白 Django Web Project" 模板在 Visual Studio 项目和解决方案中提供了相同的结构。

::: moniker range="<=vs-2019"
1. 在 Visual Studio 中，选择“文件” > “新建” > “项目”，搜索“Django”，然后选择“空白 Django Web 项目”模板。  (还可以在 " **Python**  >  **Web** " 的左侧列表中找到该模板。 ) 

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

1. 选择选项“我将自行安装”  。 立即创建虚拟环境，确保它会从源代码管理中排除。  (你始终可以从 *requirements.txt* 创建环境。 ) 
::: moniker-end

::: moniker range="vs-2022"
1. 在 Visual Studio 中，选择 "**文件** > " "**新建** > " **Project**，搜索 "Django"，然后选择 "**空白 Django Web Project** " 模板，然后选择 "**下一步**"。

    :::image type="content" source="media/django/step-01-create-new-project-screen-1-vs-2022.png" alt-text="空白 Django Web Project 的 Visual Studio 中的 &quot;新建项目&quot; 对话框。":::
  
1. 输入以下信息，然后选择 " **创建**"：

    - **Project 名称**：将 Visual Studio 项目的名称设置为 **BasicProject**。 此名称还用于 Django 项目。
    - **Location**：指定要在其中创建 Visual Studio 解决方案和项目的位置。
    - **解决方案**：将此控件设置为默认的 " **创建新解决方案** " 选项。
    - **解决方案名称**：设置为 **LearningDjango**，这对于本教程中的多个项目，它适合作为容器的解决方案。

::: moniker-end

## <a name="step-1-2-examine-the-git-controls-and-publish-to-a-remote-repository"></a>步骤 1-2：检查 Git 控件并发布到远程存储库

::: moniker range="<=vs-2019"
由于在 "**新建 Project** " 对话框中选择了 "**创建新的 Git 存储库**"，因此在创建过程完成时，项目已提交到本地源代码管理。 在此步骤中，你将熟悉 Visual Studio 的 Git 控件和在其中使用源代码管理的“团队资源管理器”  窗口。

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

1. 选择任一“发布”  控件时，“团队资源管理器”  都将提示你输入详细信息。 例如，在发布本教程中的示例时，必须先创建存储库本身，在这种情况下，" **推送到远程存储库** " 选项与存储库的 URL 一起使用。

    ![用于推送到现有远程存储库的团队资源管理器窗口](media/django/step01-push-to-github.png)

    如果没有现有存储库，可通过“发布到 GitHub”  和“推送到 Azure DevOps”  选项直接从 Visual Studio 创建一个存储库。

1. 按照本教程执行操作时，请养成定期在 Visual Studio 中使用控件提交和推送更改的习惯。 本教程会在适当时机提醒你。

> [!Tip]
> 要在团队资源管理器中快速导航，请选择标头（上图中显示为“更改”或“推送”）来查看可用页面的弹出菜单    。

::: moniker-end

::: moniker range="vs-2022"
在此步骤中，您将熟悉 Visual Studio 的 Git 控件和 **团队资源管理器**。 在 **团队资源管理器** 窗口中，您将使用源代码管理。

1. 若要将项目提交到本地源代码管理，请执行以下操作：
    1. 选择 Visual Studio 主窗口底部的 "**添加到源代码管理**" 命令。
    1. 然后，选择 " **Git** " 选项。
    1. 现在，你将转到 " **创建 Git 存储库** " 窗口，你可以在其中创建并推送新的存储库。

    :::image type="content" source="media/django/step01-git-add-to-source-control.png" alt-text="创建 Git 存储库。":::

1. 创建存储库后，会在底部显示一组新的 Git 控件。 从左到右，这些控件显示个未推送提交、未提交的更改、当前分支以及存储库的名称。

    :::image type="content" source="media/django/step01-git-controls.png" alt-text="Visual Studio 窗口中的 Git 控件。":::

1. 选择 " **Git 更改** " 按钮。 然后 Visual Studio 在 **团队资源管理器** 中打开 " **Git 更改**" 页。 由于新创建的项目已自动提交到源代码管理，因此看不到任何挂起的更改。

    :::image type="content" source="media/django/step-01-team-explorer-git-changes-vs-2022.png" alt-text="&quot;Git 更改&quot; 页上的团队资源管理器窗口。":::

1. 在 Visual Studio 状态栏中，选择“未推送的提交”按钮（标有“2”的向上箭头）以打开团队资源管理器中的“同步”页    。 " **同步** " 页提供了用于将本地存储库发布到不同远程存储库的简单选项。

    :::image type="content" source="media/django/step01-team-explorer.png" alt-text="显示源代码管理的可用 Git 存储库选项团队资源管理器窗口。":::

    可以为项目选择所需的任何服务。 本教程演示了如何使用 GitHub，其中本教程已完成的示例代码保存在 [Microsoft/python-sample-vs-learning-django](https://github.com/Microsoft/python-sample-vs-learning-django) 存储库中。

1. 选择任一“发布”  控件时，“团队资源管理器”  都将提示你输入详细信息。 例如，在发布本教程中的示例时，必须先创建存储库本身，在这种情况下，" **推送到远程存储库** " 选项与存储库的 URL 一起使用。

    :::image type="content" source="media/django/step01-push-to-github.png" alt-text="用于推送到现有远程存储库的团队资源管理器窗口。":::

    如果没有现有存储库，可通过“发布到 GitHub”  和“推送到 Azure DevOps”  选项直接从 Visual Studio 创建一个存储库。

1. 按照本教程执行操作时，请养成定期在 Visual Studio 中使用控件提交和推送更改的习惯。 本教程会在适当时机提醒你。

> [!Tip]
> 要在团队资源管理器中快速导航，请选择标头（上图中显示为“更改”或“推送”）来查看可用页面的弹出菜单    。

::: moniker-end

### <a name="question-what-are-some-advantages-of-using-source-control-from-the-beginning-of-a-project"></a>问：从项目一开始就使用源代码管理有什么好处？

答：从开始处进行源代码管理，尤其是在使用远程存储库时，会提供项目的定期非现场备份。 与在本地文件系统上维护项目不同的是，源代码管理提供完整的更改历史记录，以及将单个文件或整个项目还原到以前的状态的简单能力。 更改历史记录有助于确定回归 (测试失败) 的原因。 当多个用户正在处理一个项目时，源控件管理覆盖并提供冲突解决。

最后一种是源代码管理，它是一种自动化的形式，可让你自动执行生成、测试和发布管理。 这是使用项目 DevOps 的第一步。 从一开始就没有理由使用源代码管理，因为进入的障碍很少。

有关源代码管理的自动化的进一步讨论，请参阅[事实源： DevOps 中存储库的角色](/archive/msdn-magazine/2016/september/mobile-devops-the-source-of-truth-the-role-of-repositories-in-devops)，这篇文章是针对同样适用于 web 应用的移动应用编写的。

### <a name="question-can-i-prevent-visual-studio-from-autocommitting-a-new-project"></a>问：我是否能阻止 Visual Studio autocommitting 新项目？

答：能。 若要禁用自动提交，请跳到 **团队资源管理器** 中的 "**设置**" 页。 选择 " **Git**  >  **全局设置**"，清除 "**默认情况下，合并后提交更改**" 选项，然后选择 "**更新**"。

## <a name="step-1-3-create-the-virtual-environment-and-exclude-it-from-source-control"></a>步骤 1-3：创建虚拟环境并从源代码管理中将其排除

你已为项目配置源代码管理，现在可为项目创建包含必需 Django 包的虚拟环境。 然后，可以使用“团队资源管理器”  从源代码管理中排除环境文件夹。

::: moniker range="<=vs-2019"

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

1. 输入提交消息，选择 " **全部提交** " 按钮，然后将提交推送到远程存储库。

::: moniker-end

::: moniker range="vs-2022"

1. 在 **解决方案资源管理器** 中，右键单击 " **Python 环境** " 节点，然后选择 " **添加环境**"。

    :::image type="content" source="media/django/step-01-add-virtual-environment-command-vs-2022.png" alt-text="解决方案资源管理器中的 &quot;添加虚拟环境&quot; 命令。":::

1. 在 "添加虚拟环境" 对话框中选择 " **创建** " 以接受默认值。 （如果你愿意，可以更改虚拟环境名称，这只会更改其子文件夹的名称，但 `env` 是标准约定。）

    :::image type="content" source="media/django/step-01-add-environment-dialog-visual-studio-2022.png" alt-text="&quot;添加虚拟环境&quot; 对话框 requirements.txt 消息。":::

1. 如果系统提示，同意管理员权限，请等待几分钟，Visual Studio 下载和安装包。 在此期间，上千个文件传输到多个子文件夹。 可以在 "Visual Studio **输出**" 窗口中查看进度。 在等待时，仔细考虑下面的“问题”部分。

1. 在 Visual Studio Git 控件（位于状态栏上）上，选择更改指示器（显示“99&#42;”），这将打开团队资源管理器中的“更改”页    。

    创建虚拟环境的过程包含数千个更改，但不需要在源代码管理中包含它们中的任何一个，因为您 (或任何其他人克隆该项目) 始终可以从 *requirements.txt* 重新创建该环境。

1. 要排除虚拟环境，请右键单击 env 文件夹，然后选择“忽略这些本地项”   。

    :::image type="content" source="media/django/step-01-ignore-local-items-vs-2022.png" alt-text="忽略源代码管理中的虚拟环境更改。":::

1. 排除虚拟环境后，只剩下的更改是项目文件和 *.gitignore* 文件。 .gitignore 文件包含虚拟环境文件夹的附加条目  。 可以双击文件查看差异。

1. 输入提交消息，选择 " **全部提交** " 按钮，然后将提交推送到远程存储库。

::: moniker-end

### <a name="question-why-do-i-want-to-create-a-virtual-environment"></a>问：为什么需要创建虚拟环境？

答：虚拟环境是隔离应用确切依赖项的好办法。 此类隔离避免了全局 Python 环境中的冲突，有助于进行测试和协作。 随着时间的推移，在开发应用时，总是会引入许多有用的 Python 包。 通过在特定于项目的虚拟环境中保留包，可以轻松地更新项目的 *requirements.txt* 文件。 *requirements.txt* 文件描述了在源代码管理中包含的环境。 如果项目被复制到任何其他计算机（包括生成服务器、部署服务器和其他开发计算机），仅使用 requirements.txt 即可轻松重新创建环境（这就是为什么环境不需要包含在源代码管理中）  。 有关详细信息，请参阅[使用虚拟环境](selecting-a-python-environment-for-a-project.md#use-virtual-environments)。

### <a name="question-how-do-i-remove-a-virtual-environment-thats-already-committed-to-source-control"></a>问：如何删除已经提交给源代码管理的虚拟环境？

答：首先，编辑 *.gitignore* 文件以排除该文件夹。 找到注释 `# Python Tools for Visual Studio (PTVS)` 末尾的部分，并为虚拟环境文件夹添加新行，例如 `/BasicProject/env` 。  (Visual Studio 在 **解决方案资源管理器** 中不显示文件。 若要直接打开文件，请打开 "**文件**  >  " "**打开**  >  **文件**"。 你还可以从 **团队资源管理器** 中打开该文件。 请在 **设置**"页上，选择"**存储库 "设置**。 现在，导航到 "**忽略 & 属性文件**" 部分，然后选择 " **.gitignore**" 旁边的 "**编辑**" 链接。 ) 

然后，打开命令窗口，导航到文件夹，如 *BasicProject*。 *BasicProject* 文件夹包含虚拟环境文件夹（如 *env*），并运行 `git rm -r env` 。 然后从命令行 (`git commit -m 'Remove venv'`) 提交这些更改，或从“团队资源管理器”的“更改”页进行提交。

## <a name="step-1-4-examine-the-boilerplate-code"></a>步骤 1-4：检查样本代码

项目创建完成后，检查样本 Django 项目代码（仍与 CLI 命令 `django-admin startproject <project_name>` 生成的代码相同）。

1. 你的项目的根具有 *manage.py*、Django 命令行管理实用工具，该实用工具 Visual Studio 自动设置为项目启动文件。 可以使用 `python manage.py <command> [options]` 在命令行上运行实用工具。 对于常见的 Django 任务，Visual Studio 提供了方便的菜单命令。 右键单击“解决方案资源管理器”中的项目，然后选择“Python”查看列表。 在本教程的过程中，你将会遇到其中一些命令。

    :::image type="content" source="media/django/step01-django-commands-menu.png" alt-text="Python 项目上下文菜单上的 Django 命令。":::

1. 在您的项目中，有一个与项目同名的文件夹。 它包含基本 Django 项目文件：

   - *__init.py*：一个空文件，告知 Python 此文件夹是 Python 包。
   - *settings.py*：包含 Django 项目的设置，你将在开发 Web 应用的过程中对其进行修改。
   - *urls.py*：包含 Django 项目的目录，你还将在开发过程中对其进行修改。
   - *wsgi.py*：WSGI 兼容的 Web 服务器为项目提供服务的起点。 通常将此文件保留为""，因为它为生产 Web 服务器提供挂钩。

    :::image type="content" source="media/django/step01-django-project-in-solution-explorer.png" alt-text="解决方案资源管理器 中的 Django 项目解决方案资源管理器。":::

1. 如前文所述，Visual Studio 模板还将 requirements.txt 文件添加到指定 Django 包依赖项的项目中。 该文件旨在邀请你在第一次创建项目时创建虚拟环境。

### <a name="question-can-visual-studio-generate-a-requirementstxt-file-from-a-virtual-environment-after-i-install-other-packages"></a>问：在我安装其他包后，Visual Studio 能否从虚拟环境生成 requirements.txt 文件？

答：能。 展开“Python 环境”  节点，右键单击虚拟环境，并选择“生成 requirements.txt”  命令。 在修改环境，并将对 requirements.txt 所做的更改连同依赖于该环境的任何其他代码更改提交给源代码管理时，建议定期使用此命令  。 如果在生成服务器上设置持续集成，应该在修改环境时生成文件并提交更改。

## <a name="step-1-5-run-the-empty-django-project"></a>步骤 1-5：运行空 Django 项目

1. 在Visual Studio > 中，选择"调试""开始 **调试" (** **F5**) 或使用工具栏上的"**Web 服务器**"按钮 (显示的浏览器可能会) ：

    :::image type="content" source="media/django/run-web-server-toolbar-button.png" alt-text="运行 web 服务器工具栏按钮Visual Studio。":::

1. 运行服务器意味着运行命令 `manage.py runserver <port>`，该命令启动 Django 的内置开发服务器。 如果 Visual Studio 显示“启动调试器失败”并显示无启动文件的相关消息，右键单击解决方案资源管理器中的 manage.py 并选择“设为启动文件”。

1. 启动服务器时，会看到一个控制台窗口打开，该窗口还显示服务器日志。 Visual Studio 将自动打开浏览器并转到 `http://localhost:<port>`。 由于 Django 项目没有应用，Django 只显示一个默认页面，用于确认到目前为止你拥有的内容是否正常工作。

    :::image type="content" source="media/django/step01-first-run-success.png" alt-text="Django 项目默认视图。":::

1. 完成后，通过关闭控制台窗口，或使用 Visual Studio 中的“调试”   > “停止调试”  命令来停止服务器。

### <a name="question-is-django-a-web-server-and-a-framework"></a>问：Django 是 Web 服务器和框架吗？

答：是/否。 Django 具有用于开发目的的内置 Web 服务器。 在本地运行 Web 应用时（例如，在客户端中调试时）Visual Studio。 但是在部署到 Web 主机时，Django 会改用主机的 Web 服务器。 Django 项目中的 wsgi.py 模块负责挂接到生产服务器。

### <a name="question-whats-the-difference-between-using-the-debug-menu-commands-and-the-server-commands-on-the-projects-python-submenu"></a>问：在项目 Python 子菜单中使用“调试”菜单命令和服务器命令有何区别？

答：除了“调试”  菜单命令和工具栏按钮之外，还可以使用项目上下文菜单上的“Python”   > “运行服务器”  或“Python”   > “运行调试服务器”  命令来启动服务器。 这两个命令都打开控制台窗口，你将在控制台窗口中看到 (服务器的 localhost：port) 本地 URL。 但是，必须使用该 URL 手动打开浏览器，并且运行调试服务器不会自动启动Visual Studio器。 如果需要，可以使用 **DebugAttach**  >  to Process 命令将调试器附加到正在运行的进程。

## <a name="next-steps"></a>后续步骤

此时，基本 Django 项目不包含任何应用。 你将在下一步创建应用。 由于 Django 应用比 Django 项目更适用于 Django 应用，因此目前无需了解有关样板文件的信息。

> [!div class="nextstepaction"]
> [使用视图和页面模板创建 Django 应用](learn-django-in-visual-studio-step-02-create-an-app.md)

## <a name="go-deeper"></a>深入了解

- Django 项目代码：[编写你的第一个 Django 应用，第 1 部分](https://docs.djangoproject.com/en/2.0/intro/tutorial01/) (docs.djangoproject.com)
- 管理实用工具：[django-admin 和 manage.py](https://docs.djangoproject.com/en/2.0/ref/django-admin/) (docs.djangoproject.com)
- GitHub 上的教程源代码：[Microsoft/python-sample-vs-learning-django](https://github.com/Microsoft/python-sample-vs-learning-django)
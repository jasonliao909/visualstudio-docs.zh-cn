---
title: Visual Studio 中的 Python 教程步骤 6，使用 Git
titleSuffix: ''
description: 在 Visual Studio 中使用 Python 的核心教程的第 6 步，介绍了 Visual Studio 的 Git 相关功能。
ms.date: 02/28/2022
ms.custom: devdivchpfy22
ms.topic: tutorial
author: rjmolyneaux
ms.author: rmolyneaux
manager: jmartens
ms.technology: vs-python
ms.workload:
- python
- data-science
ms.openlocfilehash: 4b0eecc2e81e968d3b719dab325de5671b554c3e
ms.sourcegitcommit: 00af065ac27d41339b31d96a630705509b70b6fa
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2022
ms.locfileid: "140764240"
---
# <a name="step-6-work-with-git"></a>步骤 6：使用 Git

上一步：[安装程序包和管理 Python 环境](tutorial-working-with-python-in-visual-studio-step-05-installing-packages.md)

[!INCLUDE[..get-started/includes/git-source-control.md](../get-started/includes/git-source-control.md)]

::: moniker range="vs-2017"

Visual Studio提供与本地 Git 存储库和远程存储库的直接集成。 它可帮助你使用 GitHub 和 Azure Repos 等服务。 集成包括克隆存储库、提交更改和管理分支。

本文简要概述了如何创建现有项目的本地 Git 存储库，并介绍 Visual Studio 的一些 Git 相关功能。

1. 在 Visual Studio 中打开项目后，比如[上一步](tutorial-working-with-python-in-visual-studio-step-05-installing-packages.md)中的项目，右键单击解决方案并选择“将解决方案添加到源代码管理”。 Visual Studio 将创建包含项目代码的本地 Git 存储库。

1. 当Visual Studio Git 存储库中管理项目时，将显示与 Git 相关的控件。 与 Git 相关的控件显示在"git"窗口右下角Visual Studio显示。 控件显示挂起的提交、更改、存储库名称和分支。 将鼠标悬停在控件上可查看附加信息。

    ![将鼠标悬停在 Visual Studio 窗口中的 Git 控件上时显示附加信息](media/working-with-git-01.png)

1. 新建一个存储库或选择任意 Git 控件时，Visual Studio 会打开“团队资源管理器”窗口。 （你可以使用“查看” > “团队资源管理器”菜单命令随时打开窗口。）窗口中有三个主窗格，你可以使用“团队资源管理器”标题上的下拉菜单进行切换。 在选择“推送”控件（向上箭头图标）时，还显示可用于发布内容的“同步”窗格：

    ![创建本地存储库后 Visual Studio 中的团队资源管理器](media/working-with-git-02.png)

1. 选择“更改”（或带铅笔图标的 Git 控件），以查看未提交的更改并在必要时进行提交。

    ![Visual Studio 中显示未提交更改的团队资源管理器](media/working-with-git-03.png)

    双击“更改”列表中的文件打开该文件的差异视图：

    ![文件更改的差异视图](media/working-with-git-05.png)

1. 选择“分支”（或带分支名称的 Git 控件），以检查分支并执行合并和变基操作：

    ![Visual Studio 中显示分支的团队资源管理器](media/working-with-git-04.png)

1. 若要切换到另一个存储库，请在上一个映像) 中选择存储库名称为 (**CosineWave** 的 Git 控件，然后在 **团队资源管理器** 中，使用 连接 接口。

1. 使用本地存储库时，已提交更改将直接进入存储库。 如果已连接到远程存储库，请选择 团队资源管理器 中的下拉 **标头，选择"同步"** 以切换到"同步"部分，然后使用显示在那里的"拉取"和"**提取"** 命令。

## <a name="go-deeper"></a>深入了解

有关基于远程 Git 存储库创建项目的简短演练，请参阅[快速入门：在 Visual Studio 中克隆 Python 代码存储库](quickstart-03-python-in-visual-studio-project-from-repository.md)。

有关更全面的教程（包括处理合并冲突、使用拉取请求查看代码、变基和挑拣分支之间的更改），请参阅[开始使用 Git 和 Azure Repos](/azure/devops/repos/git/gitquickstart)。

::: moniker-end

## <a name="tutorial-review"></a>教程回顾

恭喜你完成有关 Visual Studio 中 Python 的这一教程。 在本教程中，已了解如何：

- 创建项目和查看项目内容。
- 使用代码编辑器和运行项目。
- 使用交互窗口开发新代码，并将该代码轻松复制到编辑器中。
- 在 Visual Studio 调试器中运行已完成的程序。
- 安装程序包和管理 Python 环境。
- 使用 Git 存储库中的代码。

在此处了解概念和操作说明指南，其中包括下文：

- [创建适用于 Python 的 C++ 扩展](working-with-c-cpp-python-in-visual-studio.md)
- [分析](profiling-python-code-in-visual-studio.md)
- [单元测试](unit-testing-python-in-visual-studio.md)

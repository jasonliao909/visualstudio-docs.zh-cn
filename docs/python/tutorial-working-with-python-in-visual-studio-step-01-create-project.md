---
title: Visual Studio 中的 Python 教程步骤 1，创建项目
titleSuffix: ''
description: 在 Visual Studio 中使用 Python 功能的核心教程概述和第 1 步，包括系统必备组件和创建新的 Python 项目。
ms.date: 09/14/2021
ms.topic: tutorial
author: rjmolyneaux
ms.author: rmolyneaux
manager: jmartens
ms.technology: vs-python
ms.custom: vs-acquisition
ms.workload:
- python
- data-science
ms.openlocfilehash: 2f26f10754de6addcab2815eecfffa394296e6bc
ms.sourcegitcommit: 8fae163333e22a673fd119e1d2da8a1ebfe0e51a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2021
ms.locfileid: "129967608"
---
# <a name="tutorial-work-with-python-in-visual-studio"></a>教程：在 Visual Studio 中使用 Python

Python 是一种流行的编程语言，它可靠、灵活、易于学习、可在所有操作系统上免费使用。 强大的开发人员社区和很多免费库都支持 Python。 该语言支持各种开发，包括 Web 应用程序、Web 服务、桌面应用、脚本编写和科学计算。 许多高校人员、科学家、业余开发人员和专业开发人员都在使用 Python。

Visual Studio 为 Python 提供一级语言支持。 本教程将指导你完成以下步骤：

- [步骤 0：安装](tutorial-working-with-python-in-visual-studio-step-00-installation.md)
- [步骤 1：创建 Python 项目（本文）](#step-1-create-a-new-python-project)
- [步骤 2：编写和运行代码，以便在工作时查看 Visual Studio IntelliSense](tutorial-working-with-python-in-visual-studio-step-02-writing-code.md)
- [步骤 3：在 REPL 交互窗口中创建更多代码](tutorial-working-with-python-in-visual-studio-step-03-interactive-repl.md)
- [步骤 4：在 Visual Studio 调试器中运行已完成的程序](tutorial-working-with-python-in-visual-studio-step-04-debugging.md)
- [步骤 5：安装程序包和管理 Python 环境](tutorial-working-with-python-in-visual-studio-step-05-installing-packages.md)
- [步骤 6：使用 Git](tutorial-working-with-python-in-visual-studio-step-06-working-with-git.md)

[!INCLUDE[tutorial-prereqs](includes/tutorial-prereqs.md)]

## <a name="step-1-create-a-new-python-project"></a>步骤 1：创建新的 Python 项目

项目是 Visual Studio 管理所有文件的一种方式，这些文件结合在一起可生成单个应用程序。 应用程序文件包括源代码、资源和配置。 项目将其所有文件之间的关系形式化并予以维护。 项目还可以管理在多个项目之间共享的外部资源。 项目使得应用程序能够毫不费力地扩展和增长。 使用项目比在临时文件夹、脚本、文本文件和内存中手动管理关系要容易得多。

本教程将从一个包含单一空代码文件的简单项目开始。

::: moniker range="<=vs-2019"
1. 在 Visual Studio 中，选择“文件” > “新建” > “项目”(Ctrl+Shift+N)，这会打开“新建项目”对话框。 可在该对话框中浏览各种语言的模板，然后为项目选择一个模板，并指定 Visual Studio 放置文件的位置。

1. 若要查看 Python 模板，可在左侧选择“已安装” > “Python”或搜索“Python”。 如果忘记了模板在语言树中的位置，使用搜索是找到该模板的好方法。

    ![显示包含 Python 项目模板的“创建新项目”对话框的屏幕截图。](media/vs-getting-started-python-01-new-project.png)

    Visual Studio 中的 Python 支持包含多个项目模板，其中包括使用 Bottle、Flask 和 Django 框架的 Web 应用程序。 但为了便于演示，我们以空项目开始。

1. 选择“Python 应用程序”模板，为项目指定名称并选择“确定”。

1. 几分钟后，Visual Studio 会在“解决方案资源管理器”窗口 (1) 中显示项目结构。 默认代码文件在编辑器 (2) 中处于打开状态。 “属性”窗口 (3) 也会出现，其中显示在“解决方案资源管理器”中选定的任何项的附加信息（包括它在磁盘上的确切位置）。

    ![显示 Visual Studio 中打开的新项目的屏幕截图。](media/vs-getting-started-python-02-windows.png)

1. 花点时间熟悉一下“解决方案资源管理器”，可在该管理器中浏览项目中的文件和文件夹。

    ![解决方案资源管理器（已展开以显示功能）的屏幕截图。](media/vs-getting-started-python-03-solution-explorer.png)

    (1) 粗体突出显示的是项目，其名称是在“新建项目”对话框中指定的名称。 在磁盘上，此项目由项目文件夹中的 .pyproj 文件表示。

    (2) 顶层是一个 *解决方案*，它与项目默认同名。 解决方案在磁盘上由 .sln 文件表示，是一个或多个相关项目的容器  。 例如，如果你为 Python 应用程序编写 C++ 扩展，则该 C++ 项目可以位于同一解决方案中。 解决方案还可以包含 Web 服务的项目，以及专用测试程序的项目。

    (3) 在项目下方可以看到源文件，在本例中，只有一个 .py 文件。 选择文件时会在“属性”窗口中显示其属性。 双击文件会以任何适合该文件的方式打开该文件。

    (4) 项目下方还有“Python 环境”节点。 展开后，可以看到可用的 Python 解释器。 展开解释器节点可查看安装到该环境 (5) 中的库。

    右键单击“解决方案资源管理器”中的任意节点或项均可访问适用命令菜单。 例如，“重命名”命令可用于更改任何节点或项（包括项目和解决方案）的名称。

::: moniker-end

::: moniker range=">=vs-2022"
1. 在 Visual Studio 中，选择“文件” > “新建” > “项目”，或按 Ctrl+Shift+N     。 此时会显示“创建新项目”屏幕，可在其中搜索和浏览不同语言的模板。
   
1. 若要查看 Python 模板，请搜索“python”。 如果忘记了模板在语言树中的位置，使用搜索是找到该模板的好方法。
   
   ![显示包含 Python 项目模板的“创建新项目”对话框的屏幕截图。](media/vs-2022/getting-started-python-new-project.png)
   
   Visual Studio 中的 Python 支持包含多个项目模板，例如 Bottle、Flask 和 Django 框架中的 Web 应用程序。 对于本教程，请从一个空项目开始。
   
1. 选择“PythonConsoleApp”模板，然后选择“下一步” 。
   
1. 在“配置新项目”屏幕上，指定项目的名称和文件位置，然后选择“创建” 。
   
   新项目将在 Visual Studio 中打开。
   
   - Visual Studio 的“解决方案资源管理器”窗口将显示项目结构 (1) 。
   - 默认代码文件将在编辑器中打开 (2)。
   - “属性”窗口将显示在“解决方案资源管理器”中选择的项的其他信息，包括它在磁盘上的确切位置 (3)  。
   
   ![显示 Visual Studio 中打开的新项目的屏幕截图。](media/vs-2022/getting-started-python-windows.png)
   
1. 请熟悉一下“解决方案资源管理器”，在其中可以浏览项目中的文件和文件夹。
   
   ![解决方案资源管理器（已展开以显示功能）的屏幕截图。](media/vs-2022/getting-started-python-solution-explorer.png)
   
   - 顶层是解决方案，默认情况下它与项目同名 (1)。
     
     在磁盘上以 .sln 文件形式显示的解决方案是一个或多个相关项目的容器。 例如，如果你为 Python 应用程序编写 C++ 扩展，则该 C++ 项目可以位于同一解决方案中。 解决方案还可以包含 Web 服务的项目，以及专用测试程序的项目。
   
   - 使用你在“创建新项目”对话框中指定的名称的项目以粗体显示 (2) 。 在磁盘上，项目是项目文件夹中的一个 .pyproj 文件。
   
   - 项目下方是源文件，在本例中只有一个 .py 文件 (3)。 选择文件时会在“属性”窗口中显示其属性。 双击文件会以任何适合该文件的方式打开该文件。
   
   - 项目下方还有“Python 环境”节点 (4) 。 展开该节点可显示可用的 Python 解释器。
   
   - 展开解释器节点可查看安装在该环境中的库 (5)。
   
   右键单击“解决方案资源管理器”中的任意节点或项可显示适用命令的上下文菜单。 例如，“重命名”可用于更改节点或项（包括项目和解决方案）的名称。
::: moniker-end

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [编写并运行代码](tutorial-working-with-python-in-visual-studio-step-02-writing-code.md)

## <a name="go-deeper"></a>深入了解

- [Visual Studio 中的 Python 项目](managing-python-projects-in-visual-studio.md)。
- [在 python.org 上了解 Python 语言](https://www.python.org)
- [Python for Beginners](https://www.python.org/about/gettingstarted/)（面向初学者的 Python，python.org）

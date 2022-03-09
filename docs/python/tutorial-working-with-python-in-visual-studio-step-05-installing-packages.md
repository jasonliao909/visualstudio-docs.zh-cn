---
title: Visual Studio 中的 Python 教程步骤 5，安装包
titleSuffix: ''
description: Visual Studio 中的 Python 功能的核心演练步骤5。 演示 Visual Studio 功能，说明如何在 Python 环境中管理和安装包。
ms.date: 02/28/2022
ms.topic: tutorial
author: rjmolyneaux
ms.author: rmolyneaux
manager: jmartens
ms.technology: vs-python
ms.workload:
- python
- data-science
ms.custom: devdivchpfy22
ms.openlocfilehash: c262b91b32a4e67c7b7198093ee2fa6bb72e2a3c
ms.sourcegitcommit: edf8137cd90c67b6078a02c93094f7e1c3bf8930
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2022
ms.locfileid: "139551966"
---
# <a name="step-5-install-packages-in-your-python-environment"></a>步骤 5：在 Python 环境中安装程序包

**上一步：[在调试器中运行代码](tutorial-working-with-python-in-visual-studio-step-04-debugging.md)**

Python 开发者社区制作了数千个有用的程序包，用户可以将它们合并到自己的项目中。 Visual Studio 提供一个 UI，用于管理 Python 环境中的程序包。

## <a name="view-environments"></a>查看环境

1. 选择“视图” > “其他窗口” > “Python 环境”菜单命令    。 “Python 环境”  窗口作为“解决方案资源管理器”  的同级打开，并向用户显示各种可用的环境。 此列表显示了使用 Visual Studio 安装程序安装的两个环境以及您单独安装的环境。 其中包括全局环境、虚拟环境和 conda 环境。 粗体显示的环境是用于新项目的默认环境。 有关使用环境的详细信息，请参阅[如何在 Visual Studio 环境中创建和管理 Python 环境](managing-python-environments-in-visual-studio.md)。

   :::moniker range=">=vs-2022"
   !["Python 环境" 窗口-2022](media/environments/environments-default-view-2022.png)
   :::moniker-end

   :::moniker range="<=vs-2019"
   !["Python 环境" 窗口-2019](media/environments/environments-default-view-2019.png)
   :::moniker-end

   > [!NOTE]
   > 你还可以使用 **ctrl + K、ctrl + "** 键盘快捷方式从" 解决方案资源管理器 "窗口打开" **Python 环境** "窗口。 如果快捷方式不起作用，并且在菜单中找不到 "Python 环境" 窗口，则可能尚未安装 Python 工作负载。 有关如何安装 python 的指南，请参阅[如何在 Visual Studio Windows 上安装 python 支持](installing-python-support-in-visual-studio.md#how-to-install-python-support-in-visual-studio-on-windows)。

   打开 Python 项目后，可以从 **解决方案资源管理器** 打开 " **python 环境**" 窗口。 右键单击 " **Python 环境** "，然后选择 " **查看所有 Python 环境**"。

   :::moniker range="vs-2022"
   ![Python 环境-2022](media/environments/environments-view-all-2022.png)
   :::moniker-end

   :::moniker range="<=vs-2019"
   ![Python 环境-2019](media/environments/environments-view-all-2019.png)
   :::moniker-end

1. 现在，通过选择“文件” > “新建” > “项目”来创建新项目，然后选择“Python 应用程序”模板     。

1. 在随即出现的代码文件中，粘贴以下代码来创建像之前的教程步骤一样的余弦波，只不过这次以图形方式绘制。 你还可以使用之前创建的项目并替换代码。

    ```python
    from math import radians
    import numpy as np # installed with matplotlib
    import matplotlib.pyplot as plt

    def main():
        x = np.arange(0, radians(1800), radians(12))
        plt.plot(x, np.cos(x), 'b')
        plt.show()

    main()
    ```

1. 在编辑器窗口中，将 `numpy` 鼠标悬停在和 `matplotlib` import 语句上。 你会注意到它们未解析。 若要解析 import 语句，请将包安装到默认全局环境中。
   :::moniker range=">=vs-2022"
   ![包导入未解析-2022](media/packages-unresolved-import-2022.png)
   :::moniker-end

   :::moniker range="<=vs-2019"
    ![未解析的包导入](media/packages-unresolved-import.png)
   :::moniker-end

1. 当您查看编辑器窗口时，请注意，当您将鼠标悬停在未解析的 `numpy` 和 `matplotlib` import 语句上时。 原因是尚未将包安装到默认全局环境中。

    例如，选择 "**打开交互窗口**"，将在 Visual Studio 中显示特定环境的 **交互窗口**。

1. "Python 环境" 窗口中的 " **包** " 选项卡列出了环境中当前安装的所有包。

## <a name="install-packages-using-the-python-environments-window"></a>使用“Python 环境”窗口安装包

1. 从 "Python 环境" 窗口中，选择新的 Python 项目的默认环境，然后选择 " **包** " 选项卡。然后，你将看到该环境中当前安装的包的列表。

   :::moniker range=">=vs-2022"
   [在环境中安装包](media/environments/install-python-packages-2022.gif)
   :::moniker-end

1. 在搜索字段输入 `matplotlib` 的名称，再选择“运行命令: pip install matplotlib”选项来安装此项目  。 运行该命令将安装 `matplotlib` ，并且它依赖的任何包都 (在此情况下包括 `numpy`) 。

1. 选择 " **包** " 选项卡。

1. 如果系统提示同意提升，请同意。

1. 安装程序包后，它会显示在“Python 环境”  窗口中。 单击程序包右侧的 **X** 可卸载它。

1. 在搜索字段中输入 `matplotlib` 安装 `matplotlib` 。

1. 选择 " **运行命令： pip install matplotlib** " 选项。
      此选项将安装 `matplotlib` ，并且它依赖的任何包都 (在这种情况下，包括 `numpy`) 。

   :::moniker range="vs-2022"
    ![在环境中安装 matplotlib-2022 in 包选项卡](media/environments/environments-add-matplotlib-2022.png)
   :::moniker-end
   :::moniker range="<=vs-2019"
   ![在环境中安装 matplotlib-2019 in 包选项卡](media/environments/environments-add-matplotlib-2019.png)
   :::moniker-end

1. 如果系统提示同意提升，请同意。

1. 安装程序包后，它将显示在 " **Python 环境** " 窗口中。 单击程序包右侧的 **X** 可卸载它。

   :::moniker range="vs-2022"
   ![在环境中安装 matplotlib-2022](media/environments/environments-add-matplotlib2-2022.png)
   :::moniker-end

   :::moniker range="<=vs-2019"
   ![在环境中安装 matplotlib-2019](media/environments/environments-add-matplotlib2-2019.png)
   :::moniker-end

    > [!NOTE]
   > 环境下方可能会出现一个小进度栏，指示 Visual Studio 正在为新安装的程序包生成 IntelliSense 数据库。 “IntelliSense”  选项卡也显示了更多详细信息。 请注意，完成该数据库之前，编辑器中的自动完成和语法检查等 IntelliSense 功能针对该程序包处于非活动状态。

   > Visual Studio 2017 15.6 及更高版本采用不同且更快的方法来使用 IntelliSense，并在“IntelliSense”选项卡上显示一条简要介绍此内容的消息  。

## <a name="run-the-program"></a>运行程序

现已安装 [matplotlib](https://matplotlib.org/)，请按 (F5) 运行项目来查看输出；如果没有调试器，则使用 (Ctrl+F5)    ：

   ![matplotlib 示例的输出](media/environments/environments-add-matplotlib3.png)

## <a name="next-step"></a>下一步

> [!div class="nextstepaction"]
> [使用 Git](tutorial-working-with-python-in-visual-studio-step-06-working-with-git.md)

## <a name="go-deeper"></a>深入了解

- [Python 环境](managing-python-environments-in-visual-studio.md)
- [了解 Visual Studio 中的 Django](learn-django-in-visual-studio-step-01-project-and-solution.md)
- [了解 Visual Studio 中的 Flask](learn-flask-visual-studio-step-01-project-solution.md)

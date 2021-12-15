---
title: 快速入门 - 克隆 Python 代码存储库
description: 在此快速入门教程中，将使用 Visual Studio 团队资源管理器进行 Python koans 存储库克隆，从而在 Visual Studio 中创建 Python 项目。
ms.date: 12/11/2021
ms.custom: devdivchpfy22
ms.topic: quickstart
author: rjmolyneaux
ms.author: rmolyneaux
manager: jmartens
ms.technology: vs-python
ms.workload:
- python
- data-science
ms.openlocfilehash: a8c754b7366236db86e8d0dd7ff9e5dabb94507e
ms.sourcegitcommit: 04fb8ba0f7ea73ba17baa88f10563c8600e7fd7b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/15/2021
ms.locfileid: "135121549"
---
# <a name="quickstart-clone-a-repository-of-python-code-in-visual-studio"></a>快速入门：在 Visual Studio 中克隆 Python 代码存储库

[在 Visual Studio 中安装 Python 支持](installing-python-support-in-visual-studio.md)后，可以添加适用于 Visual Studio 的 GitHub 扩展。 利用此扩展可轻松克隆 Python 代码的存储库，并在 IDE 中通过该存储库创建一个项目。 此外，始终可在命令行上克隆存储库，然后在 Visual Studio 中使用。

## <a name="install-the-github-extension-for-visual-studio"></a>安装 Visual Studio 的 GitHub扩展

[!INCLUDE[install-github-extension](includes/install-github-extension.md)]

## <a name="work-with-github-in-visual-studio"></a>在 Visual Studio 中使用 GitHub

1. 启动 Visual Studio。

1. 选择“视图” > “团队资源管理器”，打开“团队资源管理器”窗口，可在该窗口中连接到 GitHub 或 Azure Repos，或者克隆存储库  。 （如果下方未显示“连接”页，请选择顶部工具栏的“插入”图标，跳转到该页面。）

    ![显示 Azure Repos、GitHub 并克隆存储库的“团队资源管理器”窗口](media/team-explorer.png)

1. 在本地 **Git 存储库下，** 选择" **克隆"** 命令，然后在 `https://github.com/gregmalcolm/python_koans` URL 字段中输入 。

1. 输入克隆文件的文件夹，然后选择"克隆 **"** 按钮。

    > [!Tip]
    > 在团队资源管理器中指定的文件夹就是用于接收克隆文件的文件夹。 与 `git clone` 命令不同，在团队资源管理器中创建克隆时不会使用存储库名称自动创建一个子文件夹。

1. 克隆完成后，“本地 Git 存储库”列表中会显示存储库名称。 双击该名称导航到“团队资源管理器”中的存储库仪表板。

1. 在“解决方案”下面，选择“新建”。

    ![“团队资源管理器”窗口, 从克隆创建新项目](media/team-explorer-new-project.png)

1. 在出现的 **"Project"** 对话框中，导航到 **Python** 语言 (或搜索"Python") ，选择"从 **现有 Python 代码"。** 

1. 指定项目的名称，将 **"位置**"设置为与存储库相同的文件夹，然后选择"确定 **"。**

1. 在随即出现的向导中选择“完成”。

1. 从菜单中选择“视图” > “解决方案资源管理器”。

1. 在 **解决方案资源管理器** 中，展开 **python3** 节点，右键单击 **"contemplate_koans.py"。**

1. 选择 **"设置为启动文件"。**
此步骤指示 Visual Studio 在运行项目时应使用哪个文件。

1. 从菜单中依次选择“项目” > “Koans 属性”，再选择“常规”选项卡并将“工作目录”设置为“python3”。 此步骤是必需的，因为默认情况下Visual Studio将工作目录设置为项目根目录。 Visual Studio不会在 *python3\contemplate_koans.py* 中设置启动文件的位置，项目属性中也可以看到该位置。 程序代码会在工作文件夹中查找文件 koans.txt，因此不更改此值会导致运行时错误。

    ![设置 Python 项目的工作目录](media/projects-set-working-directory.png)

1. 按 Ctrl  +F5  或选择“调试”   > “开始执行(不调试)”  运行程序。 如果看到 koans.txt 的 FileNotFoundError，则检查上一步中的工作目录设置。

1. 程序成功运行时，会在 python3/koans/about_asserts.py 的第 17 行显示一个断言错误。 这是有意为之：程序旨在通过让用户更正所有故意设计的错误来学习 Python。 （[Ruby Koans](https://rubykoans.com/) 上提供了更多详细信息，Python Koans 的设计灵感便源于前者。）

    ![Python koans 程序的第一次输出](media/koans-output.png)

1. 通过在解决方案资源管理器中导航到 python3/koans/about_asserts.py 并双击，打开该文件。 默认情况下，行号不会出现在编辑器中。 若要更改此设置，请选择“工具” > “选项”，选择对话框底部的“显示所有设置”，然后导航到“文本编辑器” > “Python” > “常规”并选择“行号”：

    ![为 Python 文件启用行号](media/options-general-line-numbers.png)

1. 通过将第 17 行的 `False` 参数更改为 `True` 来更正错误。 该行应如下所示：

    ```python
    self.assertTrue(True) # This should be True
    ```

1. 再次运行程序。 如果 Visual Studio 发出错误警告，请回复“是”以继续运行代码。 你将看到程序通过第一次检查，然后在下一个 koan 上停止。 继续更正错误，并再次运行程序。

> [!Important]
> 在此快速入门教程中，创建了对 GitHub 上 python_koans 存储库的直接克隆。 此类存储库的作者会对其设置保护，不允许直接更改，因此尝试将更改提交到存储库会失败。 在实际操作中，开发人员会将此类存储库复制到自己的 GitHub 帐户，在那里进行更改后，再创建拉取请求将这些更改提交到原始存储库。 如果有自己的副本，请使用其 URL 而不是先前使用的原始存储库 URL。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [教程：在 Visual Studio 中使用 Python](tutorial-working-with-python-in-visual-studio-step-01-create-project.md)

## <a name="see-also"></a>另请参阅

- [手动标识现有的 Python 解释器](managing-python-environments-in-visual-studio.md#manually-identify-an-existing-environment) 
[在 Windows 上的](installing-python-support-in-visual-studio.md#how-to-install-python-support-in-visual-studio-on-windows)Visual Studio 安装 Python 支持
- [Python 工具安装目录](installing-python-support-in-visual-studio.md#install-locations)

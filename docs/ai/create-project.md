---
title: 根据模板创建 AI 项目
description: 了解如何使用 Visual Studio Tools for AI 通过各种模板创建 AI 项目。
ms.custom: SEO-VS-2020
author: jillre
ms.author: jillfra
manager: jmartens
ms.technology: vs-ai-tools
monikerRange: vs-2017
ms.date: 11/13/2017
ms.topic: how-to
ms.workload:
- multiple
ms.openlocfilehash: e1a9cbdd4449282076703134862178f3a866851f
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126641348"
---
# <a name="create-an-ai-project-from-a-template-in-visual-studio"></a>从 Visual Studio 中的模板创建 AI 项目

[安装 Visual Studio Tools for AI](installation.md) 后，即可使用各种模板轻松创建新的 AI 项目。

1. 启动 Visual Studio。

2. 选择“文件”>“新建”>“项目”(Ctrl+Shift+N)。 在“新建项目”对话框中，搜索“AI 工具”，然后选择所需的模板。 请注意，选择模板时会显示有关模板所提供内容的简短说明。

    ![显示 Python 模板的 VS2017“新建项目”对话框](media/create-project/new-ai-project.png)

3. 在本快速入门教程中，选择“TensorFlow 应用程序”模板，为项目指定名称（比如“MNIST”）和位置，然后选择“确定”。

4. Visual Studio 随即创建项目文件（磁盘上的 `.pyproj` 文件）以及模板所述的任何其他文件。 使用“TensorFlow 应用程序”模板时，项目包含一个与项目同名的文件。 默认情况下，该文件在 Visual Studio 编辑器中打开。

    ![使用 Python 应用程序模板时生成的项目](media/create-project/new-tensorflowapp.png)

5. 请注意代码已导入几个库，包括 TensorFlow、numpy、sys 和 os。 此外，它还在启动应用程序时提供一些输入参数，以便轻松切换输入培训数据、输出模型和日志文件的位置。 将作业提交到多个计算上下文（即本地开发框上而非 Azure 文件共享上的目录）时，这些参数非常有用。

6. 项目还创建了一些属性，有助于通过将命令行实参自动传递给这些输入形参，轻松调试应用。 右键单击项目，然后选择“属性”

    ![Visual Studio 解决方案资源管理器的屏幕截图，其中显示已选择“属性”的 TensorFlowApplication1 上下文菜单。](media/create-project/project-properties.png)

7. 单击“调试”选项卡以查看自动添加的脚本参数。 可根据需要将其改为输入数据的位置及存储输出的位置。

    ![TensorFlowApplication1 的“属性”设置中“调试”选项卡的屏幕截图，其中显示了项目的脚本参数。](media/create-project//project-properties_1.png)

8. 按 Ctrl+F5 或选择菜单上的“调试”>“开始执行(不调试)”运行程序。 结果显示在控制台窗口中。

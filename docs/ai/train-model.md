---
title: 提交作业以训练模型
description: 提交作业以使用 Azure Batch AI 训练模型
ms.custom: SEO-VS-2020
keywords: ai, visual studio, 训练模型, 云
author: jillre
ms.author: jillfra
manager: jmartens
ms.technology: vs-ai-tools
monikerRange: vs-2017
ms.date: 11/13/2017
ms.topic: how-to
ms.workload:
- azure
ms.openlocfilehash: e1efd5101ae606588b40a09a0c6ed5e24c171eb8
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122037546"
---
# <a name="train-ai-models-in-azure-batch-ai"></a>在 Azure Batch AI 中训练 AI 模型

Batch AI 是一种托管服务，使数据科学家和 AI 研究人员可以在 Azure 虚拟机（包括具有 GPU 支持的 VM）群集上训练 AI 和其他机器学习模型。 你只需描述作业的要求、用于查找输入和存储输出的位置，Batch AI 会处理其余部分。 [了解有关 Azure Batch AI 的详细信息](/azure/batch-ai/overview)

它与 Visual Studio Tools for AI 集成，以便你可以在 Azure 中动态横向扩展训练模型。  [安装 Visual Studio Tools for AI](installation.md) 之后，可以使用 Azure 机器学习示例库中的预制方案轻松地创建新 Python 项目。

1. 启动 Visual Studio。 通过打开“AI 工具”菜单，然后选择“选择群集”，来打开“服务器资源管理器”  

    ![群集选择器](media/train-model/select-cluster.png)

2. 展开“AI 工具”。 你具有的任何 Batch AI 资源都会自动检测到并出现在服务器资源管理器中。

    ![服务器资源管理器中 AI 工具的扩展文件夹树的屏幕截图，其中显示 Azure Batch AI 和 Azure 机器学习的扩展子文件夹。](media/train-model/batchai.png)

3. 选择“视图”>“团队资源管理器...”，打开“团队资源管理器”窗口，可在该窗口中连接到 GitHub 或 Azure DevOps Services，或者克隆存储库 。

    ![显示 Azure DevOps、GitHub 并克隆存储库的“团队资源管理器”窗口](media/train-model/team-explorer-devops.png)

4. 在“本地 Git 存储库”下的 URL 字段中，输入 `https://github.com/Microsoft/samples-for-ai`，为克隆文件输入一个文件夹，然后选择“克隆” 。

    > [!Tip]
    > 在团队资源管理器中指定的文件夹是用于接收克隆文件的特定文件夹。 与 `git clone` 命令不同，在团队资源管理器中创建克隆时不会使用存储库名称自动创建一个子文件夹。

5. 克隆完成后，单击“文件”>“打开解决方案”>“项目/解决方案”

    ![显示服务器资源管理器文件菜单的一部分的屏幕截图，其中已选中“打开”命令并在上下文菜单上选中了“项目/解决方案”。](media/train-model/open-solution.png)

6. 打开克隆存储库的目录中的 samples-for-ai\TensorFlowExamples\TensorFlowExamples.sln

    ![显示解决方案文件 TensorflowExamples.sln 的屏幕截图，该文件列在 samples-for-ai 存储库中 TensorflowExamples 文件夹的内容中。](media/train-model/tensorflowexamples.png)

7. 将 MNIST 项目设置为“启动项目”

    ![屏幕截图显示在解决方案资源管理器中的 MNIST 项目的上下文菜单中已选择“设置为启动项目”。](media/train-model/mnist-startup.png)

8. 右键单击“MNIST 项目”的“提交作业” 

    ![屏幕截图显示在解决方案资源管理器中的 MNIST 项目的上下文菜单中已选择“提交作业”。](media/train-model/submit-job.png)
9. 选择“Azure Batch AI”群集，然后单击“导入”。 选择 `AzureBatchAI_TF_MNIST.json` 文件以快速填充一些默认值，如要使用的 Docker 映像。 然后单击“提交”

    ![“提交作业”对话框的屏幕截图，其中填充了“使用群集”、“启动脚本”、“作业名称”、“映像名称”、“StdOutErr 路径前缀”和“CLI 参数”的值。](media/train-model/submit-batch.png)

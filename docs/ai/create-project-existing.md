---
title: 通过现有代码创建 AI 项目
description: 了解如何使用 Visual Studio Tools for AI，将现有的 Python 代码引入 Visual Studio 项目。
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
ms.openlocfilehash: 0f3ff4f40a42cfb7f4e3582abdb760af5dfffde9
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122045523"
---
# <a name="create-an-ai-project-from-existing-code"></a>通过现有代码创建 AI 项目

[安装 Visual Studio Tools for AI](installation.md) 后，就可以轻松地将现有 Python 代码引入 Visual Studio 项目。

> [!Important]
> 此处所述的过程不移动或复制原始源文件。 如果要使用副本，请先复制文件夹。

1. 启动 Visual Studio，然后选择“文件”>“新建”>“项目”。

2. 在“新建项目”对话框中，搜索“AI 工具”，选择“从现有的 Python 代码”模板，为项目提供名称和位置，然后选择“确定”。

   ![根据现有代码新建项目，步骤 1](media/create-project-existing/new-ai-project.png)

3. 在出现的向导中，设置现有代码的路径和文件类型筛选器，并指定项目需要的任何搜索路径，然后选择“确定”。 如果不知道搜索路径是什么，则将该字段留空。

   ![根据现有代码新建项目，步骤 2](media/create-project-existing/azurebatch-newproject.png)

   如果现有代码属于 Azure 机器学习项目，请选中“是 Azure 机器学习文件夹”，以确保成功转换重要的 Azure 机器学习配置详细信息，如试验帐户、工作区、要使用的计算上下文等。

4. 若要设置启动文件，请在“解决方案资源管理器”中找到此文件，右键单击它，再选择“设置为启动文件”。

5. 按 Ctrl+F5，或依次选择“调试”>“启动但不调试”，以运行程序。

> [!div class="nextstepaction"]
> [教程：在 Visual Studio 中使用 Python](../python/tutorial-working-with-python-in-visual-studio-step-00-installation.md)

## <a name="see-also"></a>另请参阅

- [手动标识现有的 Python 环境](../python/managing-python-environments-in-visual-studio.md#manually-identify-an-existing-environment)

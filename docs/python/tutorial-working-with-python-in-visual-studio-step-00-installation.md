---
title: Visual Studio 中的 Python 教程步骤 0，安装
titleSuffix: ''
description: 在 Visual Studio 中使用 Python 的核心教程的第 0 步（安装前提条件）。
ms.date: 12/11/2021
ms.custom: devdivchpfy22, vs-acquisition
ms.topic: tutorial
author: rjmolyneaux
ms.author: rmolyneaux
manager: jmartens
ms.technology: vs-python
ms.workload:
- python
- data-science
ms.openlocfilehash: ab21d1939a79b3065dd27449d58ce72e4001005d
ms.sourcegitcommit: 04fb8ba0f7ea73ba17baa88f10563c8600e7fd7b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/15/2021
ms.locfileid: "135121511"
---
# <a name="install-python-support-in-visual-studio"></a>在 Visual Studio 中安装 Python 支持

> [!Note]
> 目前仅在 Visual Studio for Windows 中提供 Python 支持。 在 Mac 和 Linux 上，可通过 [Visual Studio Code](https://code.visualstudio.com/docs/python/python-tutorial) 获取 Python 支持。

1. 下载并运行适用于 Windows 的最新 Visual Studio 安装程序。 版本 15.2 及更高版本提供 Python 支持。 如果已安装 Visual Studio，请通过选择“工具” > “添加工具和功能”来打开 Visual Studio 并运行安装程序。

    > [!div class="nextstepaction"]
    > [安装 Visual Studio Community](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Community&rel=15&rid=34347&utm_source=docs&utm_medium=clickbutton&utm_campaign=python_gettingstarted)

    >[!Tip]
    > Community Edition 适用于个体开发者、课堂学习、学术研究和开放源代码开发。 对于其他用途，请安装 [Visual Studio Professional](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Professional&rel=15&rid=34347&utm_source=docs&utm_medium=clickbutton&utm_campaign=python_gettingstarted) 或 [Visual Studio Enterprise](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Enterprise&rel=15&rid=34347&utm_source=docs&utm_medium=clickbutton&utm_campaign=python_gettingstarted)。

1. 安装程序提供了工作负荷列表，这些工作负荷是特定开发区域的相关选项的组。 对于 Python，请选择 **Python 开发** 工作负载，然后选择“安装”：

    ![Visual Studio 安装程序中选择的 Python 开发工作负载的屏幕截图。](media/installation-python-workload.png)

1. 若要快速测试 Python 支持，请启动 Visual Studio，按 Alt+I 打开 Python 交互窗口，然后输入 `2+2`。 如果看不到输出 4，请重新检查步骤。

    ::: moniker range="<=vs-2019"
    ![通过交互窗口测试 Python 的屏幕截图。](media/installation-interactive-test.png)
    ::: moniker-end

    ::: moniker range=">=vs-2022"
    ![通过 Visual Studio 2022 交互窗口测试 Python 的屏幕截图。](media/vs-2022/python-interactive.png)
    ::: moniker-end

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [步骤 1：创建 Python 项目](tutorial-working-with-python-in-visual-studio-step-01-create-project.md)

## <a name="see-also"></a>另请参阅

- [手动标识现有的 Python 解释器](managing-python-environments-in-visual-studio.md#manually-identify-an-existing-environment)
- [Visual Studio 2022 中安装 Python 支持](installing-python-support-in-visual-studio.md#visual-studio-2022)
- [Visual Studio 2019 中安装 Python 支持](installing-python-support-in-visual-studio.md#visual-studio-2019)
- [Visual Studio 2015 中安装 Python 支持](installing-python-support-in-visual-studio.md#visual-studio-2015)

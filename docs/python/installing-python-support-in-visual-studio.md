---
title: 安装 Python 支持
description: 如何在 Visual Studio 2017、2015、2013、2012 和 2010 中安装针对 Visual Studio 的 Python 工具 (PTVS)，包括选项和安装位置。
ms.date: 03/13/2019
ms.topic: how-to
author: rjmolyneaux
ms.author: rmolyneaux
manager: jmartens
ms.technology: vs-python
ms.workload:
- python
- data-science
ms.openlocfilehash: d8bced39dc9b2aea7678505bd597fd9e1aa6db39
ms.sourcegitcommit: 0f2af2f1a8cf0a481fd8f673accf3aebf2e262c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2021
ms.locfileid: "134714371"
---
# <a name="how-to-install-python-support-in-visual-studio-on-windows"></a>如何在 Windows 上的 Visual Studio 中安装 Python 支持

若要安装针对 Visual Studio 的 Python 支持（亦称为“针对 Visual Studio 的 Python 工具 (PTVS)”），请按照 Visual Studio 版本对应部分中的说明操作：
:::moniker range=">=vs-2022"

-[Visual Studio 2022](#visual-studio-2022)
:::moniker-end
:::moniker range="vs-2019"

- [Visual Studio 2019](#visual-studio-2019)
:::moniker-end
:::moniker range="<=vs-2017"

- [Visual Studio 2017](#visual-studio-2017)
- [Visual Studio 2015](#visual-studio-2015)
- [Visual Studio 2013 及更早版本](#visual-studio-2013-and-earlier)
:::moniker-end

若要在执行安装步骤后快速测试 Python 支持，请按 Alt+I 并输入 `2+2` 打开 Python 交互式窗口  。 如果看不到输出 `4`，请重新检查步骤。

> [!Tip]
> Python 工作负载包括有用的 Cookiecutter 扩展，扩展提供图形用户界面以发现模板、输入模板选项及创建项目和文件。 有关详细信息，请参阅[使用 Cookiecutter](using-python-cookiecutter-templates.md)。

> [!Note]
> 目前尚不提供 Python 支持 Visual Studio for Mac，但通过 Visual Studio Code 在 Mac 和 Linux 上可用。 请参阅[问题和解答](overview-of-python-tools-for-visual-studio.md#questions-and-answers)。

:::moniker range=">=vs-2022"

## <a name="visual-studio-2022"></a>Visual Studio 2022

:::moniker-end
:::Moniker range="vs-2019"

## <a name="visual-studio-2019"></a>Visual Studio 2019

:::moniker-end
:::moniker range="vs-2017"

## <a name="visual-studio-2017"></a>Visual Studio 2017

:::moniker-end

1. 下载并运行最新 Visual Studio 安装程序。 如果已安装 Visual Studio，则运行 Visual Studio 安装程序，选择“修改”选项（请参阅[修改 Visual Studio](../install/modify-visual-studio.md)），并转到步骤 2。

    :::moniker range=">=vs-2022"
  
   >[!div class="nextstepaction"]
   > [安装 Visual Studio 2022 Community](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Community&rel=17)

    >[!Tip]
    > Community Edition 适用于个体开发者、课堂学习、学术研究和开放源代码开发。 对于其他用户，请安装[Visual Studio 2022 Professional](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Professional&rel=17)或[Visual Studio 2022 Enterprise](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Enterprise&rel=17)

    :::moniker-end
    :::moniker range="vs-2019"

   >[!div class="nextstepaction"]
   > [安装 Visual Studio 2019 Community](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Community&rel=15&rid=34347&utm_source=docs&utm_medium=clickbutton&utm_campaign=python_gettingstarted)

    >[!Tip]
    > Community Edition 适用于个体开发者、课堂学习、学术研究和开放源代码开发。 对于其他用途，请安装 [Visual Studio 2019 Professional](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Professional&rel=15&rid=34347&utm_source=docs&utm_medium=clickbutton&utm_campaign=python_gettingstarted) 或 [Visual Studio 2019 Enterprise](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Enterprise&rel=15&rid=34347&utm_source=docs&utm_medium=clickbutton&utm_campaign=python_gettingstarted)。

    :::moniker-end
    :::moniker range="vs-2017"

   >[!div class="nextstepaction"]
   > [安装 Visual Studio 2017 社区](https://my.visualstudio.com/Downloads?q=Visual-Studio-2017)
    :::moniker-end

1. Visual Studio 安装程序提供了工作负荷列表，这些工作负荷是特定开发区域的相关选项的组。 对于 Python，请选择 **Python 开发** 工作负载。

   可选：如果使用数据科学，还可考虑使用 **数据科学和分析应用程序** 工作负载。 此工作负载包含 Python、R 和 F# 语言支持。 有关详细信息，请参阅[数据科学和分析应用程序工作负载](data-science-and-analytical-applications-workload.md)。

   ![Visual Studio 安装程序中的 Python 开发工作负荷 ](media/installation-python-workload.png) 。
    

1. 如果需要，请在安装程序的右侧选择其他选项。 跳过此步骤，接受默认选项。
   :::moniker range=">=vs-2022"

   ![Visual Studio 2022 安装程序中的 Python 开发选项](media/installation-python-options-2022.png)

   :::moniker-end

   :::moniker range="vs-2019"

   ![Visual Studio 2019 安装程序中的 Python 开发选项](media/installation-python-options-2019.png)

   :::moniker-end

   :::moniker range="vs-2017"

   ![Visual Studio 2017 安装程序中的 Python 开发选项](media/installation-python-options.png)

   :::moniker-end

 | 选项 | 描述 |
   | --- | --- |
| Python 分发版本 | 选择计划使用的可用选项任意组合，例如 Python 2、Python 3、Miniconda、Anaconda2 和 Anaconda3 分发版本的 32 位和 64 位变体。 每个组合都包含分发版本的解释器、运行时和库。 具体来说，Anaconda 是开放数据科学平台，包含各种预安装的包。  (你可以随时返回到 Visual Studio 安装程序以添加或删除分发。 ) **注意**：如果你在 Visual Studio 安装程序之外安装了分发版，则无需在此处检查等效的选项。 Visual Studio 会自动检测现有的 Python 安装。 请参阅[“Python 环境”窗口](managing-python-environments-in-visual-studio.md#the-python-environments-window)。 此外，若有比安装程序中所显示的版本更高的 Python 版本可用，可以单独安装较高版本，并且 Visual Studio 会检测到它。 |
| **Cookiecutter 模板支持** | 安装 Cookiecutter 图形用户界面，用于发现模板、输入模板选项以及创建项目和文件。 请参阅[使用 Cookiecutter 扩展](using-python-cookiecutter-templates.md)。 |
| **Python Web 支持** | 安装用于 Web 开发的工具（包括 HTML、CSS 和 JavaScript 编辑支持）以及用于使用 Bottle、Flask 和 Django 框架的项目的模板。 请参阅 [Python Web 项目模板](python-web-application-project-templates.md)。 |
| **Python 本机开发工具** | 安装 C++ 编译器和其他必要组件用于开发 Python 本机扩展。 请参阅[创建适用于 Python 的 C++ 扩展](working-with-c-cpp-python-in-visual-studio.md)。 若要获取全面的 C++ 支持，还请安装“使用 C++ 的桌面开发”工作负载。 |

安装后，安装程序会提供用于修改、启动、修复或卸载 Visual Studio 的选项。 当已安装的所有组件均可使用 Visual Studio 更新时，“修改”按钮将更改为“更新” 。 （随后在下拉菜单中提供“修改”选项。）还可搜索“Visual Studio”，从 Windows “开始”菜单启动 Visual Studio 及安装程序。

:::moniker range=">=vs-2022"

   ![从安装程序启动、修改、修改或卸载 Visual Studio-2022](media/installation-vs-launch-2022.png)

:::moniker-end
:::moniker range="vs-2019"

   ![从安装程序启动、修改、修改或卸载 Visual Studio-2019](media/installation-vs-launch.png)

:::moniker-end
:::moniker range="vs-2017"
  > [!Note]
> Python 和数据科学工作负载仅可用于 Visual Studio 2017 版本 15.2 及更高版本。
:::moniker-end

### <a name="troubleshooting"></a>疑难解答

若要在 Visual Studio 中安装或运行 Python 时解决问题，请尝试执行以下步骤：

- 确定使用 Python CLI（即在命令提示符处运行 python.exe）时是否会出现相同的问题。
- 使用 Visual Studio 安装程序中的[“修复”](../install/repair-visual-studio.md)选项。
- 在 Windows 中通过“设置” > “应用和功能”修复或重新安装 Python 。

**示例错误**：未能启动交互式进程：System.ComponentModel.Win32Exception (0x80004005)：Microsoft.PythonTools.Repl.PythonInteractiveEvaluator.d__43.MoveNext() 处未知错误 (0xc0000135)。

:::moniker range="<=vs-2017"

## <a name="visual-studio-2015"></a>Visual Studio 2015

1. 通过“控制面板”>“程序和功能”，选择 **Microsoft Visual Studio 2015**，然后选择“更改”，从而运行 Visual Studio 安装程序。

1. 在安装程序中，选择“修改”。

1. 选择 "**编程语言**" > **针对 Visual Studio 的 Python 工具** 然后单击 "**下一步**"：

   ![Visual Studio 2015 安装程序中的 PTVS 选项](media/installation-vs2015.png)

1. Visual Studio 安装程序完成后，[安装所选的 Python 解释器](installing-python-interpreters.md)。 Visual Studio 2015 仅支持 Python 3.5 及更早版本；更高版本生成类似“Python 3.6 版本不受支持”的消息。 如果你已安装解释器且 Visual Studio 不会自动检测它，请参阅[手动标识现有环境](managing-python-environments-in-visual-studio.md#manually-identify-an-existing-environment)。

## <a name="visual-studio-2013-and-earlier"></a>Visual Studio 2013 及更早版本

1. 为你的 Visual Studio 版本安装相应版本的针对 Visual Studio 的 Python 工具：

    - Visual Studio 2013：[PTVS 2.2.2 for Visual Studio 2013](https://github.com/Microsoft/PTVS/releases/v2.2.2)。 Visual Studio 2013 中的“文件” > “新建项目”对话框提供用于此过程的快捷方式 。
    - Visual Studio 2010 和 2012：[PTVS 2.1.1 for Visual Studio 2010 和 2012](https://github.com/Microsoft/PTVS/releases/v2.1.1)

1. [安装所选的 Python 解释器](installing-python-interpreters.md)。
如果你已安装解释器且 Visual Studio 不会自动检测它，请参阅[手动标识现有环境](managing-python-environments-in-visual-studio.md#manually-identify-an-existing-environment)。

:::moniker-end

## <a name="install-locations"></a>安装位置

:::moniker range=">=vs-2022"

默认情况下，Python 支持为计算机上的所有用户安装。

对于 Visual Studio 2022，Python 工作负荷安装在 *% ProgramFiles% \ Microsoft Visual Studio 中 \\<VS_version \\>*<VS_edition>Common7\IDE\Extensions\Microsoft\Python，其中 &lt; VS_version &gt; 为2022， &lt; VS_edition &gt; 为 Community、Professional 或Enterprise。

:::moniker-end
:::moniker range="<=vs-2019"

默认情况下，Python 支持为计算机上的所有用户安装。

对于 Visual Studio 2019 和 Visual Studio 2017，Python 工作负荷安装在 *% ProgramFiles (x86) % \ Microsoft Visual Studio \\<\\* VS_version><VS_edition>Common7\IDE\Extensions\Microsoft\Python，其中 &lt; VS_version &gt; 为2019或2017， &lt; VS_edition &gt; 是Community、Professional 或 Enterprise。

:::moniker-end

:::moniker range="<=vs-2017"

对于 Visual Studio 2015 及更早版本，安装路径如下所示：

- 32 位：
  - 路径：%Program Files(x86)%\Microsoft Visual Studio \<VS_ver>\Common7\IDE\Extensions\Microsoft\Python Tools for Visual Studio\\<PTVS_ver>
  - 路径的注册表位置：**HKEY_LOCAL_MACHINE\Software\Microsoft\PythonTools\\<VS_ver>\InstallDir**
- 64 位：
  - 路径：%Program Files%\Microsoft Visual Studio \<VS_ver>\Common7\IDE\Extensions\Microsoft\Python Tools for Visual Studio\\<PTVS_ver>
  - 路径的注册表位置：**HKEY_LOCAL_MACHINE\Software\Wow6432Node\Microsoft\PythonTools\\<VS_ver>\InstallDir**

其中：

- &lt;VS_ver&gt; 是：
  - Visual Studio 2015 14.0
  - Visual Studio 2013 12.0
  - Visual Studio 2012 11.0
  - Visual Studio 2010 10.0
- &lt;PTVS_ver&gt; 是版本号，例如 2.2.2、2.1.1、2.0、1.5、1.1 或 1.0。

### <a name="user-specific-installations-15-and-earlier"></a>特定于用户的安装（1.5 及更早版本）

针对 Visual Studio 的 Python 工具 1.5 及更早版本仅允许当前用户安装，在这种情况下，安装路径为 *%LocalAppData%\Microsoft\VisualStudio \\<VS_ver>\Extensions\Microsoft\针对 Visual Studio 的 Python 工具 \\<PTVS_ver>，* 其中 VS_ver 和 &lt; &gt; &lt; PTVS_ver &gt; 与上述相同。

:::moniker-end

---
title: 选择并安装 Python 解释器
description: Visual Studio 中支持的 Python 解释器的完整列表，并简要说明了可以在哪里找到它们的安装程序。
ms.date: 01/15/2022
ms.topic: how-to
author: rjmolyneaux
ms.author: rmolyneaux
manager: jmartens
ms.technology: vs-python
ms.workload:
- python
- data-science
ms.openlocfilehash: fb5074d5a1dc4f76eaaa814f1f730dae660cfa05
ms.sourcegitcommit: f81a8f381bcdbac96d112f815737ba1df55d97a3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2022
ms.locfileid: "137667351"
---
# <a name="install-python-interpreters"></a>安装 Python 解释器

默认情况下，在 Visual Studio 2017 和更高版本中安装 Python 开发工作负载也会同时安装 Python 3（64 位）。 可以根据需要选择安装 32 位和 64 位版本的 Python 2 和 Python 3，并安装 Miniconda (Visual Studio 2019) 或者 Anaconda 2/Anaconda 3 (Visual Studio 2017)，如[安装](installing-python-support-in-visual-studio.md)中所述。

::: moniker range=">=vs-2019"
或者，也可以从“添加环境”对话框中安装标准 Python 解释器。 在“Python 环境”窗口或 Python 工具栏中选择“添加环境”命令，选择“Python 安装”选项卡，指示安装哪个解释器，并选择“安装”。
::: moniker-end

除了 Visual Studio 安装程序，还可以手动安装下表列出的任何解释器。 例如，如果在安装 Visual Studio 之前安装了 Anaconda 3，则不需要通过 Visual Studio 安装程序再次进行安装。 例如，如果在 Visual Studio 安装程序中尚无可安装的更高版本，也可以手动安装解释器。

::: moniker range="<=vs-2017"
> [!Note]
> Visual Studio 支持 Python 版本 2.7 以及版本 3.5 - 3.7。 可以使用 Visual Studio 编辑在 Python 其他版本中编写的代码时，这些版本不受官方支持，IntelliSense 和调试等功能可能无法正常工作。
::: moniker-end

::: moniker range=">vs-2017"
> [!Note]
> Visual Studio 支持 Python 3.7 版本。 可以使用 Visual Studio 编辑在 Python 其他版本中编写的代码时，这些版本不受官方支持，IntelliSense 和调试等功能可能无法正常工作。
::: moniker-end

对于 Visual Studio 2015 及更早版本，必须手动安装其中一个解释器。

> [!Note]
> 尽管 Visual Studio 提供了安装 Anaconda 分发版的服务，但你对 Anaconda 存储库中发行版和其他包的使用都受 [Anaconda 服务条款](https://www.anaconda.com/terms-of-service)的约束。 这些条款可能要求一些组织向 Anaconda 支付商业许可证，否则就需要配置工具来访问备用存储库。 有关详细信息，请参阅 [Conda 通道文档](https://docs.conda.io/projects/conda/en/latest/user-guide/concepts/channels.html)。

Visual Studio（所有版本）通过检查注册表（根据 [PEP 514 - Windows 注册表中的 Python 注册](https://www.python.org/dev/peps/pep-0514/)）自动检测各个已安装的 Python 解释器及其环境。 Python 安装通常位于 HKEY_LOCAL_MACHINE\SOFTWARE\Python（32 位）和 HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Python（64 位）下的“PythonCore”(CPython) 和“ContinuumAnalytics”(Anaconda) 等分发节点中。

如果 Visual Studio 并未检测到安装的环境，请参阅[手动标识现有环境](managing-python-environments-in-visual-studio.md#manually-identify-an-existing-environment)。

Visual Studio 在[Python 环境”](managing-python-environments-in-visual-studio.md#the-python-environments-window)窗口中显示所有已知环境，并自动检测现有解释器的更新。

| 解释器 | 说明 |
| --- | --- |
| [CPython](https://www.python.org/) | 32位和64位版本中提供的 "本机" 和最常用解释器 (32 位建议) 。 包括最新的语言功能、最大的 Python 包兼容性、完整的调试支持以及与 [IPython](https://ipython.org/) 的互操作。 另请参阅：[Should I use Python 2 or Python 3?](https://wiki.python.org/moin/Python2orPython3)（应使用 Python 2 还是 Python 3？） Visual Studio 2015 及更早版本不支持 python 3.6 +，并可提供类似于 **不受支持的 python 版本 3.6** 的错误。 请改用 Python 3.5 或更早版本。 |
| [IronPython](https://github.com/IronLanguages/ironpython2) | Python 的 .NET 实现，32 位和 64 位版本可用，提供 C#/F#/Visual Basic 互操作、对 .NET API 的访问、标准 Python 调试（但不是 C++ 混合模式调试）和混合 IronPython/C# 调试。 但 IronPython 不支持虚拟环境。 |
| [Anaconda](https://anaconda.com) | Python 提供技术支持的开放式数据科学平台，包括最新版本的 CPython 和大部分难以安装的包。 如果无法确定，建议使用 Anaconda。 |
| [PyPy](https://www.pypy.org/) | Python 的高性能跟踪 JIT 实现，适用于长时间运行的程序以及识别性能问题但找不到其他解决方法的情况。 可与 Visual Studio 配合使用，但对高级调试功能的支持有限。 |
| [Jython](https://www.jython.org/) | Java 虚拟机 (JVM) 上 Python 的实现。 与 IronPython 类似，Jython 中运行的代码可与 Java 类和库交互。 但是，许多适用于 CPython 的库可能无法访问。 可与 Visual Studio 配合使用，但对高级调试功能的支持有限。 |

对于想要提供新形式的 Python 环境检测的开发人员，请参阅 [PTVS 环境检测](https://github.com/Microsoft/PTVS/wiki/Extensibility-Environments) (github.com)。

## <a name="move-an-interpreter"></a>移动解释器

如果将现有解释器移到使用文件系统的新位置，则 Visual Studio 不会自动检测更改。

- 如果最初通过“Python 环境”窗口指定解释器的位置，则使用该窗口中的“配置”选项卡来编辑其环境，以确定新位置。 请参阅[手动标识现有环境](managing-python-environments-in-visual-studio.md#manually-identify-an-existing-environment)。

- 如果使用安装程序安装解释器，则使用以下步骤在新位置重新安装解释器：

  1. 将 Python 解释器还原到其原始位置。
  2. 使用其安装程序卸载解释器，这会清除注册表项。
  3. 在新位置重新安装解释器。
  4. 重新启动 Visual Studio，它应自动检测新位置以替代旧位置。

遵循此过程，确保标识解释器位置的注册表项正确更新，以供 Visual Studio 使用。 使用安装程序还可以处理可能存在的任何其他副作用。

## <a name="see-also"></a>另请参阅

- [管理 Python 环境](managing-python-environments-in-visual-studio.md)
- [为项目选择解释器](selecting-a-python-environment-for-a-project.md)
- [对依赖项使用 requirements.txt](managing-required-packages-with-requirements-txt.md)
- [搜索路径](search-paths.md)
- [“Python 环境”窗口参考](python-environments-window-tab-reference.md)

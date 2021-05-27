---
title: 编写 Python 的 C++ 扩展
description: 使用 Visual Studio、CPython 和 PyBind11 创建适用于 Python 的 C++ 扩展的演练，包括混合模式调试。
ms.date: 05/11/2021
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 286d5f2c316379316b1a1cf55334cab39cdc247c
ms.sourcegitcommit: 69256dc47489853dc66a037f5b0c1275977540c0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/12/2021
ms.locfileid: "109782629"
---
# <a name="create-a-c-extension-for-python"></a>创建适用于 Python 的 C++ 扩展

使用 C++（或 C）编写的模块常用于扩展 Python 解释器的功能和启用对低级别操作系统功能的访问。 主要有以下 3 种类型的模块：

- 加速器模块：Python 是一种解释型语言，某些代码段可使用 C++ 进行编写来提高性能。
- 包装器模块：向 Python 代码公开现有 C/C++ 接口，或公开易于通过 Python 使用的更“Python 化”的 API。
- 低级别系统访问模块：创建后可用来访问 `CPython` 运行时、操作系统或基础硬件的较低级别功能。

本文逐步介绍了如何为 `CPython` 生成 C++ 扩展模块，用于计算双曲正切并通过 Python 代码调用它。 首先使用 Python 实现此例程，以演示使用 C++ 实现此相同例程时可获得的相对性能提升。

本文还演示了使 C++ 可用于 Python 的两种方法：

- [Python 文档](https://docs.python.org/3/c-api/)中所述的标准 `CPython` 扩展
- [PyBind11](https://github.com/pybind/pybind11)，由于其简单易用，推荐用于 C++ 11。

要获取本演练的完整示例，请访问 [python-samples-vs-cpp-extension](https://github.com/Microsoft/python-sample-vs-cpp-extension) (GitHub)。

## <a name="prerequisites"></a>先决条件

- 安装了“Python 开发”工作负载的 Visual Studio 2017 或更高版本，此工作负载包括“Python 本机开发工具”，带来了本机扩展所需的 C++ 工作负载和工具集。

    ![选择“Python 本机开发工具”选项](media/cpp-install-native.png)

    > [!Tip]
    > 安装 **数据科学和分析应用程序** 工作负载还包括默认安装 Python 和“Python 本机开发工具”选项。

若要详细了解安装选项，请参阅[安装对 Visual Studio 的 Python 支持](installing-python-support-in-visual-studio.md)。 如果单独安装 Python，请务必在安装程序的“高级选项”下选择“下载调试符号”。 若要在 Python 代码和本机代码之间使用混合模式调试，则必须使用此选项。

## <a name="create-the-python-application"></a>创建 Python 应用程序

1. 要在 Visual Studio 中创建新 Python 项目，请选择“文件” > “新建” > “项目”。 搜索“Python”，选择“Python 应用程序”模板，为它指定你选择的名称和位置，然后选择“确定”。

1. 在项目的 .py 文件中，粘贴以下代码（或手动输入它来体验一些 [Python 编辑功能](editing-python-code-in-visual-studio.md)）。 此代码在不使用数学库的情况下计算双曲正切，我们将使用本机扩展来加速此代码。

    > [!Tip]
    > 在用 C++ 重写之前，请先用纯 Python 编写代码。 通过这种方式，你可以更轻松地检查本机代码是否正确

    ```python
    from random import random
    from time import perf_counter

    COUNT = 500000  # Change this value depending on the speed of your computer
    DATA = [(random() - 0.5) * 3 for _ in range(COUNT)]

    e = 2.7182818284590452353602874713527

    def sinh(x):
        return (1 - (e ** (-2 * x))) / (2 * (e ** -x))

    def cosh(x):
        return (1 + (e ** (-2 * x))) / (2 * (e ** -x))

    def tanh(x):
        tanh_x = sinh(x) / cosh(x)
        return tanh_x

    def test(fn, name):
        start = perf_counter()
        result = fn(DATA)
        duration = perf_counter() - start
        print('{} took {:.3f} seconds\n\n'.format(name, duration))

        for d in result:
            assert -1 <= d <= 1, " incorrect values"

    if __name__ == "__main__":
        print('Running benchmarks with COUNT = {}'.format(COUNT))

        test(lambda d: [tanh(x) for x in d], '[tanh(x) for x in d] (Python implementation)')
    ```

1. 使用“调试” > “启动而不调试”(Ctrl+F5) 运行程序以查看结果。 用户可调整 `COUNT` 变量，更改基准检验的运行时长。 对于本演练，请将计数设置为让基准检验运行约 2 秒。

> [!TIP]
> 运行基准检验时，请始终使用“调试” > “启动而不调试”，从而避免在 Visual Studio 调试器中运行代码时产生开销。

## <a name="create-the-core-c-projects"></a>创建核心 C++ 项目

按照本节中的说明，创建名为“superfastcode”和“superfastcode2”的两个完全相同的 C++ 项目。 稍后，你将在每个项目中使用两种不同的方法将 C++ 代码公开给 Python。

1. 在“解决方案资源管理器”中右键单击此解决方案并选择“添加” > “新建项目”。 一个 Visual Studio 解决方案可同时包含 Python 和 C++ 项目（这是使用 Visual Studio for Python 的优势之一）。

1. 搜索“C++”，选择“空项目”，指定名称“superfastcode”（第二个项目则指定名称“superfastcode2”），然后选择“确定”。

    > [!Tip]
    > 如果在 Visual Studio 中安装了 Python 本机开发工具，则可改为从 Python 扩展模块模板开始，其中有许多现成的以下所述的内容。 但是，对于本演练，从空项目开始可以逐步演示如何生成扩展模块。 了解该过程后，在编写自己的扩展时，使用模板可帮助你节省时间。

1. 在新项目中创建 C++ 文件，方法是右键单击“源文件”节点，然后选择“添加” > “新建项”，选择“C++ 文件”，将其命名为 `module.cpp`，然后选择“确定”。

    > [!Important]
    > 需要扩展名为 .cpp 的文件才能在随后步骤中打开 C++ 属性页。

1. 如果使用的是 64 位 Python 运行时，请使用主工具栏中的下拉菜单来激活 x64 配置。 对于 32 位 Python 运行时，请激活 Win32 配置。

1. 右键单击“解决方案资源管理器”中的 C++ 项目，然后选择“属性”。 “配置”值应为“活动(调试)”，“平台”将为“活动(x64)”或“活动(Win32)”，具体取决于你在上一步中的选择。

    > [!Tip]
    > 对于你自己的项目，不妨同时配置“调试”和“发布”配置。 此处，我们只配置“调试”配置，并将其设置为使用 `CPython` 的发行版本，这将禁用 C++ 运行时的一些调试功能，包括断言。 使用 `CPython` 调试二进制文件 (`python_d.exe`) 将需要不同的设置。

1. 如下表所述设置特定属性，然后选择“确定”。
    ::: moniker range=">=vs-2019"
    | Tab | Property | “值” |
    | --- | --- | --- |
    | **常规** | **目标名称** | 指定想要在 `from...import` 语句中从 Python 引用的模块的名称。 定义 Python 的模块时，在 C++ 中使用相同的名称。 如果想要将项目的名称用作模块名称，请保留默认值 $(ProjectName)。 对于 `python_d.exe`，在名称末尾添加 `_d`。 |
    | | **配置类型** | **动态库(.dll)** |
    | **高级** | 目标文件扩展名 | **.pyd** |
    | C/C++ > 常规 | **附加包含目录** | 根据相应的安装添加 Python“include” 文件夹，例如 `c:\Python36\include`。  |
    | C/C++ > 预处理器 | **预处理器定义** | 如果存在，请将 _DEBUG 值更改为 NDEBUG，以匹配 `CPython` 的非调试版本。 （当使用 `python_d.exe` 时，保持此设置不变。） |
    | C/C++ > 代码生成 | **运行时库** | 多线程 DLL (/MD)，以匹配 `CPython` 的非调试版本。 （当使用 `python_d.exe` 时，保持此设置不变。） |
    | 链接器 > 常规 | **附加库目录** | 根据相应的安装添加包含 .lib 文件的 Python“libs”文件夹，例如 `c:\Python36\libs`。 （务必指向包含 .lib 文件的“libs”文件夹，而非包含 .py 文件的 Lib 文件夹。） |
    ::: moniker-end
    ::: moniker range="=vs-2017"
    | Tab | Property | “值” |
    | --- | --- | --- |
    | **常规** | 常规 > 目标名称 | 指定想要在 `from...import` 语句中从 Python 引用的模块的名称。 定义 Python 的模块时，在 C++ 中使用相同的名称。 如果想要将项目的名称用作模块名称，请保留默认值 $(ProjectName)。 对于 `python_d.exe`，在名称末尾添加 `_d`。 |
    | | 常规 > 目标扩展名 | **.pyd** |
    | | 项目默认值 > 配置类型 | **动态库(.dll)** |
    | C/C++ > 常规 | **附加包含目录** | 根据相应的安装添加 Python“include” 文件夹，例如 `c:\Python36\include`。  |
    | C/C++ > 预处理器 | **预处理器定义** | 如果存在，请将 _DEBUG 值更改为 NDEBUG，以匹配 `CPython` 的非调试版本。 （当使用 `python_d.exe` 时，保持此设置不变。） |
    | C/C++ > 代码生成 | **运行时库** | 多线程 DLL (/MD)，以匹配 `CPython` 的非调试版本。 （当使用 `python_d.exe` 时，保持此设置不变。） |
    | 链接器 > 常规 | **附加库目录** | 根据相应的安装添加包含 .lib 文件的 Python“libs”文件夹，例如 `c:\Python36\libs`。 （务必指向包含 .lib 文件的“libs”文件夹，而非包含 .py 文件的 Lib 文件夹。） |
    ::: moniker-end
    
    > [!Tip]
    > 如果在项目属性中未看到 C/C++ 选项卡，这是因为项目不包含标识为 C/C++ 源文件的任何文件。 如果创建的源文件不含 .c 或 .cpp 扩展名，则可能出现这种情况。 例如，如果之前在“新建项”对话框中不小心输入了 `module.coo`（而不是 `module.cpp`），则 Visual Studio 会创建文件，但不会将文件类型设置为“C/C+ 代码”，而正是它激活 C/C++ 属性选项卡。即使将文件重命名为带 `.cpp`，此类识别错误仍会存在。 为了正确设置文件类型，请在“解决方案资源管理器”中右键单击文件，选择“属性”，然后将“文件类型”设置为“C/C++ 代码”。

1. 右键单击 C++ 项目，然后选择“生成”来测试配置（包括“调试”和“发布”）。 .pyd 文件位于“调试”和“发布”下的“解决方案”文件夹中，而非位于 C++ 项目文件夹本身。

1. 将以下代码添加到 C++ 项目的 module.cpp 文件：

    ```cpp
    #include <Windows.h>
    #include <cmath>

    const double e = 2.7182818284590452353602874713527;

    double sinh_impl(double x) {
        return (1 - pow(e, (-2 * x))) / (2 * pow(e, -x));
    }

    double cosh_impl(double x) {
        return (1 + pow(e, (-2 * x))) / (2 * pow(e, -x));
    }

    double tanh_impl(double x) {
        return sinh_impl(x) / cosh_impl(x);
    }
    ```

1. 再次生成 C++ 项目以确认代码正确。

1. 如果尚未执行此操作，请重复上述步骤，再创建一个内容相同的项目，且名为“superfastcode2”。

## <a name="convert-the-c-projects-to-extensions-for-python"></a>将 C++ 项目转换为适用于 Python 的扩展

若要使 C++ DLL 成为适用于 Python 的扩展，首先应修改导出的方法以与 Python 类型交互。 然后，添加一个可导出模块的函数以及该模块的方法的定义。

接下来的各部分介绍了如何使用 `CPython` 扩展和 PyBind11 执行这些步骤。

### <a name="cpython-extensions"></a>CPython 扩展

有关此部分所示内容的更多背景，请参阅 python.org 上的 [Python/C API 参考手册](https://docs.python.org/3/c-api/index.html)，特别是[模块对象](https://docs.python.org/3/c-api/module.html)（请务必从右上角的下拉控件中选择你的 Python 版本，以查看正确的文档）。

1. 在 module.cpp 的顶部，包含 Python.h：

    ```cpp
    #include <Python.h>
    ```

1. 修改 `tanh_impl` 方法以接受和返回 Python 类型（即，`PyObject*`）：

    ```cpp
    PyObject* tanh_impl(PyObject* /* unused module reference */, PyObject* o) {
        double x = PyFloat_AsDouble(o);
        double tanh_x = sinh_impl(x) / cosh_impl(x);
        return PyFloat_FromDouble(tanh_x);
    }
    ```

1. 添加一个定义如何向 Python 呈现 C++ `tanh_impl` 函数的结构：

    ```cpp
    static PyMethodDef superfastcode_methods[] = {
        // The first property is the name exposed to Python, fast_tanh
        // The second is the C++ function with the implementation
        // METH_O means it takes a single PyObject argument
        { "fast_tanh", (PyCFunction)tanh_impl, METH_O, nullptr },

        // Terminate the array with an object containing nulls.
        { nullptr, nullptr, 0, nullptr }
    };
    ```

1. 添加一个定义模块的结构，因为要在 Python 代码中引用它（特别是在使用 `from...import` 语句时）。 （使其与“配置属性” > “常规” > “目标名称”中的项目属性中的值匹配。）在以下示例中，“superfastcode”模块名意味着可在 Python 中使用 `from superfastcode import fast_tanh`，因为 `fast_tanh` 是在 `superfastcode_methods` 中定义的。 （C++ 项目内部使用的文件名，如 module.cpp，是无关紧要的。）

    ```cpp
    static PyModuleDef superfastcode_module = {
        PyModuleDef_HEAD_INIT,
        "superfastcode",                        // Module name to use with Python import statements
        "Provides some functions, but faster",  // Module description
        0,
        superfastcode_methods                   // Structure that defines the methods of the module
    };
    ```

1. 添加 Python 加载模块时要调用的方法，该模块必须命名为 `PyInit_<module-name>`，其中 &lt;module-name&gt; 与 C++ 项目的“常规” > “目标名称”属性完全匹配（也就是说，其与项目生成的 .pyd 的文件名相匹配）。

    ```cpp
    PyMODINIT_FUNC PyInit_superfastcode() {
        return PyModule_Create(&superfastcode_module);
    }
    ```

1. 再次生成 C++ 项目来验证代码。 如果遇到错误，请参阅下面的[疑难解答](#troubleshooting)一节。

### <a name="pybind11"></a>PyBind11

如果已完成上一节中的步骤，你肯定已注意到，你使用了大量样本代码来为 C++ 代码创建必要的模块结构。 PyBind11 通过 C++ 头文件中的宏简化了进程，这些宏通过更少的代码实现了相同的结果。 有关本节所示内容的背景信息，请参阅[PyBind11 基础知识](https://github.com/pybind/pybind11/blob/master/docs/basics.rst)。

1. 使用 pip 安装 PyBind11：`pip install pybind11` 或 `py -m pip install pybind11`。 （或者，也可以使用“Python 环境”窗口进行安装，然后使用“在 Powershell 中打开”命令执行下一步。）

1. 在同一终端中，运行 `python -m pybind11 --includes` 或 `py -m pybind11 --includes`。 这会打印应添加到项目的“C/C ++” > “常规” > “附加包含目录”属性中的路径列表（删除 `-I` 前缀（若有））。

1. 在全新的 module.cpp（不包括来自上一部分的任何更改）的顶部，添加 pybind11.h：

    ```cpp
    #include <pybind11/pybind11.h>
    ```

1. 在 module.cpp 的底部，使用 `PYBIND11_MODULE` 宏来定义 C++ 函数的入口点：

    ```cpp
    namespace py = pybind11;

    PYBIND11_MODULE(superfastcode2, m) {
        m.def("fast_tanh2", &tanh_impl, R"pbdoc(
            Compute a hyperbolic tangent of a single argument expressed in radians.
        )pbdoc");

    #ifdef VERSION_INFO
        m.attr("__version__") = VERSION_INFO;
    #else
        m.attr("__version__") = "dev";
    #endif
    }
    ```

1. 生成 C++ 项目来验证代码。 如果遇到错误，请参阅下一节有关疑难解答的内容。

### <a name="troubleshooting"></a>疑难解答

C++ 模块可能无法编译的原因如下：

- 无法找到 Python.h （E1696：无法打开源文件 "Python.h" 和/或 C1083：无法打开 include 文件："Python.h"：没有此类文件或目录）：验证项目属性中的“C/C++” > “常规” > “附加 Include 目录”中的路径是否指向 Python 安装的“include”文件夹。 请参阅[创建核心 C++ 项目](#create-the-core-c-projects)中的步骤 6。

- 无法找到 Python 库：验证项目属性中的“链接器” > “常规” > “附加库目录”中的路径是否指向 Python 安装的“libs”文件夹。 请参阅[创建核心 C++ 项目](#create-the-core-c-projects)中的步骤 6。

- 与目标体系结构相关的链接器错误：更改 C++ 目标的项目体系结构以匹配 Python 安装。 例如，如果将 C++ 项目的目标定为 Win32，但是 Python 安装是 64 位，则将 C++ 项目更改为 x64。

## <a name="test-the-code-and-compare-the-results"></a>测试代码和比较结果

将 DLL 结构化为 Python 扩展后，便可从 Python 项目引用它们，导入模块，并使用其方法。

### <a name="make-the-dll-available-to-python"></a>使 DLL 可供 Python 使用

可通过两种方法使 DLL 可供 Python 使用。

如果 Python 项目和 C++ 项目在相同的解决方案中，则使用第一种方法。 转到“解决方案资源管理器”，右键单击 Python 项目中的“引用”节点，然后选择“添加引用”。 在随即出现的对话框中，选择“项目”选项卡，同时选择“superfastcode”和“superfastcode2”项目，然后选择“确定”。

![添加对 superfastcode 项目的引用](media/cpp-add-reference.png)

下面步骤中描述的替代方法将模块安装到 Python 环境中，使其也可用于其他 Python 项目。 有关更完整的文档，请访问 [setuptools 项目](https://setuptools.readthedocs.io/)。

1. 右键单击 C++ 项目，然后选择“添加” > “新建项”，在项目中创建名为 setup.py 的文件。 然后选择“C++ 文件 (.cpp)”并命名为 `setup.py`，再选择“确定”（尽管使用了 C++ 文件模板，但使用 .py 扩展命名文件可让 Visual Studio 将其识别为 Python）。 编辑器中出现该文件时，以适合扩展方法的形式将以下代码粘贴到其中：

    `CPython` 扩展（superfastcode 项目）：

    ```python
    from setuptools import setup, Extension

    sfc_module = Extension('superfastcode', sources = ['module.cpp'])

    setup(
        name='superfastcode',
        version='1.0',
        description='Python Package with superfastcode C++ extension',
        ext_modules=[sfc_module]
    )
    ```

    `PyBind11`（superfastcode2 项目）：

    ```python
    from setuptools import setup, Extension
    import pybind11

    cpp_args = ['-std=c++11', '-stdlib=libc++', '-mmacosx-version-min=10.7']

    sfc_module = Extension(
        'superfastcode2',
        sources=['module.cpp'],
        include_dirs=[pybind11.get_include()],
        language='c++',
        extra_compile_args=cpp_args,
        )

    setup(
        name='superfastcode2',
        version='1.0',
        description='Python package with superfastcode2 C++ extension (PyBind11)',
        ext_modules=[sfc_module],
    )
    ```

1. 在 C++ 项目中创建另一个名为 pyproject.toml 的文件，然后将以下代码粘贴到其中。

    ```toml
    [build-system]
    requires = ["setuptools", "wheel", "pybind11"]
    build-backend = "setuptools.build_meta"
    ```

1. 若要生成扩展，请右键单击打开的 pyproject.toml 选项卡，然后选择“复制完整路径”（在使用之前，我们将从路径中删除 pyproject.toml 名称）。

1. 在“解决方案资源管理器”中，右键单击当前活动的 Python 环境，然后选择“管理 Python 包”。

    > [!Tip]
    > 如果你已经安装了包，则会看到它在此处列出。 单击“X”卸载它，然后继续操作。

1. 将复制的路径粘贴到搜索框中，并从末尾删除 `pyproject.toml`。 然后，按 Enter 从此目录进行安装。

    > [!Tip]
    > 如果由于权限错误导致安装失败，请添加 `--user`，然后重试命令。


### <a name="call-the-dll-from-python"></a>从 Python 调用 DLL

如上一节所述，使 DLL 可用于 Python 之后，现在可以从 Python 代码中调用 `superfastcode.fast_tanh` 和 `superfastcode2.fast_tanh2` 函数，并将它们的性能与 Python 实现进行比较：

1. 在 .py 文件中添加以下行，调用从 DLL 中导出的方法并显示其输出：

    ```python
    from superfastcode import fast_tanh
    test(lambda d: [fast_tanh(x) for x in d], '[fast_tanh(x) for x in d] (CPython C++ extension)')

    from superfastcode2 import fast_tanh2
    test(lambda d: [fast_tanh2(x) for x in d], '[fast_tanh2(x) for x in d] (PyBind11 C++ extension)')
    ```

1. 运行 Python 程序（“调试” > “启动而不调试”或按 Ctrl+F5），观察到 C++ 例程的运行速度约比 Python 实现快 5 到 20 倍。 典型输出形式如下：

    ```output
    Running benchmarks with COUNT = 500000
    [tanh(x) for x in d] (Python implementation) took 0.758 seconds

    [fast_tanh(x) for x in d] (CPython C++ extension) took 0.076 seconds

    [fast_tanh2(x) for x in d] (PyBind11 C++ extension) took 0.204 seconds
    ```

    如果已禁用“启动而不调试”命令，请右键单击“解决方案资源管理器”中的 Python 项目，选择“设为启动项目”。

1. 尝试增加 `COUNT` 变量，让差异变得更明显。 C++ 模块调试版本的运行速度慢于发布版本的运行速度，因为调试版本优化程度较低，并包含各种错误检查。 可以随意在这些配置之间进行切换，以便进行比较（但请务必返回并更新你之前为“发布”配置设置的属性）。

在输出中，你可能会看到 PyBind11 扩展没有 `CPython` 扩展快，尽管它应该比纯 Python 实现快得多。 这主要是因为我们使用了 `METH_O` 调用，它不支持多个参数、参数名称或关键字参数。 PyBind11 生成稍微复杂一些的代码，以便为调用方提供更类似于 Python 的接口，但是由于测试代码调用函数 500,000 次，结果可能会极大地放大这种开销！

可以通过将 `for` 循环到本机代码中来进一步减少开销。 这将涉及使用[迭代器协议](https://docs.python.org/c-api/iter.html)（或 PyBind11 用于[函数参数](https://pybind11.readthedocs.io/en/stable/advanced/functions.html#python-objects-as-args)的 `py::iterable` 类型）来处理每个元素。 删除 Python 和 C++ 之间的重复转换是缩短处理序列所需时间的有效方法。

### <a name="troubleshooting"></a>疑难解答

如果在尝试导入模块时看到 `ImportError`，则可能是以下问题之一导致的：

* 当通过项目引用进行生成时，请确保 C++ 项目属性与为 Python 项目激活的 Python 环境匹配，特别是 Include 和 Library 目录。

* 请确保输出文件名为 `superfastcode.pyd`。 其他文件名或扩展名会阻止它被导入。

* 如果你使用 setup.py 文件安装了模块，请检查是否在为 Python 项目激活的 Python 环境中运行了 pip 命令。 在“解决方案资源管理器”中扩展 Python 环境应显示 `superfastcode` 的条目。

## <a name="debug-the-c-code"></a>调试 C++ 代码

Visual Studio 支持一起调试 Python 和 C++ 代码。 本节演示了使用 superfastcode 项目的整个过程；superfastcode2 项目的步骤与此相同。

1. 在“解决方案资源管理器”中，右键单击 Python 项目，依次选择“属性”、“调试”选项卡，然后选择“调试” > “启用本机代码调试”选项。

    > [!Tip]
    > 启用本机代码调试后，Python 输出窗口可能在程序完成后立即消失，而不出现通常的“按任何键以继续”暂停界面。 若要强制暂停，请在启用本机代码调试后，向“调试”选项卡上的“运行” > “解释器参数”字段添加 `-i` 选项。 此参数会在代码完成后将 Python 解释器置于交互模式，此时它等待用户按 Ctrl+Z > Enter 退出。 （或者，如果不介意修改 Python 代码，则可在程序结束时添加 `import os` 和 `os.system("pause")` 语句。 此代码会复制初始的暂停提示符。）

1. 选择“文件” > “保存”以保存属性更改。

1. 在 Visual Studio 工具栏中，将生成配置设置为“调试”。

    ![将生成配置设置为“调试”](media/cpp-set-debug.png)

1. 由于代码在调试器中运行时通常需要更长时间，可能需要将 .py 文件中的 `COUNT` 变量更改为小五倍的值（例如，从 `500000` 更改为 `100000`）。

1. 在 C++ 代码中，在 `tanh_impl` 方法内的第一行设置一个断点，然后启动调试器（F5 或“调试” > “开始调试”）。 调用该代码时，调试器将会停止。 如果未命中断点，请检查配置是否设置为“调试”以及是否已保存项目（启动调试器时，不会自动执行该操作）。

    ![在 C++ 代码中的断点处停止](media/cpp-debugging.png)

1. 此时，可浏览 C++ 代码、检查变量等。 这些功能在[一起调试 C++ 和 Python](debugging-mixed-mode-c-cpp-python-in-visual-studio.md) 中有详细介绍。

## <a name="alternative-approaches"></a>替代方法

下表描述了创建 Python 扩展的各种方法。 `CPython` 和 `PyBind11` 的前两个条目已经在本文中讨论过了。

| 方法 | 年份 | 代表用户 | 
| --- | --- | --- |
| 适用于 `CPython` 的 C/C++ 扩展模块 | 1991 | 标准库 | 
| [PyBind11](https://github.com/pybind/pybind11)（推荐用于 C++） | 2015 |  |
| [Cython](https://cython.org)（推荐用于 C） | 2007 | [gevent](https://www.gevent.org/)、[kivy](https://kivy.org/) |
| [HPy](https://hpyproject.org/) | 2019 | |
| [mypyc](https://mypyc.readthedocs.io/) | 2017 | |
| ctype | 2003 | [oscrypto](https://github.com/wbond/oscrypto) | 
| cffi | 2013 | [cryptography](https://cryptography.io/)、[pypy](https://pypy.org/) |
| SWIG | 1996 | [crfsuite](http://www.chokkan.org/software/crfsuite/) | 
| [Boost.Python](https://www.boost.org/doc/libs/1_66_0/libs/python/doc/html/index.html) | 2002 | |
| [cppyy](https://cppyy.readthedocs.io/) | 2017 | |

## <a name="see-also"></a>请参阅

要获取本演练的完整示例，请访问 [python-samples-vs-cpp-extension](https://github.com/Microsoft/python-sample-vs-cpp-extension) (GitHub)。

---
title: 编写 Python 的 C++ 扩展
description: 本文分步介绍如何使用 Visual Studio、CPython 和 PyBind11（包括混合模式调试）创建适用于 Python 的 C++ 扩展。
ms.custom: devdivchpfy22
ms.date: 12/20/2021
ms.topic: how-to
author: rjmolyneaux
ms.author: rmolyneaux
manager: jmartens
ms.technology: vs-python
ms.workload:
- python
- data-science
ms.openlocfilehash: aadcff465274916b7d872ab2a64116ab5bc3cf70
ms.sourcegitcommit: f303d052e451bcfd4722b99a9adbcb3f575d1678
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/27/2022
ms.locfileid: "137816799"
---
# <a name="create-a-c-extension-for-python"></a>创建适用于 Python 的 C++ 扩展

通常，使用 C++ (或 C) 模块来扩展 Python 解释器的功能。 还可使用它们来启用对低级别操作系统功能的访问。

主要有三种类型的模块：

- **加速器模块**：因为 Python 是一种解释型语言，所以可以编写 C++ 加速器模块来获得更高的性能。
- **包装器模块**：此类模块向 Python 代码公开现有 C/C++ 接口，或公开易于通过 Python 使用的更“Python 化”的 API。
- **低级别系统访问模块**：可创建此类模块以访问 `CPython` 运行时、操作系统或基础硬件的较低级别功能。

本文逐步介绍了如何为 `CPython` 生成 C++ 扩展模块，用于计算双曲正切并通过 Python 代码调用它。 首先使用 Python 实现此例程，以演示使用 C++ 实现此相同例程时可获得的相对性能提升。

本文还演示了使 C++ 扩展可用于 Python 的两种方法：

- 使用标准 `CPython` 扩展，如 [Python 文档](https://docs.python.org/3/c-api/)中所述。
- 使用 [PyBind11](https://github.com/pybind/pybind11)，由于其简单易用，因此推荐用于 C++11。 为了确保兼容性，请确保使用较新版本的 Python 之一。 

可通过 [python-samples-vs-cpp-extension](https://github.com/Microsoft/python-sample-vs-cpp-extension)，在 GitHub 上获取本演练中的完整示例。

## <a name="prerequisites"></a>先决条件

- Visual Studio 2017 或更高版本，已安装有 Python 开发工作负载。 该工作负载包括 Python 本机开发工具，它引入了本机扩展所需的 C++ 工作负载和工具集。

    ![Python 开发选项列表的屏幕截图，其中突出显示了 Python 本机开发工具选项。](media/cpp-install-native.png)

    > [!NOTE]
    > 在安装“数据科学和分析应用程序”工作负载时，会默认安装 Python 和“Python 本机开发工具”选项 。

若要详细了解安装选项，请参阅[安装对 Visual Studio 的 Python 支持](installing-python-support-in-visual-studio.md)。 如果单独安装 Python，请务必在安装程序的“高级选项”下选择“下载调试符号”。 若要在 Python 代码和本机代码之间使用混合模式调试，则必须使用此选项。

## <a name="create-the-python-application"></a>创建 Python 应用程序

1. 要在 Visual Studio 中创建新 Python 项目，请选择“文件” > “新建” > “项目”。 

1. 搜索“Python”，选择“Python 应用程序”模板，输入名称和位置，然后选择“确定”  。

1. 在项目的 .py 文件中粘贴以下代码。 要体验某些 [Python 编辑功能](editing-python-code-in-visual-studio.md)，请尝试手动输入代码。  

   此代码在不使用数学库的情况下计算双曲正切，你将使用本机扩展来加速此代码。

    > [!Tip]
    > 在用 C++ 重写之前，请先用纯 Python 编写代码。 通过这种方式，可以更轻松地检查本机代码是否正确。

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

1. 若要查看结果，请通过选择"调试开始而不调试"或按  >  **Ctrl+F5 运行程序**。

   可以调整 `COUNT` 变量以更改基准测试的运行时间。 对于本演练，请设置计数，以便基准测试大约需要两秒。

   > [!TIP]
   > 运行基准检验时，请始终使用“调试” > “启动但不调试” 。 这有助于避免在 Visual Studio 调试器中运行代码时产生开销。

## <a name="create-the-core-c-projects"></a>创建核心 C++ 项目

按照本节中的说明，创建名为“superfastcode”和“superfastcode2”的两个完全相同的 C++ 项目 。 稍后将在每个项目中使用单独的方法将 C++ 代码公开到 Python。

1. 在“解决方案资源管理器”中，右键单击解决方案，然后选择“添加” > “新建项目”  。 一个 Visual Studio 解决方案可同时包含 Python 和 C++ 项目（这是使用 Visual Studio for Python 的优势之一）。

1. 搜索“C++”，选择“空项目”，将第一个项目指定为“superfastcode”或将第二个项目指定为“superfastcode2”，然后选择“确定”    。

    > [!Tip]
    > 或者，如果在 Visual Studio 中安装了 Python 本机开发工具，则可从 Python 扩展模块模板开始。 该模块中有许多此处已介绍的现成内容。 
    > 
    > 但是，对于本演练，从空项目开始可以逐步演示如何生成扩展模块。 了解该过程后，可以在编写自己的扩展时利用模板来节省时间。

1. 若要在新项目中创建 C++ 文件，请右键单击“源文件”节点，然后选择“添加” > “新建项”  。

1. 选择“C++ 文件”，将其命名为“module.cpp”，然后选择“确定”。

    > [!Important]
    > 需要扩展名为 .cpp 的文件才能在随后步骤中打开 C++ 属性页。

1. 在主工具栏上，使用下拉菜单选择以下配置之一：

   * 对于 64 位 Python 运行时，请激活 x64 配置。 
   * 对于 32 位 Python 运行时，请激活 Win32 配置。

1. 在解决方案资源管理器中，右键单击 C++ 项目，选择“属性”，然后执行以下操作 ： 

   a. 在“配置”处输入“活动(调试)” 。  
   b. 根据你在前一个步骤中做出的选择，在“平台”处输入“活动(x64)”或“活动(Win32)”  。

    > [!NOTE]
    > 在创建自己的项目时，需要配置“调试”和“发布”配置 。 此单元将仅配置调试配置，并将其设置为使用 CPython 的发布版本。 此配置禁用 C++ 运行时的一些调试功能，包括断言。 要使用 CPython 调试二进制文件(python_d.exe)，需要完成不同的设置。

1. 按照下表中的内容设置属性：

    ::: moniker range=">=vs-2019"

    | Tab | Property | “值” |
    | --- | --- | --- |
    | **常规** | **目标名称** | 指定要在 `from...import` 语句中从 Python 引用的模块的名称。 定义 Python 的模块时，请在 C++ 代码中使用相同的名称。 若要将项目的名称用作模块名称，请保留默认值 $\<ProjectName>。  对于 `python_d.exe`，在名称末尾添加 `_d`。 |
    | | **配置类型** | **动态库(.dll)** |
    | | “高级”>“目标文件扩展” | **.pyd** |
    | | 项目默认值 > 配置类型 | **动态库(.dll)** |
    | C/C++ > 常规 | **附加包含目录** | 根据相应的安装添加 Python“include” 文件夹（例如 `c:\Python36\include`）。  |
    | C/C++ > 预处理器 | **预处理器定义** | 如果已存在，请将 _DEBUG 值更改为 NDEBUG，以匹配 CPython 的非调试版本。 使用 python_d.exe 时，请将此值保持不变。 |
    | C/C++ > 代码生成 | **运行时库** | 多线程 DLL (/MD)，以匹配 CPython 的非调试版本。 使用 python_d.exe 时，请将此值保留为“多线程调试 DLL (/MDd)”。 |
    | 链接器 > 常规 | **附加库目录** | 根据相应的安装添加包含 .lib 文件的 Python“libs”文件夹（例如 c:\Python36\libs）  。 务必指向包含 .lib 文件的“libs”文件夹，而非包含 .py 文件的 Lib 文件夹。 |
    | | |

    ::: moniker-end

    ::: moniker range="=vs-2017"

    | Tab | Property | “值” |
    | --- | --- | --- |
    | **常规** | 常规 > 目标名称 | 指定要在 `from...import` 语句中从 Python 引用的模块的名称。 定义 Python 的模块时，请在 C++ 代码中使用相同的名称。 若要将项目的名称用作模块名称，请保留默认值 $\<ProjectName>。 对于 `python_d.exe`，在名称末尾添加 `_d`。 |
    | | 常规 > 目标扩展名 | **.pyd** |
    | | 项目默认值 > 配置类型 | **动态库(.dll)** |
    | C/C++ > 常规 | **附加包含目录** | 根据相应的安装添加 Python“include” 文件夹（例如 c:\Python36\include） 。  |
    | C/C++ > 预处理器 | **预处理器定义** | 如果已存在，请将 _DEBUG 值更改为 NDEBUG，以匹配 `CPython` 的非调试版本。 使用 `python_d.exe` 时，请将此值保持不变。 |
    | C/C++ > 代码生成 | **运行时库** | 多线程 DLL (/MD)，以匹配 `CPython` 的非调试版本。 使用 `python_d.exe` 时，请将此值保持不变。 |
    | 链接器 > 常规 | **附加库目录** | 根据相应的安装添加包含 .lib 文件的 Python“libs”文件夹（例如 c:\Python36\libs）  。 务必指向包含 .lib 文件的“libs”文件夹，而非包含 .py 文件的 Lib 文件夹。 |
    | | |

    ::: moniker-end
    
    > [!NOTE]
    > 如果 " **c/c + +** " 选项卡未显示在项目属性中，则该项目不包含标识为 c/c + + 源文件的任何文件。 如果创建的源文件不含 .c 或 .cpp 文件扩展名，则可能出现这种情况 。 
    > 
    > 例如，如果在“新建项”对话框中不慎输入了“module.coo”（而不是“module.cpp”），Visual Studio 会创建该文件，但不会将文件类型设置为 C/C+ 代码，该文件类型能激活“C/C++ 属性”选项卡。即使将该文件重命名为带有 .cpp 文件扩展名，此标识错误仍会存在   。 
    > 
    > 若要正确设置文件类型，请在解决方案资源管理器中右键单击该文件，然后选择“属性” 。 然后在“文件类型”处选择“C/C++ 代码” 。

1. 选择“确定”  。

1. 通过右键单击 C++ 项目，然后选择“生成”，可以测试配置（包括“调试”和“发布”） 。 

   你将在解决方案文件夹中的“调试”和“发布”下找到 .pyd 文件，而非 C++ 项目文件夹本身   。

1. 将以下代码添加到 C++ 项目的 module.cpp 文件中：

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

1. 如果尚未执行此操作，请重复上述步骤，采用相同的配置创建名为“superfastcode2”的第二个项目。

## <a name="convert-the-c-projects-to-extensions-for-python"></a>将 C++ 项目转换为适用于 Python 的扩展

若要使 c + + DLL 成为 Python 的扩展，请首先修改导出的方法以与 Python 类型交互。 然后，添加一个用于导出模块的函数以及该模块的方法的定义。

以下各节介绍如何使用 CPython 扩展和 PyBind11 执行这些步骤。

### <a name="use-cpython-extensions"></a>使用 CPython 扩展

有关本部分中所示代码的更多背景信息，请参阅 [Python/C API 参考手册](https://docs.python.org/3/c-api/index.html)，特别是[模块对象](https://docs.python.org/3/c-api/module.html)页。 请确保在右上角的下拉列表中选择你的 Python 版本。

1. 在 module.cpp 文件顶部，添加 Python.h ：

    ```cpp
    #include <Python.h>
    ```

1. 修改 `tanh_impl` 方法以接受和返回 Python 类型（即 `PyObject*`）：

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

1. 添加一个定义模块的结构，因为要在 Python 代码中引用它（特别是在使用 `from...import` 语句时）。 

   此代码中要导入的名称应与“配置属性” > “常规” > “目标名称”中的项目属性值匹配  。 

   在以下示例中，`"superfastcode"` 模块名意味着可在 Python 中使用 `from superfastcode import fast_tanh`，因为 `fast_tanh` 是在 `superfastcode_methods` 中定义的。 C++ 项目的内部文件名称（如 module.cpp）是无关紧要的。

    ```cpp
    static PyModuleDef superfastcode_module = {
        PyModuleDef_HEAD_INIT,
        "superfastcode",                        // Module name to use with Python import statements
        "Provides some functions, but faster",  // Module description
        0,
        superfastcode_methods                   // Structure that defines the methods of the module
    };
    ```

1. 添加 Python 加载模块时要调用的方法，该方法必须命名为 `PyInit_<module-name>`，其中 \<module-name> 与 C++ 项目的“常规” > “目标名称”属性完全匹配 。 也就是说，它与项目生成的 .pyd 的文件名相匹配。

    ```cpp
    PyMODINIT_FUNC PyInit_superfastcode() {
        return PyModule_Create(&superfastcode_module);
    }
    ```

1. 再次生成 C++ 项目来验证代码。 如果遇到错误，请参阅 ["故障排除"](#troubleshoot-compiling-failures) 部分。

### <a name="use-pybind11"></a>使用 PyBind11

如果你已完成上一部分中的步骤，则可能已注意到，你使用了大量样板代码来为 c + + 代码创建必要的模块结构。 PyBind11 可通过 c + + 头文件中的宏简化此过程，该文件可实现相同的结果，但代码更少。 

有关本部分中的代码的详细信息，请参阅 [PyBind11 基础知识](https://github.com/pybind/pybind11/blob/master/docs/basics.rst)。

1. 使用 pip 安装 PyBind11：`pip install pybind11` 或 `py -m pip install pybind11`。 

   或者，也可以使用“Python 环境”窗口安装 PyBind11，然后使用“在 Powershell 中打开”命令执行下一步。

1. 在同一终端中，运行 `python -m pybind11 --includes` 或 `py -m pybind11 --includes`。 

   此操作将打印路径列表，你应将这些路径添加到项目的 **c/c + +**"  >  **常规**  >  **附加包含目录**" 属性中。 请确保删除 `-I` 前缀（若有）。

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

1. 生成 C++ 项目来验证代码。 如果遇到错误，请在下一部分“关于编译失败的疑难解答”中查看解决方案。

### <a name="troubleshoot-compiling-failures"></a>关于编译失败的疑难解答

C++ 模块可能无法编译的原因如下：

- 错误：找不到 Python（E1696：无法打开源文件“Python .h”和/或 C1083：无法打开 Include 文件：“Python .h”：没有此文件或目录 ） 

  解决方案：验证 "项目属性" 中的 "路径 **c/c + +**  >  **常规**  >  **附加包含目录**" 是否指向 Python 安装的 *包含* 文件夹。 请参阅[创建核心 C++ 项目](#create-the-core-c-projects)中的步骤 6。

- 错误：无法找到 Python 库 
 
   解决方案：验证 "项目属性" 中的路径：**链接器**  >  **常规**  >  **附加库目录** 是否指向 Python 安装的库文件夹。 请参阅[创建核心 C++ 项目](#create-the-core-c-projects)中的步骤 6。

- 与目标体系结构相关的链接器错误
   
   解决方案：更改 C++ 目标的项目体系结构以匹配 Python 安装的项目体系结构。 例如，如果将 C++ 项目的目标定为 Win32，但是 Python 安装是 64 位，则将 C++ 项目更改为 x64。

## <a name="test-the-code-and-compare-the-results"></a>测试代码和比较结果

将 DLL 结构化为 Python 扩展后，便可从 Python 项目引用它们，导入模块，并使用其方法。

### <a name="make-the-dll-available-to-python"></a>使 DLL 可供 Python 使用

可以通过多种方式使 DLL 可供 Python 使用。 请考虑以下两种方法： 

* 如果 Python 项目和 C++ 项目在相同的解决方案中，则使用第一种方法。 请执行以下操作： 

   1. 在“解决方案资源管理器”中，右键单击 Python 项目中的“引用”节点，然后选择“添加引用”。 
   1. 在随即出现的对话框中，选择“项目”选项卡，同时选择“superfastcode”和“superfastcode2”项目，然后选择“确定”。

      ![显示如何添加对“superfastcode”项目的引用的屏幕截图。](media/cpp-add-reference.png)

* 另一种方法是在 Python 环境中安装模块，使该模块也可供其他 Python 项目使用。 有关详细信息，请参阅 [setuptools 项目文档](https://setuptools.readthedocs.io/)。 请执行以下操作：

    1. 右键单击 C++ 项目，然后选择“添加” > “新建项”，在项目中创建名为 setup.py 的文件。 
    
    1. 选择“C++ 文件 (.cpp)”，将文件命名为“setup.py”，然后选择“确定”。
    
       尽管使用了 C++ 文件模板，但使用 .py 扩展名来命名文件可让 Visual Studio 将其识别为 Python 文件。 

       编辑器中出现该文件时，以适合扩展方法的形式将以下代码粘贴到其中：
    
        对于 `CPython` 扩展（superfastcode 项目）：
    
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
    
        对于 `PyBind11`（superfastcode2 项目）：
    
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
    
    1. 在 C++ 项目中创建另一个名为 pyproject.toml 的文件，然后将以下代码粘贴到其中：
    
        ```toml
        [build-system]
        requires = ["setuptools", "wheel", "pybind11"]
        build-backend = "setuptools.build_meta"
        ```
    
    1. 若要生成扩展，请右键单击“打开 pyproject.toml”选项卡，然后选择“复制完整路径”。 使用该路径之前，需要从中删除 pyproject.toml 名称。
    
    1. 在“解决方案资源管理器”中，右键单击当前活动的 Python 环境，然后选择“管理 Python 包” 。
    
        > [!Tip]
        > 如果已经安装了包，则会看到它在此处列出。 继续下一步之前，单击“X”将其卸载。
    
    1. 在搜索框中，粘贴复制的路径，从末尾删除 *pyproject* ，然后按 **Enter** 从该目录中安装该模块。
    
        > [!Tip]
        > 如果安装由于权限错误而失败，请将 --user 添加到末尾处，然后重试该命令。


### <a name="call-the-dll-from-python"></a>从 Python 调用 DLL

如上一节所述，使 DLL 可用于 Python 之后，可以从 Python 代码中调用 `superfastcode.fast_tanh` 和 `superfastcode2.fast_tanh2` 函数，并将它们的性能与 Python 实现进行比较。 若要调用 DLL，请执行以下操作：

1. 在 .py 文件中添加以下行，调用从 DLL 中导出的方法并显示其输出：

    ```python
    from superfastcode import fast_tanh
    test(lambda d: [fast_tanh(x) for x in d], '[fast_tanh(x) for x in d] (CPython C++ extension)')

    from superfastcode2 import fast_tanh2
    test(lambda d: [fast_tanh2(x) for x in d], '[fast_tanh2(x) for x in d] (PyBind11 C++ extension)')
    ```

1. 若要运行 Python 程序，请选择“调试” > “启动而不调试”，或按 Ctrl + F5 。

    > [!NOTE]
    > 如果已禁用“启动但不调试”命令，请右键单击“解决方案资源管理器”中的 Python 项目，选择“设为启动项目”。  

    请注意，C++ 例程的运行速度大约比 Python 实现快 5 到 20 倍。 典型输出形式如下：

    ```output
    Running benchmarks with COUNT = 500000
    [tanh(x) for x in d] (Python implementation) took 0.758 seconds

    [fast_tanh(x) for x in d] (CPython C++ extension) took 0.076 seconds

    [fast_tanh2(x) for x in d] (PyBind11 C++ extension) took 0.204 seconds
    ```

1. 尝试增加 `COUNT` 变量，让差异变得更明显。 

    C++ 模块调试版本的运行速度慢于发布版本的运行速度，因为调试版本优化程度较低，并包含各种错误检查 。 可以随意在这些配置之间进行切换，以便进行比较，但请务必返回并更新你之前为“发布”配置设置的属性。

在输出中，你可能会看到 PyBind11 扩展的速度不如 CPython 扩展快，尽管它应比纯 Python 实现更快。 这主要是因为使用了 `METH_O` 调用，它不支持多个参数、参数名称或关键字参数。 PyBind11 会生成稍微复杂一些的代码，以便为调用方提供更类似于 Python 的接口。 但是因为测试代码调用该函数 500,000 次，结果可能会大大增加开销！

可以通过将 `for` 循环到本机代码中来进一步减少开销。 此方法涉及使用[函数参数的](https://docs.python.org/c-api/iter.html) (或 PyBind11 类型) `py::iterable` 处理每个元素。 [](https://pybind11.readthedocs.io/en/stable/advanced/functions.html#python-objects-as-args) 删除 Python 和 C++ 之间的重复转换是缩短处理序列所需时间的有效方法。

### <a name="troubleshoot-importing-errors"></a>关于导入错误的疑难解答

如果在尝试导入模块时收到一条 `ImportError` 消息，可以通过以下方式之一来解决此问题：

* 当通过项目引用进行生成时，请确保 C++ 项目属性与为 Python 项目激活的 Python 环境匹配，特别是 Include 和 Library 目录 。

* 请确保输出文件的名称为 superfastcode.pyd。 任何其他文件名或扩展名都会阻止它的导入。

* 如果通过使用 setup.py 文件安装了模块，请进行检查以确保在为 Python 项目激活的 Python 环境中运行了 pip 命令。 在“解决方案资源管理器”中扩展 Python 环境应显示 superfastcode 的条目。

## <a name="debug-the-c-code"></a>调试 C++ 代码

Visual Studio 支持一起调试 Python 和 C++ 代码。 本部分采用 superfastcode 项目介绍了此过程。 Superfastcode2 项目的过程是相同的。

1. 在“解决方案资源管理器”中，右键单击 Python 项目，依次选择“属性”、“调试”选项卡，然后选择“调试” > “启用本机代码调试”选项。

    > [!Tip]
    > 启用本机代码调试后，Python 输出窗口可能在程序完成后立即关闭，且不会出现通常的“按任何键以继续”暂停界面。 
    >
    > 解决方案：若要在启用本机代码调试后强制暂停，请向"调试"选项卡上的"运行解释器 `-i`   >  **参数**"**字段添加** 选项。此参数在代码运行后将 Python 解释器置于交互模式，此时它将等待你选择 Ctrl+Z，然后按 Enter 关闭窗口。 
    >
    > 或者，如果不介意修改 Python 代码，则可在程序结束时添加 `import os` 和 `os.system("pause")` 语句。 此代码会复制初始的暂停提示符。

1. 选择“文件” > “保存”以保存属性更改。

1. 在 Visual Studio 工具栏上，将生成配置设置为“调试”。

    ![Visual Studio 工具栏上的“调试”设置的屏幕截图。](media/cpp-set-debug.png)

1. 由于代码在调试器中运行时通常需要更长时间，可能需要将 .py 文件中的 `COUNT` 变量更改为比默认值小五倍的值。 例如，将该值从 500000 更改为 100000 。

1. 在 C++ 代码中，在 `tanh_impl` 方法内的第一行设置一个断点，然后启动调试器（按 F5 或选择“调试” > “开始调试”）。 

    调用该断点代码时，调试器将会停止。 如果未命中断点，请进行检查以确保配置设置为“调试”以及已保存项目（启动调试器时，不会自动执行该操作）。

    ![包含断点的 C++ 代码的屏幕截图。](media/cpp-debugging.png)

1. 在断点处，可单步执行 C++ 代码、检查变量等。 有关这些功能的详细信息，请参阅[同时调试 Python 和 C++](debugging-mixed-mode-c-cpp-python-in-visual-studio.md)。

## <a name="alternative-approaches"></a>替代方法

可以通过各种方式创建 Python 扩展，如下表所述。 本文介绍前两行，即 `CPython` 和 `PyBind11`。

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

可通过 [python-samples-vs-cpp-extension](https://github.com/Microsoft/python-sample-vs-cpp-extension)，在 GitHub 上获取本演练中的完整示例。

---
title: 如何使用适用于 C++ 的 Google Test
description: 使用 Google Test 在 Visual Studio 中创建 C++ 单元测试。
ms.date: 01/19/2022
ms-custom: devdivchpfy22
ms.topic: how-to
ms.author: corob
manager: markl
ms.workload:
- cplusplus
author: corob-msft
ms.openlocfilehash: 858eb1abc651b578a2320658b5b46c278ee2666b
ms.sourcegitcommit: edf8137cd90c67b6078a02c93094f7e1c3bf8930
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2022
ms.locfileid: "139550575"
---
# <a name="how-to-use-google-test-for-c-in-visual-studio"></a>如何在 Visual Studio 中使用适用于 C++ 的 Google Test

在 Visual Studio 2017 及更高版本中，Google Test 作为“使用 C++ 的桌面开发”工作负载的默认组件集成到 Visual Studio IDE 中。 若要验证是否已在计算机上安装，请打开 Visual Studio 安装程序。 在工作负荷组件列表下查找 Google Test：

![安装 Google Test](media/vs-2022/cpp-google-component.png)

::: moniker range=">=vs-2022"

## <a name="add-a-google-test-project-in-visual-studio-2022"></a>在 Visual Studio 2022 中添加 Google Test 项目

1. 在“解决方案资源管理器”中，右键单击解决方案节点，然后选择“添加”>“新建项目”  。
2. 将“语言”设置为“C++”并在搜索框中键入“测试”。 从结果列表中，选择“Google Test 项目”。
3. 为测试项目指定一个名称，然后选择 **"确定"**。

![新建 Google Test 项目](media/vs-2022/cpp-gtest-new-project.png)

::: moniker-end

::: moniker range="vs-2019"

## <a name="add-a-google-test-project-in-visual-studio-2019"></a>在 Visual Studio 2019 中添加 Google Test 项目

1. 在“解决方案资源管理器”中，右键单击解决方案节点，然后选择“添加”>“新建项目”  。
2. 将“语言”设置为“C++”并在搜索框中键入“测试”。 从结果列表中，选择“Google Test 项目”。
3. 为测试项目指定一个名称，然后选择 **"确定"**。

![新建 Google Test 项目](media/vs-2019/cpp-gtest-new-project-vs2019.png)

::: moniker-end

::: moniker range="vs-2017"

## <a name="add-a-google-test-project-in-visual-studio-2017"></a>在 Visual Studio 2017 中添加 Google Test 项目

1. 在“解决方案资源管理器”中，右键单击解决方案节点，然后选择“添加”>“新建项目”  。
2. 在左窗格中，依次选择“Visual C++”“测试”，然后在中心窗格中选择“Google Test 项目” > 。
3. 为测试项目指定一个名称，然后选择 **"确定"**。

![新建 Google Test 项目](media/cpp-gtest-new-project.png)

::: moniker-end

## <a name="configure-the-test-project"></a>配置测试项目

在显示的 "**测试 Project 配置**" 对话框中，可以选择要测试的项目。 选择一个项目时，Visual Studio 会添加对所选项目的引用。 如果你不选择任何项目，则需要手动添加对要测试的项目的引用。 在 Google Test 二进制文件的静态和动态链接之间进行选择时，注意事项与任何 C++ 程序相同。 有关详细信息，请参阅 [Visual C++ 中的 DLL](/cpp/build/dlls-in-visual-cpp)。

![配置 Google Test 项目](media/vs-2022/cpp-gtest-config.png)

## <a name="set-additional-options"></a>设置附加选项

从主菜单中，选择“工具” > “选项” > “Google Test 测试适配器”以设置附加选项  。 有关这些设置的详细信息，请参阅 Google Test 文档。

![Google Test 项目设置](media/vs-2022/cpp-gtest-settings.png)

## <a name="add-include-directives"></a>添加 include 指令

在测试 .cpp 文件中，添加任何所需的 `#include` 指令以使程序的类型和函数对测试代码可见。 通常，程序在文件夹层次结构中的上一层。 如果键入 `#include "../"` ，则将弹出一个 IntelliSense 窗口，并使你能够选择头文件的完整路径。

![添加 #include 指令](media/cpp-gtest-includes.png)

## <a name="write-and-run-tests"></a>编写和运行测试

现在，你可以编写和运行 Google 测试了。 有关测试宏的信息，请参阅 [Google Test 入门](https://github.com/google/googletest/blob/master/docs/primer.md)。 有关使用 **测试资源管理器** 发现、运行和对测试进行分组的信息，请参阅 [使用测试资源管理器运行单元测试](run-unit-tests-with-test-explorer.md)。

## <a name="see-also"></a>请参阅

[编写适用于 C/C++ 的单元测试](writing-unit-tests-for-c-cpp.md)

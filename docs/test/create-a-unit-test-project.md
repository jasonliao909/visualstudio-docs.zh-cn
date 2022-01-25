---
title: 创建单元测试项目
description: 了解如何创建单元测试项目。 测试项目可以与成品代码位于同一解决方案中，也可以位于单独的解决方案中。
ms.custom: SEO-VS-2020, devdivchpfy22
ms.date: 01/13/2022
ms.topic: how-to
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-test
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: 71f0a341c3ddd544fbf795755db4e3e52b380816
ms.sourcegitcommit: f81a8f381bcdbac96d112f815737ba1df55d97a3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2022
ms.locfileid: "137667403"
---
# <a name="create-a-unit-test-project"></a>创建单元测试项目

单元测试往往反映被测代码的结构。 例如，系统会为项目中的每个代码项目创建一个单元测试项目。 测试项目可以与成品代码位于同一解决方案中，也可以位于单独的解决方案中。 解决方案中可以有多个单元测试项目。

> [!NOTE]
> 本机代码的单元测试位置和测试项目结构可能不同于本文中所述的结构。 有关详细信息，请参阅[编写 C/C++ 单元测试](writing-unit-tests-for-c-cpp.md)。

## <a name="to-create-a-unit-test-project"></a>创建单元测试项目

1. 在"**文件"** 菜单上 **，选择"** 新建  >  Project"，**或** 按 **Ctrl** + **Shift** + **N**。

::: moniker range="vs-2017"

2. 在“新建项目”对话框中，展开“已安装”节点，选择要用于测试项目的语言，然后选择“测试”  。

3. 选择要使用的测试框架的项目模板，例如“MSTest 测试项目”或“NUnit 测试项目”。 为项目命名，然后选择“确定”。

   ![Visual Studio 2017 中的测试项目模板](media/test-project-templates.png)

::: moniker-end

::: moniker range=">=vs-2019"

2. 在“创建新项目”页上，在搜索框中键入“单元测试”。 为想要使用的测试框架选择项目模板，例如 **"MSTest** Test Project 或 **NUnit Test Project"，** 然后选择"下一 **步"。**

   ![Visual Studio 2019 中的测试项目模板](media/vs-2019/test-project-templates.png)

3. 在"**配置新项目"页上**，输入项目的名称，然后选择"创建 **"。**

::: moniker-end

4. 在单元测试项目中，添加对被测代码的引用。 要添加对相同解决方案中代码项目的引用，请执行以下操作：

   1. 在解决方案资源管理器中选择测试项目。

   2. 在“项目”菜单中，选择“添加引用”。

   3. 在“引用管理器”中，选择“项目”下的“解决方案”节点。 选择要测试的代码项目，然后选择“确定”。

   如果要测试的代码位于其他位置，请参阅[管理项目中的引用](../ide/managing-references-in-a-project.md)了解有关添加引用的信息。

## <a name="next-steps"></a>后续步骤

请参阅以下部分之一：

**编写单元测试**

- [单元测试代码](../test/unit-test-your-code.md)

- [编写 C/C++ 单元测试](writing-unit-tests-for-c-cpp.md)

- [在单元测试中使用 MSTest 框架](using-microsoft-visualstudio-testtools-unittesting-members-in-unit-tests.md)

**运行单元测试**

- [使用测试资源管理器运行单元测试](../test/run-unit-tests-with-test-explorer.md)
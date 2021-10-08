---
title: 项目和解决方案简介
description: 了解 Visual Studio 中的项目和解决方案之间的区别，以及如何使用它们。
ms.date: 09/14/2021
ms.technology: vs-ide-general
ms.custom:
- vs-acquisition
- get-started
- SEO-VS-2020
ms.topic: tutorial
f1_keywords:
- project.addnewitem
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: db3eea7017645d51065ed62e038c3323125e7b71
ms.sourcegitcommit: 8e74969ff61b609c89b3139434dff5a742c18ff4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2021
ms.locfileid: "128432030"
---
# <a name="introduction-to-projects-and-solutions"></a>项目和解决方案简介

在这篇介绍性的文章中，我们将探讨如何在 Visual Studio 中创建解决方案和项目 。 解决方案是一个容器，用于组织一个或多个相关的代码项目，例如，类库项目和对应的测试项目。

你将从头开始构建解决方案和项目，我们以此作为教学手段来帮助你理解项目的概念。 通常，你将使用 Visual Studio 项目模板来创建新项目。 你还将了解项目的属性及其包含的部分文件，并创建从一个项目到另一个项目的引用。

> [!NOTE]
> 在 Visual Studio 中开发应用不需要用到解决方案和项目。 你可直接打开包含代码的文件夹，然后便可开始进行编码、生成和调试。 例如，克隆的 [GitHub](https://github.com/) 存储库可能不包含 Visual Studio 项目和解决方案。 有关详细信息，请参阅[在 Visual Studio 中开发代码而无需创建项目或解决方案](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)。
::: moniker range="vs-2017"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)页免费安装。

::: moniker-end

::: moniker range="vs-2019"

如果尚未安装 Visual Studio 2019，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页免费安装。

::: moniker-end

::: moniker range=">=vs-2022"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页免费安装。

::: moniker-end

## <a name="solutions-and-projects"></a>解决方案和项目

在 Visual Studio 中，解决方案不是“答案”。 解决方案仅仅是 Visual Studio 用来组织一个或多个相关项目的容器。 打开某个解决方案时，Visual Studio 会自动加载该解决方案包含的所有项目。

### <a name="create-a-solution"></a>创建解决方案

首先创建一个空解决方案，以此来开始探索。 对 Visual Studio 有一定了解后，可能就不会经常创建空解决方案。 创建新项目时，Visual Studio 会自动为该项目创建一个解决方案，除非已经打开了一个解决方案。

::: moniker range="vs-2017"

1. 打开 Visual Studio。

1. 从顶部菜单栏中选择“文件”>“新建”>“项目”  。

   **“新建项目”** 对话框随即打开。

1. 在左侧窗格中，展开“其他项目类型”，然后选择“Visual Studio 解决方案” 。 在中间窗格中，选择“空白解决方案”模板。 将解决方案命名为“QuickSolution”，然后选择“确定”按钮 。

   ![显示在 Visual Studio 2017 中选择了“空白解决方案”模板的屏幕截图。](media/tutorial-projects-new-solution.png "Visual Studio 2017 中的空白解决方案模板。")

   此时“起始页”关闭，Visual Studio 窗口右侧的“解决方案资源管理器”中出现解决方案   。 你可能会经常使用“解决方案资源管理器”来浏览项目的内容  。

::: moniker-end

::: moniker range="vs-2019"

1. 打开 Visual Studio。

2. 在“开始”窗口中，选择“创建新项目”。

3. 在“创建新项目”页上，在搜索框中输入“空白解决方案”，选择“空白解决方案”模板，然后选择“下一步”   。

   ![显示在 Visual Studio 2019 中选择了“空白解决方案”模板的屏幕截图。](media/vs-2019/tutorial-projects-blank-solution-template.png "Visual Studio 2019 中的空白解决方案模板。")

    > [!TIP]
    > 如果你安装了多个工作负载，那么“空白解决方案”模板可能不会出现在搜索结果列表的顶部。 尝试滚动到列表的“基于你搜索的其他结果”部分。 它应该出现在那里。

4. 将解决方案命名为“QuickSolution”，然后选择“创建” 。

   解决方案将显示在 Visual Studio 窗口右侧的解决方案资源管理器中  。 你可能会经常使用“解决方案资源管理器”来浏览项目的内容  。

::: moniker-end

::: moniker range=">=vs-2022"

1. 打开 Visual Studio，然后在“开始”窗口上，选择“创建新项目”。

3. 在“创建新项目”页面上的搜索框中键入“空白解决方案”，选择“空白解决方案”模板，然后选择“下一步” 。

   :::image type="content" source="media/vs-2022/tutorial-projects-blank-solution-template.png" alt-text="显示在 Visual Studio 中选择了“空白解决方案”模板的屏幕截图。" border="false":::

    > [!TIP]
    > 如果你安装了多个工作负载，那么“空白解决方案”模板可能不会出现在搜索结果列表的顶部。 尝试滚动浏览“基于你搜索的其他结果”以查找模板。

4. 在“配置新项目”页面上，将解决方案命名为 QuickSolution，然后选择“创建”  。

   QuickSolution 解决方案随即出现在 Visual Studio 窗口右侧的“解决方案资源管理器”中 。 你将经常使用“解决方案资源管理器”来浏览项目的内容。

::: moniker-end

### <a name="add-a-project"></a>添加项目

现在，将你的第一个项目添加到解决方案。 先从空项目开始，添加所需的项。

::: moniker range="vs-2017"

1. 在“解决方案资源管理器”中的“解决方案 'QuickSolution'”的右键菜单或上下文菜单中，依次选择“添加”>“新建项目”   。

   此时会打开 **“添加新项目”** 对话框。

1. 在左侧窗格中，展开“Visual C#”，然后选择“Windows 桌面” 。 然后在中间窗格中，选择“空项目 (.NET Framework)”模板。 将项目命名为“QuickDate”，然后选择“确定” 。

   随后名为“QuickDate”的项目出现在“解决方案资源管理器”中的解决方案下  。 目前它包含一个名为“App.config”的文件  。

   > [!NOTE]
   > 如果在对话框的左侧窗格中看不到“Visual C#”，则需安装 .NET 桌面开发 Visual Studio 工作负载 。 Visual Studio 使用基于工作负载的安装旨在仅安装所执行的开发类型需要的组件。 一种安装新工作负载的简单方法是选择“添加新项目”对话框左下角的“打开 Visual Studio 安装程序”链接 。 在“Visual Studio 安装程序”启动后，选择“.NET 桌面开发”工作负载，再单击“修改”按钮 。
   >
   > ![显示“打开 Visual Studio 安装程序”链接的屏幕截图。](media/tutorial-projects-open-installer.png "Visual Studio 2017 中“添加新项目”对话框中的“打开 Visual Studio 安装程序”链接。")

::: moniker-end

::: moniker range="vs-2019"

1. 在“解决方案资源管理器”中的“解决方案 'QuickSolution'”的右键菜单或上下文菜单中，依次选择“添加”>“新建项目”   。

   随即打开显示“添加新项目”的对话框  。

1. 在顶部的搜索框中输入文本“空”，然后在“语言”下选择“C#”。

1. 然后选择“空项目 (.NET Framework)”模板并选择“下一步” 。

1. 将项目命名为“QuickDate”，然后选择“创建” 。

   随后名为“QuickDate”的项目出现在“解决方案资源管理器”中的解决方案下  。 目前它包含一个名为“App.config”的文件  。

   > [!NOTE]
   > 如果没有看到“空项目(.NET Framework)”模板，则需要安装 .NET 桌面开发 Visual Studio 工作负载 。 Visual Studio 使用基于工作负载的安装旨在仅安装所执行的开发类型需要的组件。
   >
   >在创建新项目时安装新工作负载的简便方法是，在显示“未找到你要查找的内容”的文本下选择“安装更多工具和功能”链接 。 在“Visual Studio 安装程序”启动后，选择“.NET 桌面开发”工作负载，再单击“修改”按钮 。
   >
   > ![显示“打开 Visual Studio 安装程序”链接的屏幕截图。](media/vs-2019/tutorial-projects-open-installer.png "Visual Studio 中“新建项目”对话框中的“打开 Visual Studio 安装程序”链接。")

::: moniker-end

::: moniker range=">=vs-2022"

1. 在“解决方案资源管理器”中右键单击 QuickSolution 解决方案，然后从上下文菜单中选择“添加”>“新项目”   。

1. 在“添加新项目”页面顶部的搜索框中键入“空”，然后在“所有语言”下选择“C#” 。

1. 选择 C#“空项目(.NET Framework)”模板，然后选择“下一步” 。

   > [!NOTE]
   > Visual Studio 使用基于工作负载的安装旨在仅安装所执行的开发类型需要的组件。 如果没有看到“空项目(.NET Framework)”模板，则需要安装“.NET 桌面开发”Visual Studio 工作负载 。
   >
   >在创建新项目时安装新工作负载的简便方法是，在显示“未找到你要查找的内容”的文本下选择“安装更多工具和功能”链接 。 在 Visual Studio 安装程序中，选择“.NET 桌面开发”工作负载，然后选择“修改” 。
   >
   > :::image type="content" source="media/vs-2022/tutorial-projects-open-installer.png" alt-text="显示“打开 Visual Studio 安装程序”链接的屏幕截图。" border="false":::

1. 在“配置新项目”页面中，将项目命名为 QuickDate，然后选择“创建”  。

   QuickDate 项目随即出现在“解决方案资源管理器”中的解决方案下 。 目前，该项目包含一个名为 App.config 的文件。

::: moniker-end

## <a name="add-an-item-to-the-project"></a>向项目添加一个项

将代码文件添加到你的空项目。

1. 在“解决方案资源管理器”中的“QuickDate”项目的右键菜单或上下文菜单中，依次选择“添加” > “新建项”   。

   此时将打开“添加新项”对话框。

1. 展开“Visual C# 项”，然后选择“代码” 。 在中间窗格中，选择“类”项模板。 在“名称”下，键入 Calendar，然后选择“添加”。

   Visual Studio 随即将名为 Calendar.cs 的文件添加到项目。 末尾的 .cs 是 C# 代码文件的文件扩展名。 Calendar.cs 文件出现在“解决方案资源管理器”的直观项目层次结构中，文件在编辑器中打开 。

1. 将 Calendar.cs 文件的内容替换为以下代码：

   ```csharp
   using System;

   namespace QuickDate
   {
       internal class Calendar
       {
           static void Main(string[] args)
           {
               DateTime now = GetCurrentDate();
               Console.WriteLine($"Today's date is {now}");
               Console.ReadLine();
           }

           internal static DateTime GetCurrentDate()
           {
               return DateTime.Now.Date;
           }
       }
   }
   ```

   你还不需要了解代码执行的所有操作。 按 Ctrl+F5 运行应用，查看应用是否将今天的日期输出到控制台（标准输出）窗口 。

## <a name="add-a-second-project"></a>添加第二个项目

解决方案通常包含多个项目，这些项目通常相互引用。 解决方案中的一些项目可能是类库，一些可能是可执行应用程序，一些可能是单元测试项目或网站。

要将单元测试项目添加到解决方案，请从项目模板开始，这样就无需将其他代码文件添加到项目。

::: moniker range="vs-2017"

1. 在“解决方案资源管理器”中的“解决方案 'QuickSolution'”的右键菜单或上下文菜单中，依次选择“添加”>“新建项目”   。

2. 在左侧窗格中，展开 Visual C#，然后选择“测试”类别 。 在中间窗格中，选择“MSTest 测试项目(.NET Core)”项目模板。 将项目命名为“QuickTest”，然后选择“确定” 。

   第二个项目已添加到“解决方案资源管理器”，且编辑器中打开了名为 UnitTest1.cs 的文件。

   ![显示包含两个项目的解决方案资源管理器的屏幕截图。](media/tutorial-projects-solution-explorer.png "Visual Studio 2017 中包含两个项目的解决方案资源管理器”。")

::: moniker-end

::: moniker range="vs-2019"

1. 在“解决方案资源管理器”中的“解决方案 'QuickSolution'”的右键菜单或上下文菜单中，依次选择“添加”>“新建项目”   。

2. 在“添加新项目”对话框中，在顶部的搜索框输入文本“单元测试”，然后在“语言”下选择“C#”。

3. 对 .NET Core 选择“单元测试项目”项目模板，然后选择“下一步” 。

   > [!NOTE]
   > 从 Visual Studio 2019 版本 16.9 开始，MSTest 项目模板名称已从“MSTest 单元测试项目(.NET Core)”更改为“单元测试项目”。 在此更新中更改了项目创建过程中的几个步骤。

4. 将项目命名为“QuickTest”，然后选择“下一步” 。

5. 选择建议的目标框架 (.NET Core 3.1) 或 .NET 5，然后选择“创建”。

   第二个项目已添加到“解决方案资源管理器”，且编辑器中打开了名为 UnitTest1.cs 的文件。

   ![显示包含两个项目的解决方案资源管理器的屏幕截图。](media/vs-2019/tutorial-projects-solution-explorer.png "Visual Studio 中包含两个项目的解决方案资源管理器”。")

::: moniker-end

::: moniker range=">=vs-2022"

1. 在“解决方案资源管理器”中的“解决方案 'QuickSolution'”的右键菜单或上下文菜单中，依次选择“添加”>“新建项目”   。

1. 在“添加新项目”对话框顶部的搜索框中键入“单元测试”，然后在“语言”下选择“C#” 。

1. 选择 C#“单元测试项目(.NET Framework)”项目模板，然后选择“下一步” 。

1. 在“配置新项目”页面中，将项目命名为 QuickTest，然后选择“创建”。

   Visual Studio 随即将 QuickTest 项目添加到“解决方案资源管理器”，并在编辑器中打开 UnitTest1.cs 文件  。

   :::image type="content" source="media/vs-2022/tutorial-projects-solution-explorer.png" alt-text="显示包含两个项目的解决方案资源管理器的屏幕截图。" border="false":::

::: moniker-end

## <a name="add-a-project-reference"></a>添加项目引用

你将使用新的单元测试项目测试 QuickDate 项目中的方法，因此需要将对 QuickDate 的引用添加到 QuickTest 项目  。 添加引用会在两个项目之间创建生成依赖关系，这意味着生成解决方案时，会先生成 QuickDate，再生成 QuickTest 。

::: moniker range="vs-2017"

1. 选择“QuickTest”项目中的“依赖关系”节点，然后在右键菜单或上下文菜单中选择“添加引用”  。

   打开“引用管理器”对话框。

1. 在左侧窗格中，展开“项目”，选择“解决方案” 。 在中间窗格中，选择“QuickDate”旁的复选框，然后选择“确定” 。

   已添加对“QuickDate”项目的引用。

   ![Visual Studio 中显示项目引用的解决方案资源管理器的屏幕截图。](media/vs-2019/tutorial-projects-solution-explorer-reference.png "Visual Studio 中显示项目引用的解决方案资源管理器的屏幕截图。")

::: moniker-end

::: moniker range="vs-2019"

1. 选择 QuickTest 项目中的“依赖项”节点，然后在右键菜单或上下文菜单中选择“添加项目引用”  。

   打开“引用管理器”对话框。

1. 在左侧窗格中，展开“项目”，然后选择“解决方案” 。 在中间窗格中，选择“QuickDate”旁的复选框，然后选择“确定” 。

   已添加对“QuickDate”项目的引用。

   ![Visual Studio 2019 中显示项目引用的解决方案资源管理器的屏幕截图。](media/vs-2019/tutorial-projects-solution-explorer-reference.png)

::: moniker-end

::: moniker range=">=vs-2022"

1. 在“解决方案资源管理器”中，右键单击 QuickTest 项目的“引用”节点，然后从上下文菜单中选择“添加引用”   。

1. 在“引用管理器”对话框中的“项目”下，选中 QuickDate 旁边的复选框，然后选择“确定”   。

   对 QuickDate 项目的引用随即出现在“解决方案资源管理器”中的 QuickTest 项目下  。

   :::image type="content" source="media/vs-2022/tutorial-projects-solution-explorer-reference.png" alt-text="显示项目引用的解决方案资源管理器的屏幕截图。" border="false":::

::: moniker-end

## <a name="add-test-code"></a>添加测试代码

1. 现在，将测试代码添加到 C# 测试代码文件。 将 *UnitTest1.cs* 的内容替换为以下代码：

   ```csharp
   using System;
   using Microsoft.VisualStudio.TestTools.UnitTesting;

   namespace QuickTest
   {
       [TestClass]
       public class UnitTest1
       {
           [TestMethod]
           public void TestGetCurrentDate()
           {
               Assert.AreEqual(DateTime.Now.Date, QuickDate.Calendar.GetCurrentDate());
           }
       }
   }
   ```

   一些代码下方会出现红色波浪线。 你可以通过将测试项目设为 QuickDate 项目的[友元程序集](/dotnet/standard/assembly/friend-assemblies)来解决此错误。

1. 在 Calendar.cs 文件中，将以下 [using 语句](/dotnet/csharp/language-reference/keywords/using-statement)和 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 属性添加到文件顶部，以解决测试项目中的错误。

   ```csharp
   using System.Runtime.CompilerServices;

   [assembly: InternalsVisibleTo("QuickTest")]
   ```

   Calendar.cs 代码应类似于如下屏幕截图：

   ::: moniker range="<=vs-2019"

   ![显示 C# 代码的屏幕截图。](media/tutorial-projects-cs-code.png)

   ::: moniker-end

   ::: moniker range=">=vs-2022"

   :::image type="content" source="media/vs-2022/tutorial-projects-cs-code.png" alt-text="显示 C# 代码的屏幕截图。" border="false":::

   ::: moniker-end

### <a name="run-the-unit-test"></a>运行单元测试

::: moniker range="vs-2017"

若希望检查单元测试是否正常工作，请从菜单栏依次选择“测试” > “运行” > “所有测试”  。 此时名为“测试资源管理器”的窗口打开，你应该会看到“TestGetCurrentDate”测试通过。

::: moniker-end

::: moniker range=">=vs-2019"

要检查单元测试是否正常工作，请从菜单栏中依次选择“测试” > “运行所有测试” 。 “测试资源管理器”窗口随即打开，你应该会看到 TestGetCurrentDate 测试通过 。

::: moniker-end

::: moniker range="<=vs-2019"

![显示具有通过测试的测试资源管理器的屏幕截图。](media/tutorial-projects-test-explorer.png)

::: moniker-end

::: moniker range=">=vs-2022"

:::image type="content" source="media/vs-2022/tutorial-projects-test-explorer.png" alt-text="显示具有通过测试的测试资源管理器的屏幕截图。" border="false":::

::: moniker-end

::: moniker range="vs-2017"

> [!TIP]
> 如果“测试资源管理器”未自动打开，请从菜单中选择“测试” > “Windows” > “测试资源管理器”。

::: moniker-end

::: moniker range=">=vs-2019"

> [!TIP]
> 如果“测试资源管理器”未自动打开，请从菜单栏中选择“测试” > “测试资源管理器”将其打开  。

::: moniker-end

## <a name="project-properties"></a>项目属性

包含 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 属性的 Calendar.cs 文件中的行引用 QuickTest 项目的程序集名称或文件名。 程序集名称可能不会始终与项目名称相同。 要查找项目的程序集名称，请使用项目属性。 属性页包含项目的各种设置。

1. 在“解决方案资源管理器”中，右键单击 QuickTest 项目，然后选择“属性”，或者选择该项目，然后按 Alt+Enter    。

   项目的属性页打开到“应用程序”选项卡。QuickTest 项目的程序集名称确实是 QuickTest  。

   如果需要，可以在此处更改该名称。 随后，在生成测试项目时，生成的二进制文件的名称将从 QuickTest.dll 更改为 \<NewName>.dll 。

    ::: moniker range="<=vs-2019"

    ![显示项目属性的屏幕截图。](media/tutorial-projects-netcore-properties.png)

    ::: moniker-end

    ::: moniker range=">=vs-2022"

    :::image type="content" source="media/vs-2022/tutorial-project-properties.png" alt-text="显示项目属性的屏幕截图。" border="false":::

    ::: moniker-end

1. 了解项目属性页的其他选项卡，例如“生成”和“调试”。 这些选项卡对不同类型的项目是不同的。

## <a name="see-also"></a>另请参阅

- [使用项目和解决方案](../ide/creating-solutions-and-projects.md)
- [管理项目和解决方案属性](../ide/managing-project-and-solution-properties.md)
- [管理项目中的引用](../ide/managing-references-in-a-project.md)
- [在 Visual Studio 中开发代码而无需创建项目或解决方案](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)
- [Visual Studio IDE 概述](../get-started/visual-studio-ide.md)

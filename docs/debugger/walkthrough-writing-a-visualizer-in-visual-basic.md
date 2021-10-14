---
title: 用 Visual Basic 编写可视化工具 | Microsoft Docs
description: 按照演练进行操作，使用 Visual Basic 创建简单的可视化工具。 还可以创建测试工具来测试可视化工具。
ms.date: 05/27/2020
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- visualizers, writing
- walkthroughs [Visual Studio], visualizers
ms.assetid: c93bf5a1-3e5e-422f-894e-bd72c9bc1b57
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 31ccdc8b832e8203dd1e7ad8606f1869dccc00a6
ms.sourcegitcommit: 8fae163333e22a673fd119e1d2da8a1ebfe0e51a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2021
ms.locfileid: "129968145"
---
# <a name="walkthrough-writing-a-visualizer-in-visual-basic"></a>演练：用 Visual Basic 编写可视化工具

本演练演示如何使用 [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] 编写简单的可视化工具。 本演练中创建的可视化工具使用 Windows 窗体消息框显示字符串的内容。 此简单字符串可视化工具是一个基本示例，将演示如何创建更加适合您项目的其他数据类型的可视化工具。

> [!NOTE]
> 显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你的当前设置或版本。 若要更改设置，请转到“工具”菜单，然后选择“导入和导出” 。 有关详细信息，请参阅[重置设置](../ide/environment-settings.md#reset-settings)。

可视化工具代码必须放置在一个将由调试器读取的 DLL 中。 第一步是为此 DLL 创建一个类库项目。

## <a name="create-and-prepare-a-class-library-project"></a>创建和准备类库项目

### <a name="to-create-a-class-library-project"></a>创建类库项目

1. 创建一个新类库项目。

    ::: moniker range=">=vs-2019"
    按 Esc 关闭启动窗口。 键入 Ctrl + Q 打开搜索框，键入“visual basic”，选择“模板”，然后选择“创建新的类库(.NET Framework)”   。 在出现的对话框中，选择“创建”。
    ::: moniker-end
    ::: moniker range="vs-2017"
    从顶部菜单栏中选择“文件” > “新建” > “项目”。 在“新建项目”对话框的左窗格中，在“Visual Basic”下，选择“.NET Standard”，然后在中间窗格中选择“类库(.NET Standard)”   。
    ::: moniker-end

2. 为类库键入一个适当的名称，例如 `MyFirstVisualizer`，然后单击“创建”或“确定”。

   创建类库后，必须添加对 Microsoft.VisualStudio.DebuggerVisualizers.DLL 的引用，以便使用其中定义的类。 不过，首先要为您的项目赋予一个有意义的名称。

### <a name="to-rename-class1vb-and-add-microsoftvisualstudiodebuggervisualizers"></a>重命名 Class1.vb 并添加 Microsoft.VisualStudio.DebuggerVisualizers

1. 在“解决方案资源管理器”中，右键单击“Class1.vb”，然后在快捷菜单上单击“重命名”  。

2. 将名称从 Class1.vb 更改为有意义的名称，例如 DebuggerSide.vb。

   > [!NOTE]
   > [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 会自动更改 DebuggerSide.vb 中的类声明，以便与新文件名匹配。

3. 在“解决方案资源管理器”中，右键单击“My First Visualizer”，然后在快捷菜单上单击“添加引用”  。

4. 在“添加引用”对话框的“浏览”选项卡上，选择“浏览”并找到 Microsoft.VisualStudio.DebuggerVisualizers.DLL  。

    可以在 Visual Studio 安装目录的 \<Visual Studio Install Directory>\Common7\IDE\PublicAssemblies 子目录中找到该 DLL。

5. 单击 **“确定”** 。

6. 在 DebuggerSide.vb 中，将以下语句添加到 `Imports` 语句中：

   ```vb
   Imports Microsoft.VisualStudio.DebuggerVisualizers
   ```

## <a name="add-the-debugger-side-code"></a>添加调试器端代码
 现在已经准备好创建调试器端代码了。 这是运行在调试器中以显示要可视化的信息的代码。 首先，必须更改 `DebuggerSide` 对象的声明，以便它从基类 `DialogDebuggerVisualizer` 继承。

### <a name="to-inherit-from-dialogdebuggervisualizer"></a>从 DialogDebuggerVisualizer 继承

1. 在 DebuggerSide.vb 中，转到下面的代码行：

   ```vb
   Public Class DebuggerSide
   ```

2. 编辑代码，使它类似于以下内容：

   ```vb
   Public Class DebuggerSide
   Inherits DialogDebuggerVisualizer
   ```

   `DialogDebuggerVisualizer` 具有一个抽象方法 (`Show`)，必须重写此方法。

### <a name="to-override-the-dialogdebuggervisualizershow-method"></a>重写 DialogDebuggerVisualizer.Show 方法

- 在 `public class DebuggerSide` 中添加下面的方法：

  ```vb
  Protected Overrides Sub Show(ByVal windowService As Microsoft.VisualStudio.DebuggerVisualizers.IDialogVisualizerService, ByVal objectProvider As Microsoft.VisualStudio.DebuggerVisualizers.IVisualizerObjectProvider)

      End Sub
  ```

  `Show` 方法包含实际创建可视化工具对话框或其他用户界面的代码，并显示已从调试器传递到可视化工具的信息。 您必须添加创建该对话框并显示该信息的代码。 在本演练中，将使用 Windows 窗体消息框执行此操作。 首先，必须为 `Imports` 添加一个引用和 <xref:System.Windows.Forms> 语句。

### <a name="to-add-systemwindowsforms"></a>添加 System.Windows.Forms

1. 在“解决方案资源管理器”中，右键单击“引用”，然后在快捷菜单上单击“添加引用”  。

2. 在“添加引用”对话框的“浏览”选项卡上，选择“浏览”并找到 System.Windows.Forms.DLL  。

    可以在 C:\Windows\Microsoft.NET\Framework\v4.0.30319 中找到该 DLL。

3. 单击 **“确定”** 。

4. 在 DebuggerSide.cs 中，将下面的语句添加到 `Imports` 语句中：

    ```vb
    Imports System.Windows.Forms
    ```

## <a name="create-your-visualizers-user-interface"></a>创建您的可视化工具的用户界面
 现在，您将添加一些代码以创建和显示可视化工具的用户界面。 由于这是您的第一个可视化工具，因此您将保持用户界面简洁并使用消息框。

### <a name="to-show-the-visualizer-output-in-a-dialog-box"></a>在对话框中显示可视化工具输出

1. 在 `Show` 方法中，添加以下代码行：

    ```vb
    MessageBox.Show(objectProvider.GetObject().ToString())
    ```

     此代码示例中不包含错误处理。 但在实际的可视化工具或任何其他类型的应用程序中，应当包含错误处理。

2. 在“生成”菜单上，单击“生成 MyFirstVisualizer” 。 该项目应能成功生成。 在继续前更正所有生成错误。

## <a name="add-the-necessary-attribute"></a>添加必需特性
 这是调试器端代码的结尾部分。 但是还有一步操作：添加用于通知调试对象端哪些类集合构成可视化工具的特性。

### <a name="to-add-the-type-to-visualize-for-the-debuggee-side-code"></a>添加类型以可视化调试对象端代码

在调试器端代码中，使用 <xref:System.Diagnostics.DebuggerVisualizerAttribute> 属性来指定用于可视化调式对象的类型（对象源）。 `Target` 属性设置要可视化的类型。

1. 在 DebuggerSide.vb 中的 `Imports` 语句之后但在 `namespace MyFirstVisualizer` 之前，添加以下特性代码：

    ```vb
    <Assembly: System.Diagnostics.DebuggerVisualizer(GetType(MyFirstVisualizer.DebuggerSide), GetType(VisualizerObjectSource), Target:=GetType(System.String), Description:="My First Visualizer")>
    ```

2. 在“生成”菜单上，单击“生成 MyFirstVisualizer” 。 该项目应能成功生成。 在继续前更正所有生成错误。

## <a name="create-a-test-harness"></a>创建测试套
 这时，第一个可视化工具就完成了。 如果您已正确地按照每一步操作，您可以生成该可视化工具，并将其安装到 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中。 但在将可视化工具安装到 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中之前，应对其进行测试以确保它能够正常运行。 你现在将创建一个测试套以在没有将可视化工具安装到 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中的情况下运行它。

### <a name="to-add-a-test-method-to-show-the-visualizer"></a>添加测试方法以显示可视化工具

1. 将下面的方法添加到类 `public DebuggerSide`：

   ```vb
   Shared Public Sub TestShowVisualizer(ByVal objectToVisualize As Object)
       Dim visualizerHost As New VisualizerDevelopmentHost(objectToVisualize, GetType(DebuggerSide))
   visualizerHost.ShowVisualizer()
   End Sub
   ```

2. 在“生成”菜单上，单击“生成 MyFirstVisualizer” 。 该项目应能成功生成。 在继续前更正所有生成错误。

   然后，您必须创建一个可执行项目以调用可视化工具 DLL。 为简单起见，使用一个控制台应用程序项目。

### <a name="to-add-a-console-application-project-to-the-solution"></a>将控制台应用程序项目添加到解决方案中

1. 在“解决方案资源管理器”中，右键单击解决方案，选择“添加”，然后单击“新建项目”。

    ::: moniker range=">=vs-2019"
    在搜索框中键入“visual basic”，选择“模板”，然后选择“创建新的控制台应用(.NET Framework)”  。 在出现的对话框中，选择“创建”。
    ::: moniker-end
    ::: moniker range="vs-2017"
    从顶部菜单栏中选择“文件” > “新建” > “项目”。 在“新建项目”对话框的左窗格中，在“Visual Basic”下，选择“Windows 桌面”，然后在中间窗格中选择“控制台应用(.NET Framework)”   。
    ::: moniker-end

2. 为类库键入一个适当的名称，例如 `MyTestConsole`，然后单击“创建”或“确定”。

   现在，必须添加必要的引用，以便 MyTestConsole 能够调用 MyFirstVisualizer。

### <a name="to-add-necessary-references-to-mytestconsole"></a>添加对 MyTestConsole 的必需引用

1. 在“解决方案资源管理器”中右键单击“MyTestConsole”，然后在快捷菜单上单击“添加引用”  。

2. 在“添加引用”对话框的“浏览”选项卡上，单击“Microsoft.VisualStudio.DebuggerVisualizers” 。

3. 单击 **“确定”** 。

4. 右键单击“MyTestConsole”，然后单击“添加引用” 。

5. 在“添加引用”对话框中单击“项目”选项卡，然后选择“MyFirstVisualizer” 。

6. 单击 **“确定”** 。

## <a name="finish-your-test-harness-and-test-your-visualizer"></a>完成测试套并测试可视化工具
 现在，你将添加代码以完成测试套。

### <a name="to-add-code-to-mytestconsole"></a>将代码添加到 MyTestConsole

1. 在“解决方案资源管理器”中右键单击“Program.vb”，然后单击快捷菜单上的“重命名”  。

2. 将名称从 Module1.vb 更改为合适的名称，例如“TestConsole.vb”。

    请注意，[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 会自动更改 TestConsole.vb 中的类声明，使之与新文件名匹配。

3. 在 TestConsole. vb 中，添加以下 `Imports` 语句：

   ```vb
   Imports MyFirstVisualizer
   ```

4. 在方法 `Main` 中，添加以下代码：

   ```vb
   Dim myString As String = "Hello, World"
   DebuggerSide.TestShowVisualizer(myString)
   ```

   现在已准备好测试您的第一个可视化工具了。

### <a name="to-test-the-visualizer"></a>测试可视化工具

1. 在“解决方案资源管理器”中右键单击“MyTestConsole”，然后单击快捷菜单中的“设为启动项目”  。

2. 在“调试”菜单上，单击“启动” 。

    控制台应用程序启动。 此时将出现可视化工具，其中显示字符串“Hello, World”。

   祝贺您！ 你刚刚生成了第一个可视化工具并进行了测试。

   如果您想在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中使用可视化工具，而不是只从测试工具中调用它，则需要安装它。 有关详细信息，请参阅[如何：安装可视化工具](../debugger/how-to-install-a-visualizer.md)。

## <a name="see-also"></a>请参阅

- [可视化工具体系结构](../debugger/visualizer-architecture.md)
- [如何：安装可视化工具](../debugger/how-to-install-a-visualizer.md)
- [创建自定义可视化工具](../debugger/create-custom-visualizers-of-data.md)
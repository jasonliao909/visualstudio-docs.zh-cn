---
title: 使用 C# 编写可视化工具 | Microsoft Docs
description: 按照演练进行操作，使用 C# 创建简单的可视化工具。 它显示使用和不使用可视化工具项模板所需的步骤。
ms.custom: SEO-VS-2020
ms.date: 07/02/2021
ms.topic: conceptual
dev_langs:
- CSharp
helpviewer_keywords:
- visualizers, writing
- walkthroughs [Visual Studio], visualizers
ms.assetid: 53467461-8e0f-45ee-9bc4-374bbaeaf00f
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: a6ce1a6d9f2f8a36d892d484cf9353e1312758b4
ms.sourcegitcommit: 4e09130bcd55bb9cb8ad157507c23b67aa209fad
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/09/2021
ms.locfileid: "113549506"
---
# <a name="walkthrough-writing-a-visualizer-in-c"></a>演练：使用 C\# 编写可视化工具

本演练演示如何使用 C# 编写简单的可视化工具。 本演练中创建的可视化工具使用 Windows 窗体显示字符串的内容。 这种简单的字符串可视化工具本身并不是特别有用，但它显示了为其他数据类型创建更有用的可视化工具时必须遵循的基本步骤。

> [!NOTE]
> 显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你的当前设置或版本。 若要更改设置，请转到“工具”菜单，然后选择“导入和导出设置” 。 有关详细信息，请参阅[重置设置](../ide/environment-settings.md#reset-settings)。

可视化工具代码必须放置在一个将由调试器读取的 DLL 中。 因此，第一步是为此 DLL 创建一个类库项目。

## <a name="create-a-visualizer-manually"></a>手动创建可视化工具

请完成以下任务以创建可视化工具。

### <a name="to-create-a-class-library-project"></a>创建类库项目

* 创建一个新类库项目。

    ::: moniker range=">=vs-2019"
    依次选择“文件” > “新建” > “项目”    。 在“语言”下拉列表中，选择“C#”。 在“搜索”框中，键入“类库”，然后选择“类库(.NET Framework)” 。 单击“下一步”  。 在出现的对话框中，键入名称 `MyFirstVisualizer`，然后单击“创建”。

    对于可视化工具项目，请确保选择的是 .NET Framework 类库而不是 .NET。 虽然可视化工具需为 .NET Framework，但调用的应用可以是 .NET Core。
    ::: moniker-end
    ::: moniker range="vs-2017"
    从顶部菜单栏中选择“文件” > “新建” > “项目”。 在“新建项目”对话框的左窗格中，在“Visual C#”下，选择“.NET Framework”，然后在中间窗格中选择“类库(.NET Framework)”   。

    为类库键入一个适当的名称，例如 `MyFirstVisualizer`，然后单击“创建”或“确定”。
    ::: moniker-end

   创建类库后，必须添加对 Microsoft.VisualStudio.DebuggerVisualizers.DLL 的引用，以便使用其中定义的类。 但是，在添加引用之前，必须重命名某些类，使其名称有意义。

### <a name="to-rename-class1cs-and-add-microsoftvisualstudiodebuggervisualizers"></a>重命名 Class1.cs 并添加 Microsoft.VisualStudio.DebuggerVisualizers

1. 在“解决方案资源管理器”中，右键单击“Class1.cs”并选择快捷菜单上的“重命名” 。

2. 将名称从 Class1.cs 更改为有意义的名称，例如 DebuggerSide.cs。

   > [!NOTE]
   > [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 会自动更改 DebuggerSide.cs 中的类声明，以便与新文件名匹配。

3. 在“解决方案资源管理器”中，右键单击“引用”，然后在快捷菜单上选择“添加引用”  。

4. 在“添加引用”对话框的“浏览”选项卡上，选择“浏览”并找到 Microsoft.VisualStudio.DebuggerVisualizers.DLL  。

    可以在 Visual Studio 安装目录的 \<Visual Studio Install Directory>\Common7\IDE\PublicAssemblies 子目录中找到该 DLL。

5. 单击 **“确定”** 。

6. 在 DebuggerSide.cs 中，将以下内容添加到 `using` 指令中：

   ```csharp
   using Microsoft.VisualStudio.DebuggerVisualizers;
   ```

   现在已经准备好创建调试器端代码了。 这是运行在调试器中以显示要可视化的信息的代码。 首先，必须更改 `DebuggerSide` 对象的声明，以便从基类 `DialogDebuggerVisualizer` 继承。

### <a name="to-inherit-from-dialogdebuggervisualizer"></a>从 DialogDebuggerVisualizer 继承

1. 在 DebuggerSide.cs 中，转到下面的代码行：

   ```csharp
   public class DebuggerSide
   ```

2. 将代码更改为以下内容：

   ```csharp
   public class DebuggerSide : DialogDebuggerVisualizer
   ```

   `DialogDebuggerVisualizer` 具有一个抽象方法 (`Show`)，必须重写此方法。

#### <a name="to-override-the-dialogdebuggervisualizershow-method"></a>重写 DialogDebuggerVisualizer.Show 方法

- 在 `public class DebuggerSide` 中添加下面的方法：

  ```csharp
  protected override void Show(IDialogVisualizerService windowService, IVisualizerObjectProvider objectProvider)
  {
  }
  ```

  `Show` 方法包含实际创建可视化工具对话框或其他用户界面的代码，并显示已从调试器传递到可视化工具的信息。 您必须添加创建该对话框并显示该信息的代码。 在本演练中，将使用 Windows 窗体消息框执行此操作。 首先，必须为 System.Windows.Forms 添加引用和 `using` 指令。

### <a name="to-add-systemwindowsforms"></a>添加 System.Windows.Forms

1. 在“解决方案资源管理器”中，右键单击“引用”，然后在快捷菜单上选择“添加引用”  。

2. 在“添加引用”对话框的“浏览”选项卡上，选择“浏览”并找到 System.Windows.Forms.DLL  。

    可以在 C:\Windows\Microsoft.NET\Framework\v4.0.30319 中找到该 DLL。

3. 单击 **“确定”** 。

4. 在 DebuggerSide.cs 中，将以下内容添加到 `using` 指令中：

   ```csharp
   using System.Windows.Forms;
   ```

   现在，可添加一些代码以创建和显示可视化工具的用户界面。 由于这是你的第一个可视化工具，因此我们会保持用户界面简洁并使用消息框。

### <a name="to-show-the-visualizer-output-in-a-dialog-box"></a>在对话框中显示可视化工具输出

1. 在 `Show` 方法中，添加以下代码行：

   ```csharp
   MessageBox.Show(objectProvider.GetObject().ToString());
   ```

    此代码示例中不包含错误处理。 但在实际的可视化工具或任何其他类型的应用程序中，应当包含错误处理。

2. 在“生成”菜单上选择“生成 MyFirstVisualizer” 。 该项目应能成功生成。 在继续前更正所有生成错误。

   这是调试器端代码的结尾部分。 但是还有一步操作：添加用于通知调试对象端哪些类集合构成可视化工具的属性。

### <a name="to-add-the-type-to-visualize-for-the-debuggee-side-code"></a>添加类型以可视化调试对象端代码

在调试器端代码中，使用 <xref:System.Diagnostics.DebuggerVisualizerAttribute> 属性来指定用于可视化调式对象的类型（对象源）。 `Target` 属性设置要可视化的类型。

1. 在 DebuggerSide.cs 中的 `using` 指令之后以及 `namespace MyFirstVisualizer` 之前添加以下特性代码：

   ```csharp
   [assembly:System.Diagnostics.DebuggerVisualizer(
   typeof(MyFirstVisualizer.DebuggerSide),
   typeof(VisualizerObjectSource),
   Target = typeof(System.String),
   Description = "My First Visualizer")]
   ```

2. 在“生成”菜单上选择“生成 MyFirstVisualizer” 。 该项目应能成功生成。 在继续前更正所有生成错误。

   这时，第一个可视化工具就完成了。 如果您已正确地按照每一步操作，您可以生成该可视化工具，并将其安装到 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中。 但在将可视化工具安装到 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中之前，应对其进行测试以确保它能够正常运行。 你现在将创建一个测试套以在没有将可视化工具安装到 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中的情况下运行它。

### <a name="to-add-a-test-method-to-show-the-visualizer"></a>添加测试方法以显示可视化工具

1. 将下面的方法添加到类 `public DebuggerSide`：

   ```csharp
   public static void TestShowVisualizer(object objectToVisualize)
   {
      VisualizerDevelopmentHost visualizerHost = new VisualizerDevelopmentHost(objectToVisualize, typeof(DebuggerSide));
      visualizerHost.ShowVisualizer();
   }
   ```

2. 在“生成”菜单上选择“生成 MyFirstVisualizer” 。 该项目应能成功生成。 在继续前更正所有生成错误。

   然后，您必须创建一个可执行项目以调用可视化工具 DLL。 为简单起见，使用一个控制台应用程序项目。

### <a name="to-add-a-console-application-project-to-the-solution"></a>将控制台应用程序项目添加到解决方案中

1. 在“解决方案资源管理器”中，右键单击解决方案，选择“添加”，然后单击“新建项目”。

    ::: moniker range=">=vs-2019"

    依次选择“文件” > “新建” > “项目”    。 在“语言”下拉列表中，选择“C#”。 在搜索框中键入“控制台应用”，然后选择“控制台应用(.NET Framework)”或用于 .NET 的“控制台应用”  。 单击“下一步”  。 在出现的对话框中，键入名称 `MyTestConsole`，然后单击“创建”。

    > [!NOTE]
    > 如果要使用测试工具轻松测试可视化工具，请创建一个 .NET Framework 控制台应用。 可以改为创建 .NET 控制台应用，但稍后介绍的测试工具尚不支持 .NET，因此需要安装可视化工具来对其进行测试。 对于 .NET 控制台应用，首先在此处创建控制台应用，添加所需的 DLL 和项目引用，然后按照[添加调试对象端数据对象](#add-a-debuggee-side-data-object)中所述的步骤进行操作。
    ::: moniker-end
    ::: moniker range="vs-2017"
    从顶部菜单栏中选择“文件” > “新建” > “项目”。 在“新建项目”对话框的左窗格中，在“Visual C#”下，选择“Windows 桌面”，然后在中间窗格中选择“控制台应用(.NET Framework)”   。

    为类库键入一个适当的名称，例如 `MyTestConsole`，然后单击“确定”。
    ::: moniker-end

   现在，必须添加必要的引用，以便 MyTestConsole 能够调用 MyFirstVisualizer。

### <a name="to-add-necessary-references-to-mytestconsole"></a>添加对 MyTestConsole 的必需引用

1. 在“解决方案资源管理器”中右键单击“MyTestConsole”，然后在快捷菜单上选择“添加引用”  。

2. 在“添加引用”对话框的“浏览”选项卡上选择“Microsoft.VisualStudio.DebuggerVisualizers.DLL” 。

3. 单击 **“确定”** 。

4. 右键单击“MyTestConsole”并再次选择“添加引用” 。

5. 在“添加引用”对话框中单击“项目”选项卡，然后单击“MyFirstVisualizer” 。

6. 单击 **“确定”** 。

   现在，你将添加代码以完成测试套。

### <a name="to-add-code-to-mytestconsole"></a>将代码添加到 MyTestConsole

1. 在“解决方案资源管理器”中，右键单击“Program.cs”并选择快捷菜单上的“重命名” 。

2. 编辑名称“Program.cs”，将其更改为更有意义的名称，例如“TestConsole.cs”。

    > [!NOTE]
    > [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 会自动更改 TestConsole.cs 中的类声明，使之与新文件名匹配。

3. 在 TestConsole.cs 中，将以下代码添加到 `using` 指令中：

   ```csharp
   using MyFirstVisualizer;
   ```

4. 在方法 `Main` 中，添加以下代码：

   ```csharp
   String myString = "Hello, World";
   DebuggerSide.TestShowVisualizer(myString);
   ```

   现在已准备好测试你的第一个可视化工具了。

### <a name="to-test-the-visualizer"></a>测试可视化工具

1. 在“解决方案资源管理器”中右键单击“MyTestConsole”，然后选择快捷菜单中的“设为启动项目”  。

2. 在“调试”菜单上选择“启动” 。

    控制台应用程序会启动并显示可视化工具，其中显示字符串“Hello, World”。

   祝贺您！ 你刚刚已生成你的第一个可视化工具并进行了测试！

   如果您想在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中使用可视化工具，而不是只从测试工具中调用它，则需要安装它。 有关详细信息，请参阅[如何：安装可视化工具](../debugger/how-to-install-a-visualizer.md)。

::: moniker range=">=vs-2019"
## <a name="add-a-debuggee-side-data-object"></a>添加调试对象端数据对象

在本部分中，将从 `System.String` 数据对象转换到自定义数据对象。  

1. 在“解决方案资源管理器”中，右键单击解决方案，选择“添加”，然后单击“新建项目”。 在“语言”下拉列表中，选择“C#”。 在“搜索”框中，键入“类库”，然后选择“类库(.NET Framework)”或用于 .NET Standard 的“类库”  。

   >[!NOTE]
   >如果使用 .NET Framework 测试控制台应用，请确保创建 .NET Framework 类库项目。

1. 单击“下一步”  。 在出现的对话框中，键入名称 `MyDataObject`，然后单击“创建”。

1. （仅限 .NET Standard 类库）在解决方案资源管理器中，右键单击项目并选择“编辑项目文件”。 将 `<TargetFramework>` 值更改为 `netstandard2.0`。

   ```xml
   <TargetFramework>netstandard2.0</TargetFramework>
   ```

1. 在 `MyDataObject` 命名空间中，将默认代码替换为以下代码。

   ```csharp
   [Serializable] 
   public class CustomDataObject
   {
      public CustomDataObject()
      {
         this.MyData = "MyTestData";
      }
      public string MyData { get; set; }
   }
   ```

   对于只读可视化工具，如本示例中的工具，不一定要实现 [VisualizerObjectSource](/dotnet/api/microsoft.visualstudio.debuggervisualizers.visualizerobjectsource) 的方法。

   接下来，更新 MyFirstVisualizer 项目以使用新的数据对象。

1. 在解决方案资源管理器中的“MyFirstVisualizer”项目下，右键单击“引用”节点，然后选择“添加引用”。

1. 在“项目”下，选择“MyDataObject”项目 。

1. 在 Debuggerside.cs 的特性代码中，更新“目标”值，将 `System.String` 更改为 `MyDataObject.CustomDataObject`。

   ```csharp
   Target = typeof(MyDataObject.CustomDataObject),
   ```

1. 在 MyFirstVisualizer 项目中，将 `Show` 方法的代码替换为以下代码。

   ```csharp
   var data = objectProvider.GetObject() as MyDataObject.CustomDataObject;

   // You can replace displayForm with your own custom Form or Control.  
   Form displayForm = new Form();
   displayForm.Text = data.MyData;
   windowService.ShowDialog(displayForm);
   ```

   前面的代码使用要在窗体标题中显示的数据对象的属性。

   接下来，更新控制台应用以使用自定义数据对象。

1. 在解决方案资源管理器中的“MyTestConsole”项目下，右键单击“引用”或“依赖项”节点，并添加对 `MyDataObject` 的项目引用 。

1. 在 Program.cs 中，将 `Main` 方法中的代码替换为以下代码。

   ```csharp
   // String myString = "Hello, World";
   CustomDataObject customDataObject = new CustomDataObject();

   DebuggerSide.TestShowVisualizer(customDataObject.MyData);
   ```

1. （.NET 控制台应用）将对 `TestShowVisualizer` 的调用括在 try-catch 语句中，因为不支持测试工具。

   ```csharp
   try
   {
         DebuggerSide.TestShowVisualizer(customDataObject.MyData);
   }
   catch (Exception) {
   }
   ```

   控制台应用需要对可视化工具的运行时引用。 可以通过保留前面的代码（而不是将其注释掉）来维护引用。

1. 对于 .NET Framework 控制台应用，可以运行测试工具（按 F5），也可以按照[如何：安装可视化工具](../debugger/how-to-install-a-visualizer.md)中的说明进行操作。

   如果使用测试工具运行应用，应用会显示 Windows 窗体。

1. 对于 .NET 控制台应用，将 `MyFirstVisualizer.dll` 和 `MyDataObject.dll` 复制到[如何：安装可视化工具](../debugger/how-to-install-a-visualizer.md)中所述的文件夹中。

1. 安装可视化工具后，设置断点、运行控制台应用，并将鼠标悬停在 `customDataObject` 上方。 如果所有内容均设置正确，应会看到放大镜图标 ![VisualizerIcon](../debugger/media/dbg-tips-visualizer-icon.png "可视化工具图标")。

   :::image type="content" source="../debugger/media/vs-2019/visualizer-csharp-data-object.png" alt-text="可视化工具放大镜图标。":::

   从放大镜中选择“MyFirstVisualizer”时，会看到窗体及其标题中显示的数据对象文本。

   ![显示 Windows 窗体的可视化工具](../debugger/media/vs-2019/visualizer-csharp-windows-form.png)

::: moniker-end

::: moniker range="vs-2017"

## <a name="create-a-visualizer-using-the-visualizer-item-template"></a>使用可视化工具项模板创建可视化工具

到目前为止，本演练演示了如何手动创建可视化工具。 至此，我们完成了这项学习训练。 现在你已了解简单的可视化工具的工作原理，可以通过更简单的方法创建一个可视化工具：使用可视化工具项模板。

首先，必须新建一个类库项目。

### <a name="to-create-a-new-class-library"></a>新建一个类库

1. 在“文件”菜单上，选择“新建”>“项目” 。

2. 在“新建项目”对话框中的“Visual C#”下选择“.NET Framework”。

3. 在中间窗格中，选择“类库”。

4. 在“名称”框中，为类库键入一个适当的名称，例如“MySecondVisualizer”。

5. 单击 **“确定”** 。

   现在可以向其添加可视化工具项：

### <a name="to-add-a-visualizer-item"></a>添加可视化工具项

1. 在“解决方案资源管理器”中，右键单击“MySecondVisualizer”项目。

2. 在快捷菜单中，选择“添加”然后单击“新项”。

3. 在“添加新项”对话框的“Visual C# 项”下选择“调试器可视化工具”  。

4. 在“名称”框中，键入一个适当的名称，例如“SecondVisualizer.cs”。

5. 单击 **添加**。

   就这么简单。 查看文件 SecondVisualizer.cs，并查看模板添加的代码。 继续试验这些代码。 了解基础知识后，可以自己创建更复杂、更有用的可视化工具。
::: moniker-end

## <a name="see-also"></a>请参阅

- [可视化工具体系结构](../debugger/visualizer-architecture.md)
- [如何：安装可视化工具](../debugger/how-to-install-a-visualizer.md)
- [创建自定义可视化工具](../debugger/create-custom-visualizers-of-data.md)

---
title: 扩展属性、任务列表、输出、选项窗口
description: 了解如何将有关工具窗口的信息集成到Visual Studio"属性"页上的新"选项"页和新设置中。
ms.date: 11/04/2016
ms.custom: SEO-VS-2020
ms.topic: how-to
helpviewer_keywords:
- properties pane
- task list
- output window
- properties window
- tutorials
- tool windows
ms.assetid: 06990510-5424-44b8-9fd9-6481acec5c76
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3334ba3694ee3c1354c152b013c38472e4b90b72
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112903276"
---
# <a name="extend-the-properties-task-list-output-and-options-windows"></a>扩展"属性任务列表、输出和选项"窗口
可以访问工具窗口中的任何Visual Studio。 本演练演示如何将有关工具窗口的信息集成到"属性"页上的新"选项"页 **和新** 设置中，以及如何写入"任务列表和 **输出**"窗口。 

## <a name="prerequisites"></a>先决条件
 从 2015 Visual Studio开始，不会从下载Visual Studio安装 Visual Studio SDK。 它作为可选功能包含在安装程序Visual Studio中。 也可稍后安装 VS SDK。 有关详细信息，请参阅安装[Visual Studio SDK。](../extensibility/installing-the-visual-studio-sdk.md)

## <a name="create-an-extension-with-a-tool-window"></a>使用工具窗口创建扩展

1. 使用 VSIX 模板创建名为 **TodoList** 的项目，并添加名为 **TodoWindow** 的自定义工具窗口项模板。

    > [!NOTE]
    > 有关使用工具窗口创建扩展的信息，请参阅 [使用工具窗口 创建扩展](../extensibility/creating-an-extension-with-a-tool-window.md)。

## <a name="set-up-the-tool-window"></a>设置工具窗口
 添加用于键入新 ToDo 项的 TextBox、用于将新项添加到列表的按钮和用于显示列表项的 ListBox。

1. 在 *TodoWindow.xaml* 中，从 UserControl 中删除 Button、TextBox 和 StackPanel 控件。

    > [!NOTE]
    > 这不会 **删除button1_Click处理程序** ，你将在稍后的步骤中重复使用该处理程序。

2. 从" **工具箱"的"所有 WPF** 控件 **"部分，** 将 **"画布"** 控件拖到网格中。

3. 将 **TextBox、****按钮** 和 **ListBox** 拖动到画布。 排列元素，使 TextBox 和 Button 位于同一级别，ListBox 将填充它们下面的窗口的其余部分，如下图所示。

     ![已完成的工具窗口](../extensibility/media/t5-toolwindow.png "T5-ToolWindow")

4. 在"XAML"窗格中，找到"按钮"，将其"内容"属性设置为"**添加"。** 通过添加 属性将按钮事件处理程序重新连接到 Button `Click="button1_Click"` 控件。 Canvas 块应如下所示：

    ```xml
    <Canvas HorizontalAlignment="Left" Width="306">
        <TextBox x:Name="textBox" HorizontalAlignment="Left" Height="23" Margin="10,10,0,0" TextWrapping="Wrap" Text="TextBox" VerticalAlignment="Top" Width="208"/>
            <Button x:Name="button" Content="Add" HorizontalAlignment="Left" Margin="236,13,0,0" VerticalAlignment="Top" Width="48" Click="button1_Click"/>
            <ListBox x:Name="listBox" HorizontalAlignment="Left" Height="222" Margin="10,56,0,0" VerticalAlignment="Top" Width="274"/>
    </Canvas>
    ```

### <a name="customize-the-constructor"></a>自定义构造函数

1. 在 *TodoWindowControl.xaml.cs* 文件中，添加以下 using 指令：

    ```csharp
    using System;
    ```

2. 添加对 TodoWindow 的公共引用，让 TodoWindowControl 构造函数使用 TodoWindow 参数。 代码应如下所示：

    ```csharp
    public TodoWindow parent;

    public TodoWindowControl(TodoWindow window)
    {
        InitializeComponent();
        parent = window;
    }
    ```

3. 在 *TodoWindow.cs* 中，更改 TodoWindowControl 构造函数以包含 TodoWindow 参数。 代码应如下所示：

    ```csharp
    public TodoWindow() : base(null)
    {
        this.Caption = "TodoWindow";
        this.BitmapResourceID = 301;
        this.BitmapIndex = 1;

         this.Content = new TodoWindowControl(this);
    }
    ```

## <a name="create-an-options-page"></a>"创建选项"页
 可以在"选项"对话框中 **提供** 一个页面，以便用户可以更改工具窗口的设置。 创建"选项"页需要描述选项的类以及 *TodoListPackage.cs* 或 *TodoListPackage.vb 文件中一个* 条目。

1. 添加名为的 `ToolsOptions.cs` 的类。 使 `ToolsOptions` 类继承自 <xref:Microsoft.VisualStudio.Shell.DialogPage> 。

   ```csharp
   class ToolsOptions : DialogPage
   {
   }
   ```

2. 添加以下 using 指令：

   ```csharp
   using Microsoft.VisualStudio.Shell;
   ```

3. 本演练中的"选项"页仅提供一个名为 DaysAhead 的选项。 将名为 **daysAhead 的** 私有字段和名为 **DaysAhead** 的属性添加到 `ToolsOptions` 类：

   ```csharp
   private double daysAhead;

   public double DaysAhead
   {
       get { return daysAhead; }
       set { daysAhead = value; }
   }
   ```

   现在，必须让项目了解此"选项"页。

### <a name="make-the-options-page-available-to-users"></a>使"选项"页可供用户使用

1. 在 *TodoWindowPackage.cs* 中，将 <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> 添加到 `TodoWindowPackage` 类：

    ```csharp
    [ProvideOptionPage(typeof(ToolsOptions), "ToDo", "General", 101, 106, true)]
    ```

2. ProvideOptionPage 构造函数的第一个参数是之前创建的 `ToolsOptions` 类的类型。 第二个参数"ToDo"是"选项"对话框中 **类别** 的名称。 第三个参数"常规"是"选项"对话框的子类别的名称，其中"选项"页将可用。 接下来的两个参数是字符串的资源 D;第一个是类别的名称，第二个是子类别的名称。 最后一个参数确定是否可以使用自动化访问此页。

     当用户打开"选项"页时，它应如下图所示。

     ![“选项”页](../extensibility/media/t5optionspage.gif "T5OptionsPage")

     请注意类别 **ToDo** 和子类别"常规 **"。**

## <a name="make-data-available-to-the-properties-window"></a>使数据可供属性窗口
 可以通过创建一个名为 的类来存储有关 ToDo 列表中各个项的信息，使 `TodoItem` ToDo 列表信息可用。

1. 添加名为的 `TodoItem.cs` 的类。

     当用户可以使用工具窗口时，ListBox 中的项由 TodoItems 表示。 当用户在 ListBox 中选择这些项之一时，"属性 **"窗口将显示** 有关该项的信息。

     若要使数据在"属性 **"** 窗口中可用，请将数据转换为具有两个特殊属性 的公共属性： `Description` 和 `Category` 。 `Description` 是显示在"属性" **窗口底部的文本** 。 `Category` 确定在"分类" **视图中显示"** 属性"窗口时 **属性应显示** 的位置。 下图中，"属性"窗口位于"分类"视图中 **，"ToDo** 字段"类别中的"名称"属性处于选中状态，"**名称**"属性的说明显示在窗口底部。

     ![“属性”窗口](../extensibility/media/t5properties.png "T5Properties")

2. 将以下 using 指令添加到 *TodoItem.cs* 文件。

    ```csharp
    using System.ComponentModel;
    using System.Windows.Forms;
    using Microsoft.VisualStudio.Shell.Interop;
    ```

3. 将 `public` 访问修饰符添加到类声明。

    ```csharp
    public class TodoItem
    {
    }
    ```

     添加两个属性： `Name` 和 `DueDate` 。 我们将执行 `UpdateList()` 和 `CheckForErrors()` 更高版本。

    ```csharp
    public class TodoItem
    {
        private TodoWindowControl parent;
        private string name;
        [Description("Name of the ToDo item")]
        [Category("ToDo Fields")]
        public string Name
        {
            get { return name; }
            set
            {
                name = value;
                parent.UpdateList(this);
            }
        }

        private DateTime dueDate;
        [Description("Due date of the ToDo item")]
        [Category("ToDo Fields")]
        public DateTime DueDate
        {
            get { return dueDate; }
            set
            {
                dueDate = value;
                parent.UpdateList(this);
                parent.CheckForErrors();
            }
        }
    }
    ```

4. 添加对用户控件的专用引用。 添加一个构造函数，该构造函数采用用户控件和此 ToDo 项的名称。 若要查找 的值 `daysAhead` ，它获取"选项"页属性。

    ```csharp
    private TodoWindowControl parent;

    public TodoItem(TodoWindowControl control, string itemName)
    {
        parent = control;
        name = itemName;
        dueDate = DateTime.Now;

        double daysAhead = 0;
        IVsPackage package = parent.parent.Package as IVsPackage;
        if (package != null)
        {
            object obj;
            package.GetAutomationObject("ToDo.General", out obj);

            ToolsOptions options = obj as ToolsOptions;
            if (options != null)
            {
                daysAhead = options.DaysAhead;
            }
        }

        dueDate = dueDate.AddDays(daysAhead);
    }
    ```

5. 由于 类的实例将存储在 `TodoItem` ListBox 中，ListBox 将调用 函数， `ToString` 因此必须重载 `ToString` 函数。 将以下代码添加到 *TodoItem.cs*，在 构造函数之后和 类的末尾之前。

    ```csharp
    public override string ToString()
    {
        return name + " Due: " + dueDate.ToShortDateString();
    }
    ```

6. 在 *TodoWindowControl.xaml.cs* 中，将存根方法添加到 和 `TodoWindowControl` 方法的 `CheckForError` `UpdateList` 类。 将它们放在 ProcessDialogChar 之后和文件末尾之前。

    ```csharp
    public void CheckForErrors()
    {
    }
    public void UpdateList(TodoItem item)
    {
    }
    ```

     方法将调用父对象中同名的方法，该方法将检查是否发生了任何错误 `CheckForError` 并正确处理它们。 `UpdateList`方法将更新父控件中的 ListBox;当此类中的 和 属性更改 `Name` 时 `DueDate` ，将调用 方法。 稍后将实现它们。

## <a name="integrate-into-the-properties-window"></a>集成到属性窗口
 现在编写用于管理 ListBox 的代码，该代码将绑定到" **属性"** 窗口。

 必须更改按钮单击处理程序以读取 TextBox、创建 TodoItem 并添加到 ListBox。

1. 将现有 `button1_Click` 函数替换为创建新 TodoItem 并添加到 ListBox 的代码。 它调用 `TrackSelection()` ，稍后将定义它。

    ```csharp
    private void button1_Click(object sender, RoutedEventArgs e)
    {
        if (textBox.Text.Length > 0)
        {
            var item = new TodoItem(this, textBox.Text);
            listBox.Items.Add(item);
            TrackSelection();
            CheckForErrors();
        }
    }
    ```

2. 在"设计视图选择 ListBox 控件。 在" **属性** "窗口中，单击 **"事件处理程序"** 按钮并找到 **SelectionChanged** 事件。 在文本框中 **填写listBox_SelectionChanged。** 这样做会为 SelectionChanged 处理程序添加存根，并将其分配给 事件。

3. 实现 `TrackSelection()` 方法。 由于需要获取服务 <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> ，因此需要使 <xref:Microsoft.VisualStudio.Shell.WindowPane.GetService%2A> TodoWindowControl 可访问 。 将以下方法添加到 `TodoWindow` 类：

    ```
    internal object GetVsService(Type service)
    {
        return GetService(service);
    }
    ```

4. 将以下 using 指令添加到 *TodoWindowControl.xaml.cs*：

    ```csharp
    using System.Runtime.InteropServices;
    using Microsoft.VisualStudio.Shell.Interop;
    using Microsoft.VisualStudio;
    using Microsoft.VisualStudio.Shell;
    ```

5. 按如下所示填写 SelectionChanged 处理程序：

    ```
    private void listBox_SelectionChanged(object sender, SelectionChangedEventArgs e)
    {
        TrackSelection();
    }
    ```

6. 现在，填写 TrackSelection 函数，该函数将提供与"属性" **窗口的** 集成。 当用户将项添加到 ListBox 或单击 ListBox 中的项时，将调用此函数。 它将 ListBox 的内容添加到 SelectionContainer，并将 SelectionContainer 传递给"属性 **"窗口** <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A> 的事件处理程序。 TrackSelection 服务跟踪用户界面中的选定对象 (UI) 并显示其属性

    ```csharp
    private SelectionContainer mySelContainer;
    private System.Collections.ArrayList mySelItems;
    private IVsWindowFrame frame = null;

    private void TrackSelection()
    {
        if (frame == null)
        {
            var shell = parent.GetVsService(typeof(SVsUIShell)) as IVsUIShell;
            if (shell != null)
            {
                var guidPropertyBrowser = new
                Guid(ToolWindowGuids.PropertyBrowser);
                shell.FindToolWindow((uint)__VSFINDTOOLWIN.FTW_fForceCreate,
                ref guidPropertyBrowser, out frame);
            }
        }
        if (frame != null)
            {
                frame.Show();
            }
        if (mySelContainer == null)
        {
            mySelContainer = new SelectionContainer();
        }

        mySelItems = new System.Collections.ArrayList();

        var selected = listBox.SelectedItem as TodoItem;
        if (selected != null)
        {
            mySelItems.Add(selected);
        }

        mySelContainer.SelectedObjects = mySelItems;

        ITrackSelection track = parent.GetVsService(typeof(STrackSelection))
                                as ITrackSelection;
        if (track != null)
        {
            track.OnSelectChange(mySelContainer);
        }
    }
    ```

     有了"属性"窗口可以使用的类后，可以将"属性 **"** 窗口与工具窗口集成。 当用户单击工具窗口的 ListBox 中的项时 **，"属性** "窗口应相应地更新。 同样，当用户在"属性"窗口中更改 ToDo项时，应更新关联的项。

7. 现在，在 *TodoWindowControl.xaml.cs 中添加 UpdateList 函数代码的其余部分*。 它应从 ListBox 删除并重新添加修改后的 TodoItem。

    ```csharp
    public void UpdateList(TodoItem item)
    {
        var index = listBox.SelectedIndex;
        listBox.Items.RemoveAt(index);
        listBox.Items.Insert(index, item);
        listBox.SelectedItem = index;
    }
    ```

8. 测试代码。 生成项目并启动调试。 应显示实验实例。

9. 打开"**工具**  >  **选项"** 页。 应在左窗格中看到"ToDo"类别。 类别按字母顺序列出，因此在 Ts 下查看。

10. 在 **"Todo** 选项"页上，应看到 `DaysAhead` 属性设置为 **0。** 将更改为 **2**。

11. 在"**视图"/"其他窗口"菜单** 上，打开 **"TodoWindow"。** 在 **文本框中键入 EndDate，** 然后单击"添加 **"。**

12. 在列表框中，应会看到比今天晚两天的日期。

## <a name="add-text-to-the-output-window-and-items-to-the-task-list"></a>将文本添加到"输出"窗口，将项添加到任务列表
 对于 **任务列表，** 请创建 Task **类型的** 新对象，然后通过调用其 方法将任务列表 Task `Add` 对象添加到该对象。 若要写入 **"输出"** 窗口，请调用其 方法来获取窗格对象，然后调用 `GetPane` `OutputString` 窗格对象的 方法。

1. 在 *TodoWindowControl.xaml.cs* 的 方法中，添加代码，获取"输出"窗口的"常规"窗格 (这是默认) ，并写入 `button1_Click` 其中。 方法应如下所示：

    ```csharp
    private void button1_Click(object sender, EventArgs e)
    {
        if (textBox.Text.Length > 0)
        {
            var item = new TodoItem(this, textBox.Text);
            listBox.Items.Add(item);

            var outputWindow = parent.GetVsService(
                typeof(SVsOutputWindow)) as IVsOutputWindow;
            IVsOutputWindowPane pane;
            Guid guidGeneralPane = VSConstants.GUID_OutWindowGeneralPane;
            outputWindow.GetPane(ref guidGeneralPane, out pane);
            if (pane != null)
            {
                 pane.OutputString(string.Format(
                    "To Do item created: {0}\r\n",
                 item.ToString()));
        }
            TrackSelection();
            CheckForErrors();
        }
    }
    ```

2. 若要将项添加到 任务列表，需要将嵌套类添加到 TodoWindowControl 类。 嵌套类需要从 派生 <xref:Microsoft.VisualStudio.Shell.TaskProvider> 。 将以下代码添加到 类 `TodoWindowControl` 的末尾。

    ```csharp
    [Guid("72de1eAD-a00c-4f57-bff7-57edb162d0be")]
    public class TodoWindowTaskProvider : TaskProvider
    {
        public TodoWindowTaskProvider(IServiceProvider sp)
            : base(sp)
        {
        }
    }
    ```

3. 接下来，向 类添加对 `TodoTaskProvider` 的私有引用 `CreateProvider()` 和 `TodoWindowControl` 方法。 代码应如下所示：

    ```csharp
    private TodoWindowTaskProvider taskProvider;
    private void CreateProvider()
    {
        if (taskProvider == null)
        {
            taskProvider = new TodoWindowTaskProvider(parent);
            taskProvider.ProviderName = "To Do";
        }
    }
    ```

4. 添加 `ClearError()` ，它清除任务列表和 ，这将向 类任务列表 `ReportError()` 项 `TodoWindowControl` 。

    ```csharp
    private void ClearError()
    {
        CreateProvider();
        taskProvider.Tasks.Clear();
    }
    private void ReportError(string p)
    {
        CreateProvider();
        var errorTask = new Task();
        errorTask.CanDelete = false;
        errorTask.Category = TaskCategory.Comments;
        errorTask.Text = p;

        taskProvider.Tasks.Add(errorTask);

        taskProvider.Show();

        var taskList = parent.GetVsService(typeof(SVsTaskList))
            as IVsTaskList2;
        if (taskList == null)
        {
            return;
        }

        var guidProvider = typeof(TodoWindowTaskProvider).GUID;
         taskList.SetActiveProvider(ref guidProvider);
    }
    ```

5. 现在实现 `CheckForErrors` 方法，如下所示。

    ```csharp
    public void CheckForErrors()
    {
        foreach (TodoItem item in listBox.Items)
        {
            if (item.DueDate < DateTime.Now)
            {
                ReportError("To Do Item is out of date: "
                    + item.ToString());
            }
        }
    }
    ```

## <a name="try-it-out"></a>试试看

1. 生成项目并启动调试。 这将显示实验实例。

2. 打开 **TodoWindow (**  >  **查看其他 Windows**  >  **TodoWindow**) 。

3. 在文本框中键入内容，然后单击"添加 **"。**

     将在今天之后 2 天的截止日期添加到列表框中。 不会生成任何错误，任务列表 (**视图**  >  **任务列表)** 应没有条目。

4. 现在，将"工具选项  >    >  **""ToDo"** 页上的设置从 **2** 更改回 **0。**

5. 在 **TodoWindow 中键入其他内容，** 然后再次单击" **添加** "。 这会在 中触发错误 **和任务列表。**

     添加项时，初始日期设置为现在加上 2 天。

6. 在" **视图"** 菜单上，单击 **"输出** "打开" **输出"** 窗口。

     请注意，每次添加项时，都会在"项目" **窗格中任务列表消息** 。

7. 单击 ListBox 中的项之一。

     " **属性** "窗口显示项的两个属性。

8. 更改其中一个属性，然后按 **Enter**。

     该项在 ListBox 中更新。

---
title: 向"属性"窗口窗口公开|Microsoft Docs
description: 了解对象的公共属性。 对这些属性所做的更改将反映在属性窗口。
ms.custom: SEO-VS-2020
ms.date: 3/16/2019
ms.topic: how-to
helpviewer_keywords:
- properties [Visual Studio SDK], exposing in Property Browser
- properties [Visual Studio SDK]
- Property Browser, exposing properties
ms.assetid: 47f295b5-1ca5-4e7b-bb52-7b926b136622
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 957a6445934d9d3af7cb0f9d61b72171d48521755a1ff9ff4410b31fbe9893a4
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121388690"
---
# <a name="expose-properties-to-the-properties-window"></a>向对象公开属性窗口

本演练向"属性"窗口公开对象 **的公共** 属性。 对这些属性所做的更改将反映在"属性 **"** 窗口中。

## <a name="prerequisites"></a>先决条件

从 2015 Visual Studio开始，不会从下载Visual Studio安装 Visual Studio SDK。 它作为可选功能包含在安装程序Visual Studio中。 也可稍后安装 VS SDK。 有关详细信息，请参阅安装[Visual Studio SDK。](../extensibility/installing-the-visual-studio-sdk.md)

## <a name="expose-properties-to-the-properties-window"></a>向对象公开属性窗口

在本部分，你将创建自定义工具窗口，并显示"属性"窗口中关联窗口窗格 **对象的公共** 属性。

### <a name="to-expose-properties-to-the-properties-window"></a>向对象公开属性窗口

1. 每个Visual Studio扩展都从 VSIX 部署项目开始，该项目将包含扩展资产。 创建名为 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 的 VSIX 项目 `MyObjectPropertiesExtension` 。 可以通过搜索"vsix"在"新建Project"找到 VSIX 项目模板。 

2. 通过添加名为 的自定义工具窗口项模板来添加工具窗口 `MyToolWindow` 。 在“解决方案资源管理器”中，右键单击项目节点并选择“添加” > “新建项”  。 在"**添加新项"对话框中**，转到 **"Visual C# 项**  >  **扩展性"，然后选择**"**自定义工具窗口"。** 在 **对话框底部的** "名称"字段中，将文件名更改为 *MyToolWindow.cs*。 若要详细了解如何创建自定义工具窗口，请参阅 [使用工具窗口创建扩展](../extensibility/creating-an-extension-with-a-tool-window.md)。

3. 打开 *MyToolWindow.cs* 并添加以下 using 语句：

   ```csharp
   using System.Collections;
   using System.ComponentModel;
   using Microsoft.VisualStudio.Shell.Interop;
   ```

4. 现在，将以下字段添加到 `MyToolWindow` 类。

   ```csharp
   private ITrackSelection trackSel;
   private SelectionContainer selContainer;

   ```

5. 将以下代码添加到 `MyToolWindow` 类。

   ```csharp
   private ITrackSelection TrackSelection
   {
       get
       {
           if (trackSel == null)
               trackSel =
                  GetService(typeof(STrackSelection)) as ITrackSelection;
           return trackSel;
       }
   }

   public void UpdateSelection()
   {
       ITrackSelection track = TrackSelection;
       if (track != null)
           track.OnSelectChange((ISelectionContainer)selContainer);
   }

   public void SelectList(ArrayList list)
   {
       selContainer = new SelectionContainer(true, false);
       selContainer.SelectableObjects = list;
       selContainer.SelectedObjects = list;
       UpdateSelection();
   }

   public override void OnToolWindowCreated()
   {
       ArrayList listObjects = new ArrayList();
       listObjects.Add(this);
       SelectList(listObjects);
   }
   ```

    `TrackSelection`属性使用 `GetService` 获取提供 `STrackSelection` 接口的服务 <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection> 。 事件 `OnToolWindowCreated` 处理程序和方法共同创建仅包含工具窗口窗格对象本身的选定 `SelectList` 对象的列表。 `UpdateSelection`方法告知"**属性"** 窗口显示工具窗口窗格的公共属性。

6. 生成项目并启动调试。 应显示 Visual Studio实例。

7. 如果" **属性"** 窗口不可见，则按 **F4 打开它**。

8. 打开 **"MyToolWindow"** 窗口。 可以在"**查看其他"Windows**  >  找到它。

    窗口随即打开，窗口窗格的公共属性将显示在"属性 **"** 窗口中。

9. 将"**属性"** 窗口中的 Caption **属性** 更改为 **"我的对象属性"。**

     MyToolWindow 窗口标题会相应地更改。

## <a name="expose-tool-window-properties"></a>公开工具窗口属性

在本部分，你将添加一个工具窗口并公开其属性。 对属性所做的更改将反映在"属性 **"** 窗口中。

### <a name="to-expose-tool-window-properties"></a>公开工具窗口属性

1. 打开 *MyToolWindow.cs*，将公共布尔属性 IsChecked 添加到 `MyToolWindow` 类。

    ```csharp
    [Category("My Properties")]
    [Description("MyToolWindowControl properties")]
    public bool IsChecked
    {
        get {
            if (base.Content == null)  return false;
            return (bool)(( MyToolWindowControl) base.Content).checkBox.IsChecked;
        }
        set {
            ((MyToolWindowControl) base.Content).checkBox.IsChecked = value;
        }
    }
    ```

     此属性从稍后创建的 WPF 复选框获取其状态。

2. 打开 *MyToolWindowControl.xaml.cs，* 将 MyToolWindowControl 构造函数替换为以下代码。

    ```vb
    private MyToolWindow pane;
    public MyToolWindowControl(MyToolWindow pane)
    {
        InitializeComponent();
        this.pane = pane;
        checkBox.IsChecked = false;
    }
    ```

     这将 `MyToolWindowControl` 授予对窗格 `MyToolWindow` 的访问权限。

3. 在 *MyToolWindow.cs* 中， `MyToolWindow` 按如下所示更改构造函数：

    ```csharp
    base.Content = new MyToolWindowControl(this);
    ```

4. 更改为 MyToolWindowControl 的设计视图。

5. 删除按钮，将"工具箱" **中的复选框添加到** 左上角。

6. 添加 Checked 和 Unchecked 事件。 选中设计视图中的复选框。 在"**属性**"窗口中，单击"属性 (窗口右上方的"事件处理程序"**按钮) 。** 在 **文本框** 中checkbox_Checked **Checked"****并键入**"已选中"，然后在文本框 **checkbox_Unchecked键入"** 未选中"。

7. 添加复选框事件处理程序：

    ```csharp
    private void checkbox_Checked(object sender, RoutedEventArgs e)
    {
        pane.IsChecked = true;
        pane.UpdateSelection();
    }
    private void checkbox_Unchecked(object sender, RoutedEventArgs e)
    {
        pane.IsChecked = false;
        pane.UpdateSelection();
    }
    ```

8. 生成项目并启动调试。

9. 在实验实例中，打开 **MyToolWindow** 窗口。

     在"属性"窗口中查找 **窗口** 的属性。 **IsChecked** 属性显示在窗口底部的"我的属性"**类别** 下。

10. 选中 **"MyToolWindow"窗口中的** 复选框。 **"属性"****窗口中的** IsChecked 将更改为 **True。** 清除 **"MyToolWindow"窗口中的** 复选框。 **"属性"****窗口中的** IsChecked 将更改为 **False。** 在"属性"**窗口中更改 IsChecked****的值。** **MyToolWindow** 窗口中的复选框会更改以匹配新值。

    > [!NOTE]
    > 如果必须释放"属性"窗口中显示 **的对象** ，请首先 `OnSelectChange` 使用选择 `null` 容器调用 。 释放属性或对象后，可以更改为已更新 和 列表的选择 <xref:Microsoft.VisualStudio.Shell.SelectionContainer.SelectableObjects%2A> <xref:Microsoft.VisualStudio.Shell.SelectionContainer.SelectedObjects%2A> 容器。

## <a name="change-selection-lists"></a>更改选择列表

 在本部分，你将为基本属性类添加选择列表，并使用工具窗口界面选择要显示的选择列表。

### <a name="to-change-selection-lists"></a>更改选择列表

1. 打开 *MyToolWindow.cs* 并添加名为 的公共类 `Simple` 。

    ```csharp
    public class Simple
    {
        private string someText = "";

        [Category("My Properties")]
        [Description("Simple Properties")]
        [DisplayName("My Text")]
        public string SomeText
        {
            get { return someText; }
            set { someText = value; }
        }

        [Category("My Properties")]
        [Description("Read-only property")]
        public bool ReadOnly
        {
            get { return false; }
        }
    }
    ```

2. 将 `SimpleObject` 属性添加到 类 `MyToolWindow` ，以及两种方法以在窗口窗格和 对象之间切换"属性" `Simple` 窗口选择。

    ```csharp
    private Simple simpleObject = null;
    public Simple SimpleObject
    {
        get
        {
            if (simpleObject == null) simpleObject = new Simple();
            return simpleObject;
        }
    }

    public void SelectSimpleList()
    {
        ArrayList listObjects = new ArrayList();
        listObjects.Add(SimpleObject);
        SelectList(listObjects);
    }

    public void SelectThisList()
    {
        ArrayList listObjects = new ArrayList();
        listObjects.Add(this);
        SelectList(listObjects);
    }
    ```

3. 在 *MyToolWindowControl.cs* 中，将复选框处理程序替换为以下代码行：

    ```csharp
    private void checkbox_Checked(object sender, RoutedEventArgs e)
     {
        pane.IsChecked = true;
        pane.SelectSimpleList();
        pane.UpdateSelection();
    }
    private void checkbox_Unchecked(object sender, RoutedEventArgs e)
    {
        pane.IsChecked = false;
        pane.SelectThisList();
        pane.UpdateSelection();
    }
    ```

4. 生成项目并启动调试。

5. 在实验实例中，打开 **MyToolWindow** 窗口。

6. 选中 **"MyToolWindow"窗口中的** 复选框。 "**属性"** 窗口显示 `Simple` 对象属性 **SomeText** 和 **ReadOnly。** 清除该复选框。 窗口的公共属性显示在" **属性"窗口中** 。

    > [!NOTE]
    > SomeText 的显示 **名称** 为"**我的文本"。**

## <a name="best-practice"></a>最佳做法

本演练中实现了 ，以便可选择的对象集合和所选 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> 对象集合是同一集合。 "属性浏览器"列表中只显示所选对象。 有关更完整的 ISelectionContainer 实现，请参阅 Reference.ToolWindow 示例。

Visual Studio会话之间保持Visual Studio窗口。 有关保留工具窗口状态的信息，请参阅 <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> 。

## <a name="see-also"></a>另请参阅

- [扩展属性和"属性"窗口](../extensibility/extending-properties-and-the-property-window.md)

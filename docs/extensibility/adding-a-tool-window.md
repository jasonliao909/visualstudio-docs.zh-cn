---
title: 添加工具窗口|Microsoft Docs
description: 了解如何通过将控件和包含命令的工具栏添加到工具窗口Visual Studio工具窗口并将其集成到工具窗口。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- tutorials
- tool windows
ms.assetid: 8e16c381-03c8-404e-92ef-3614cdf3150a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 3bf82de2fd491f786ed3a882ee44adb20b38d442
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122035277"
---
# <a name="add-a-tool-window"></a>添加工具窗口

本演练将了解如何创建工具窗口并将其集成到Visual Studio中：

- 将控件添加到工具窗口。

- 将工具栏添加到工具窗口。

- 将命令添加到工具栏。

- 实现命令。

- 设置工具窗口的默认位置。

## <a name="prerequisites"></a>必备条件

Visual Studio SDK 作为可选功能包含在安装程序Visual Studio中。 有关详细信息，请参阅安装[Visual Studio SDK。](../extensibility/installing-the-visual-studio-sdk.md)

## <a name="create-a-tool-window"></a>创建工具窗口

1. 使用 VSIX 模板创建 **名为 FirstToolWin** 的项目，并添加名为 **FirstToolWindow** 的自定义工具窗口项模板。

    > [!NOTE]
    > 有关使用工具窗口创建扩展的信息，请参阅使用工具窗口 [创建扩展](../extensibility/creating-an-extension-with-a-tool-window.md)。

## <a name="add-a-control-to-the-tool-window"></a>向工具窗口添加控件

1. 删除默认控件。 打开 *FirstToolWindowControl.xaml* 并删除" **单击我！"** 按钮。

2. 在" **工具箱"** 中，展开" **所有 WPF 控件** "部分，并将 **"媒体元素** "控件拖动到 **"FirstToolWindowControl"** 窗体。 选择控件，在"属性 **"** 窗口中，将此元素命名 **mediaElement1**。

## <a name="add-a-toolbar-to-the-tool-window"></a>向工具窗口添加工具栏
通过按以下方式添加工具栏，可以保证其渐变和颜色与 IDE 的其余部分一致。

1. 在 **解决方案资源管理器** 中，打开 *FirstToolWindowPackage.vsct*。 *.vsct* 文件使用 XML 定义 (GUI) 工具窗口中元素的图形用户界面。

2. 在 `<Symbols>` 部分中，找到 `<GuidSymbol>` 其属性 `name` 为 的节点 `guidFirstToolWindowPackageCmdSet` 。 将以下两个元素添加到此节点中的元素 `<IDSymbol>` `<IDSymbol>` 列表中，以定义工具栏和工具栏组。

    ```xml
    <IDSymbol name="ToolbarID" value="0x1000" />
    <IDSymbol name="ToolbarGroupID" value="0x1001" />
    ```

3. 在 节 `<Buttons>` 的正上方， `<Menus>` 创建类似于以下内容的部分：

    ```xml
    <Menus>
        <Menu guid="guidFirstToolWindowPackageCmdSet" id="ToolbarID" priority="0x0000" type="ToolWindowToolbar">
            <Parent guid="guidFirstToolWindowPackageCmdSet" id="ToolbarID" />
            <Strings>
                <ButtonText>Tool Window Toolbar</ButtonText>
                <CommandName>Tool Window Toolbar</CommandName>
            </Strings>
        </Menu>
    </Menus>
    ```

    有几种不同类型的菜单。 此菜单是工具窗口中的工具栏，由其 属性 `type` 定义。 `guid`和 `id` 设置是工具栏的完全限定 ID。 通常， `<Parent>` 菜单的 是包含组。 但是，工具栏定义为其自己的父级。 因此， 和 元素使用相同的 `<Menu>` `<Parent>` 标识符。 属性 `priority` 只是"0"。

4. 工具栏以多种方式类似于菜单。 例如，正如菜单可能包含一组命令一样，工具栏也可能有组。  (菜单上，命令组由水平行分隔。 在工具栏上，组不由可视分隔符分隔。) 

    添加 `<Groups>` 包含 元素的 `<Group>` 节。 这将定义在 节中声明其 ID 的 `<Symbols>` 组。 在 节 `<Groups>` 的正后添加 `<Menus>` 部分。

    ```xml
    <Groups>
        <Group guid="guidFirstToolWindowPackageCmdSet" id="ToolbarGroupID" priority="0x0000">
            <Parent guid="guidFirstToolWindowPackageCmdSet" id="ToolbarID" />
        </Group>
    </Groups>
    ```

    将父 GUID 和 ID 设置为工具栏的 GUID 和 ID，即可将组添加到工具栏。

## <a name="add-a-command-to-the-toolbar"></a>将命令添加到工具栏

将命令添加到工具栏，该命令显示为按钮。

1. 在 `<Symbols>` 部分中，在工具栏和工具栏组声明之后声明以下 IDSymbol 元素。

    ```xml
    <IDSymbol name="cmdidWindowsMedia" value="0x0100" />
    <IDSymbol name="cmdidWindowsMediaOpen" value="0x132" />
    ```

2. 在 节中添加 Button `<Buttons>` 元素。 此元素将显示在工具窗口的工具栏上，具有"搜索 **" (放大** 镜) 图标。

    ```xml
    <Button guid="guidFirstToolWindowPackageCmdSet" id="cmdidWindowsMediaOpen" priority="0x0101" type="Button">
        <Parent guid="guidFirstToolWindowPackageCmdSet" id="ToolbarGroupID"/>
        <Icon guid="guidImages" id="bmpPicSearch" />
        <Strings>
            <CommandName>cmdidWindowsMediaOpen</CommandName>
            <ButtonText>Load File</ButtonText>
        </Strings>
    </Button>
    ```

3. 打开 *FirstToolWindowCommand.cs，* 将以下行添加到 类中现有字段的正之后。

    ```csharp
    public const string guidFirstToolWindowPackageCmdSet = "00000000-0000-0000-0000-0000";  // get the GUID from the .vsct file
    public const uint cmdidWindowsMedia = 0x100;
    public const int cmdidWindowsMediaOpen = 0x132;
    public const int ToolbarID = 0x1000;
    ```

    这样做可使命令在代码中可用。

## <a name="add-a-mediaplayer-property-to-firsttoolwindowcontrol"></a>将 MediaPlayer 属性添加到 FirstToolWindowControl
从工具栏控件的事件处理程序中，代码必须能够访问 Media Player 控件，该控件是 FirstToolWindowControl 类的子级。

在 **解决方案资源管理器** 中，右键单击 *"FirstToolWindowControl.xaml"，* 单击"查看代码"，将以下代码添加到 FirstToolWindowControl 类。 

```csharp
public System.Windows.Controls.MediaElement MediaPlayer
{
    get { return mediaElement1; }
}
```

## <a name="instantiate-the-tool-window-and-toolbar"></a>实例化工具窗口和工具栏
添加一个工具栏和一个菜单命令，用于调用"打开 **文件** "对话框并播放选定的媒体文件。

1. 打开 *FirstToolWindow.cs* 并添加以下 `using` 指令：

    ```csharp
    using System.ComponentModel.Design;
    using System.Windows.Forms;
    using Microsoft.VisualStudio.Shell.Interop;
    ```

2. 在 FirstToolWindow 类中，添加对 FirstToolWindowControl 控件的公共引用。

    ```csharp
    public FirstToolWindowControl control;
    ```

3. 在构造函数的末尾，将此控件变量设置为新创建的控件。

    ```csharp
    control = new FirstToolWindowControl();
    base.Content = control;
    ```

4. 实例化构造函数内的工具栏。

    ```csharp
    this.ToolBar = new CommandID(new Guid(FirstToolWindowCommand.guidFirstToolWindowPackageCmdSet),
        FirstToolWindowCommand.ToolbarID);
    this.ToolBarLocation = (int)VSTWT_LOCATION.VSTWT_TOP;
    ```

5. 此时，FirstToolWindow 构造函数应如下所示：

    ```csharp
    public FirstToolWindow() : base(null)
    {
        this.Caption = "FirstToolWindow";
        this.BitmapResourceID = 301;
        this.BitmapIndex = 1;
        control = new FirstToolWindowControl();
        base.Content = control;
        this.ToolBar = new CommandID(new Guid(FirstToolWindowCommand.guidFirstToolWindowPackageCmdSet),
            FirstToolWindowCommand.ToolbarID);
            this.ToolBarLocation = (int)VSTWT_LOCATION.VSTWT_TOP;
    }
    ```

6. 将菜单命令添加到工具栏。 在 FirstToolWindowCommand.cs 类中，添加以下 using 指令：

    ```csharp
    using System.Windows.Forms;
    ```

7. 在 FirstToolWindowCommand 类中，将以下代码添加到 ShowToolWindow () 末尾。 ButtonHandler 命令将在下一部分中实现。

    ```csharp
    // Create the handles for the toolbar command.
    var mcs = this.ServiceProvider.GetService(typeof(IMenuCommandService)) as OleMenuCommandService;
    var toolbarbtnCmdID = new CommandID(new Guid(FirstToolWindowCommand.guidFirstToolWindowPackageCmdSet),
        FirstToolWindowCommand.cmdidWindowsMediaOpen);
    var menuItem = new MenuCommand(new EventHandler(
        ButtonHandler), toolbarbtnCmdID);
    mcs.AddCommand(menuItem);
    ```

### <a name="to-implement-a-menu-command-in-the-tool-window"></a>在工具窗口中实现菜单命令

1. 在 FirstToolWindowCommand 类中，添加调用"打开文件"对话框的 ButtonHandler **方法。** 选择文件后，它播放媒体文件。

2. 在 FirstToolWindowCommand 类中，添加对在 FindToolWindow () 中创建的 FirstToolWindow 窗口的私有引用。

    ```csharp
    private FirstToolWindow window;
    ```

3. 更改 ShowToolWindow () 方法以设置上面定义的窗口 (以便 ButtonHandler 命令处理程序可以访问窗口控件。 下面是完整的 ShowToolWindow () 方法。

    ```csharp
    private void ShowToolWindow(object sender, EventArgs e)
    {
        window = (FirstToolWindow) this.package.FindToolWindow(typeof(FirstToolWindow), 0, true);
        if ((null == window) || (null == window.Frame))
        {
            throw new NotSupportedException("Cannot create tool window");
        }

        IVsWindowFrame windowFrame = (IVsWindowFrame)window.Frame;
        Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure(windowFrame.Show());

        var mcs = this.ServiceProvider.GetService(typeof(IMenuCommandService)) as OleMenuCommandService;
        var toolbarbtnCmdID = new CommandID(new Guid(FirstToolWindowCommandguidFirstToolWindowPackageCmdSet),
            FirstToolWindowCommand.cmdidWindowsMediaOpen);
        var menuItem = new MenuCommand(new EventHandler(
            ButtonHandler), toolbarbtnCmdID);
        mcs.AddCommand(menuItem);
    }
    ```

4. 添加 ButtonHandler 方法。 它会创建一个 OpenFileDialog，供用户指定要播放的媒体文件，然后播放所选文件。

    ```csharp
    private void ButtonHandler(object sender, EventArgs arguments)
    {
        OpenFileDialog openFileDialog = new OpenFileDialog();
        DialogResult result = openFileDialog.ShowDialog();
        if (result == DialogResult.OK)
        {
            window.control.MediaPlayer.Source = new System.Uri(openFileDialog.FileName);
        }
    }
    ```

## <a name="set-the-default-position-for-the-tool-window"></a>设置工具窗口的默认位置

接下来，在 IDE 中为工具窗口指定默认位置。 工具窗口的配置信息位于 *FirstToolWindowPackage.cs* 文件中。

1. 在 *FirstToolWindowPackage.cs* 中，查找 类上的 属性，该属性将 <xref:Microsoft.VisualStudio.Shell.ProvideToolWindowAttribute> `FirstToolWindowPackage` FirstToolWindow 类型传递给构造函数。 若要指定默认位置，必须将更多参数添加到以下示例的构造函数。

    ```csharp
    [ProvideToolWindow(typeof(FirstToolWindow),
        Style = Microsoft.VisualStudio.Shell.VsDockStyle.Tabbed,
        Window = "3ae79031-e1bc-11d0-8f78-00a0c9110057")]
    ```

    第一个命名参数为 `Style` ，其值为 `Tabbed` ，这意味着窗口将是现有窗口中的选项卡。 停靠位置由 参数（本例中为 `Window` ）指定，解决方案资源管理器。 

    > [!NOTE]
    > 有关 IDE 中窗口类型的信息，请参阅 <xref:EnvDTE.vsWindowType> 。

## <a name="test-the-tool-window"></a>测试工具窗口

1. 按 **F5** 打开试验性Visual Studio实例。

2. 在"**视图"** 菜单上，指向"**其他Windows，** 然后单击"第 **一个工具窗口"。**

    媒体播放器工具窗口应与 打开 **解决方案资源管理器。** 如果窗口布局仍与以前相同，请重置窗口布局 **(/重置窗口布局) 。**

3. 单击按钮 (**工具窗口中有** "搜索) 图标。 选择受支持的声音或视频文件，例如 *C：\windows\media\wav，* 然后按 **"打开"。**

    应会听到声音。

## <a name="see-also"></a>请参阅
- [命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)

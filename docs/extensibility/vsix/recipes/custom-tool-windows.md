---
title: 生成自定义工具窗口
description: 如何将自定义工具窗口添加到 Visual Studio。
ms.date: 12/01/2021
ms.topic: conceptual
author: madskristensen
ms.author: madsk
manager: pchapman
ms.prod: visual-studio-windows
ms.technology: vs-ide-sdk
ms.custom: cookbook
ms.openlocfilehash: c7080bcb279d5ca50477f7efdf5d51f9340be576
ms.sourcegitcommit: a149b3a034bb555ad217656c0ec8bc1672b1e215
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2021
ms.locfileid: "133515863"
---
# <a name="build-custom-tool-windows"></a>生成自定义工具窗口

自定义工具窗口是向应用程序添加复杂 UI Visual Studio。

工具窗口是工具窗口中的核心 UI Visual Studio，以下视频将展示如何添加自定义窗口。

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RWPhtK]

工具窗口是一个可以四处移动和停靠的窗口，就像解决方案资源管理器、错误列表和其他已知工具窗口一样。 工具窗口由 Visual Studio 提供的外部 shell 和一个自定义内部 UI 控件（通常是扩展提供的 `<usercontrol>` XAML） 组成。

>[!NOTE]
> 若要使用工具窗口创建新扩展，请通过 **VSIX Project/** 工具窗口 (Community) 模板创建新项目，并跳过此方案的其余部分。 有关详细信息 [，](../get-started/first-extension.md) 请参阅入门。

将工具窗口添加到现有扩展需要 4 个简单的步骤：

1. 创建工具窗口外部 shell 类。
2. 将 XAML `<usercontrol>` 添加到工具窗口。
3. 注册工具窗口。
4. 创建一个命令以显示工具窗口。

让我们从步骤 1 开始。

## <a name="create-the-tool-window"></a>创建工具窗口
使用 `BaseToolWindow<T>` 泛型基类时，需要提供一些基本信息片段。 必须指定工具窗口的标题，创建并返回 XAML 用户控件，并设置 Visual Studio 用于创建窗口 `ToolWindowPane` 的外部 shell 的实际类。

```csharp
using System;
using System.Runtime.InteropServices;
using System.Threading;
using System.Threading.Tasks;
using System.Windows;
using Community.VisualStudio.Toolkit;
using EnvDTE80;
using Microsoft.VisualStudio.Imaging;
using Microsoft.VisualStudio.Shell;

public class MyToolWindow : BaseToolWindow<MyToolWindow>
{
    public override string GetTitle(int toolWindowId) => "My Tool Window";

    public override Type PaneType => typeof(Pane);

    public override async Task<FrameworkElement> CreateAsync(int toolWindowId, CancellationToken cancellationToken)
    {
        await Task.Delay(2000); // Long running async task
        return new MyUserControl();
    }

    // Give this a new unique guid
    [Guid("d3b3ebd9-87d1-41cd-bf84-268d88953417")] 
    internal class Pane : ToolWindowPane
    {
        public Pane()
        {
            // Set an image icon for the tool window
            BitmapImageMoniker = KnownMonikers.StatusInformation;
        }
    }
}
```

必须从 方法创建自定义用户控件的实例，然后，当工具窗口 shell 由用户创建时，该实例 `CreateAsync(int, CancellationToken)` Visual Studio。

但首先，必须创建用户控件。

## <a name="add-the-xaml-user-control"></a>添加 XAML 用户控件
它可以是任何 XAML 及其代码隐藏类，因此下面是包含单个按钮 `<usercontrol>` 的 的简单示例：

```xml
<UserControl x:Class="MyUserControl"
             xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
             xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
             xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
             xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
             xmlns:toolkit="clr-namespace:Community.VisualStudio.Toolkit;assembly=Community.VisualStudio.Toolkit"
             mc:Ignorable="d"
             toolkit:Themes.UseVsTheme="True"
             d:DesignHeight="300" d:DesignWidth="300"
             Name="MyToolWindow">
    <Grid>
        <StackPanel Orientation="Vertical">
            <Label Margin="10" HorizontalAlignment="Center">My Window</Label>
            <Button Content="Click me!" Click="button1_Click" Width="120" Height="80" Name="button1"/>
        </StackPanel>
    </Grid>
</UserControl>
```

现在，我们有一个返回自定义控件的工具窗口类。 下一步是将工具窗口注册到 Visual Studio。

## <a name="register-the-tool-window"></a>注册工具窗口
注册工具窗口意味着我们要告知Visual Studio及其实例化方式。 我们使用 属性从包类 `[ProvideToolWindow]` 中执行此工作。

```csharp
[ProvideToolWindow(typeof(MyToolWindow.Pane))]
public sealed class MyPackage : ToolkitPackage
{
     protected override async Task InitializeAsync(CancellationToken cancellationToken, IProgress<ServiceProgressData> progress)
     {
         this.RegisterToolWindows();
     }
}
```

>[!NOTE]
> 请注意，包类必须从 继承 `ToolkitPackage` ，而不是从 `Package` 或 继承 `AsyncPackage` 。

可以指定工具窗口应具有的样式以及默认应显示的位置。 以下示例显示工具窗口应放置在链接样式中解决方案资源管理器停靠容器中。

```csharp
[ProvideToolWindow(typeof(MyToolWindow.Pane), Style = VsDockStyle.Linked, Window = WindowGuids.SolutionExplorer)]
```

若要使工具窗口默认可见，可以使用 属性在不同的 UI 上下文中指定其 `[ProvideToolWindowVisibility]` 可见性。

```csharp
[ProvideToolWindowVisibility(typeof(MyToolWindow.Pane), VSConstants.UICONTEXT.NoSolution_string)]
```

## <a name="command-to-show-the-tool-window"></a>用于显示工具窗口的命令
这与其他任何命令相同，可以在"菜单"和"命令"脚本 [&添加一个](menus-buttons-commands.md)。

显示工具窗口的命令处理程序类将如下所示：

```csharp
using Community.VisualStudio.Toolkit;
using Microsoft.VisualStudio.Shell;
using Task = System.Threading.Tasks.Task;

[Command(PackageIds.RunnerWindow)]
internal sealed class MyToolWindowCommand : BaseCommand<MyToolWindowCommand>
{
    protected override async Task ExecuteAsync(OleMenuCmdEventArgs e) =>
        await MyToolWindow.ShowAsync();
}
```

工具窗口的命令位置通常位于主菜单中的"视图 **>""** 其他Windows"下。

完成了。 恭喜，现已创建自定义工具窗口。

## <a name="get-the-source-code"></a>获取源代码
可以在示例存储库中找到此配方 [的源代码](https://github.com/VsixCommunity/Samples/tree/master/ToolWindow)。

---
title: 将用户控件添加到起始页|Microsoft Docs
description: 了解如何将 WPF Windows Presentation Foundation (用户) 添加到"开始"页Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- start page dll
- custom start page
- start page assembly
ms.assetid: 5b7997db-af6f-4fa9-a128-bceb42bddaf1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 794ff65d58e03b22584f0a4d2a291371b1e08c81
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664637"
---
# <a name="add-user-control-to-the-start-page"></a>将用户控件添加到起始页

本演练演示如何向自定义起始页添加 DLL 引用。 该示例将用户控件添加到解决方案，生成用户控件，然后从起始页 *.xaml* 文件引用生成程序集。 新选项卡承载用户控件，该控件用作基本 Web 浏览器。

可以使用同一过程添加可以从 *.xaml* 文件调用的任何程序集。

## <a name="add-a-wpf-user-control-to-the-solution"></a>将 WPF 用户控件添加到解决方案

首先，将 Windows Presentation Foundation (WPF) 用户控件添加到起始页解决方案。

1. 使用在创建自定义起始页 中创建的 [创建起始页](../extensibility/creating-a-custom-start-page.md)。

2. 在 **解决方案资源管理器** 中，右键单击解决方案，单击 **"添加**"，然后单击"**新建Project"。**

3. 在 "新建Project对话框的左窗格中，展开 Visual Basic 或 Visual  **C#** 节点，然后单击 "Windows"。  在中间窗格中，选择 **"WPF 用户控件库"。**

4. 将控件命名， `WebUserControl` 然后单击"确定 **"。**

## <a name="implement-the-user-control"></a>实现用户控件

若要实现 WPF 用户控件，请 (XAML) UI 控件的用户界面，然后以 C# 或其他 .NET 语言编写代码隐藏事件。

### <a name="to-write-the-xaml-for-the-user-control"></a>为用户控件编写 XAML

1. 打开用户控件的 XAML 文件。 在 `<Grid>` 元素中，将以下行定义添加到 控件。

    ```vb
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="*" />
    </Grid.RowDefinitions>

    ```

2. 在 main 元素中，添加以下新元素，其中包含用于键入 Web 地址的文本框和用于设置新 `<Grid>` `<Grid>` 地址的按钮。

    ```xml
    <Grid Grid.Row="0">
        <Grid.ColumnDefinitions>
            <ColumnDefinition Width="*" />
            <ColumnDefinition Width="Auto" />
        </Grid.ColumnDefinitions>
        <TextBox x:Name="UserSource" Grid.Column="0" />
        <Button Grid.Column="1" x:Name="SetButton" Content="Set Address" Click="SetButton_Click" />
    </Grid>
    ```

3. 在包含按钮和文本框的元素之后，将以下帧添加到顶级 `<Grid>` `<Grid>` 元素。

    ```vb
    <Frame Grid.Row="1" x:Name="WebFrame" Source="http://www.bing.com" Navigated="WebFrame_Navigated" />
    ```

4. 以下示例演示用户控件的已完成 XAML。

    ```xml
    <UserControl x:Class="WebUserControl.UserControl1"
                 xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
                 xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
                 xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
                 xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
                 mc:Ignorable="d"
                 d:DesignHeight="300" d:DesignWidth="300">
        <Grid>
            <Grid.RowDefinitions>
                <RowDefinition Height="Auto"/>
                <RowDefinition Height="*" />
            </Grid.RowDefinitions>
            <Grid Grid.Row="0">
                <Grid.ColumnDefinitions>
                    <ColumnDefinition Width="*" />
                    <ColumnDefinition Width="Auto" />
                </Grid.ColumnDefinitions>
                <TextBox x:Name="UserSource" Grid.Column="0" />
                <Button Grid.Column="1" x:Name="SetButton" Content="Set Address" Click="SetButton_Click" />
            </Grid>
            <Frame Grid.Row="1" x:Name="WebFrame" Source="http://www.bing.com" Navigated="WebFrame_Navigated" />
        </Grid>
    </UserControl>

    ```

### <a name="to-write-the-code-behind-events-for-the-user-control"></a>为用户控件编写代码隐藏事件

1. 在 XAML 设计器中，双击添加到 **控件** 的"设置地址"按钮。

    *UserControl1.cs 文件* 将在代码编辑器中打开。

2. 按如下所示SetButton_Click事件处理程序。

    ```csharp
    private void SetButton_Click(object sender, RoutedEventArgs e)
    {
        try
        {
            this.WebFrame.Source = new Uri(this.UserSource.Text, UriKind.Absolute);
        }
        catch (Exception error)
        {
            MessageBox.Show(error.Message);
        }
    }
    ```

    此代码将文本框中键入的 Web 地址设置为 Web 浏览器的目标。 如果地址无效，代码将引发错误。

3. 还必须处理WebFrame_Navigated事件：

    ```csharp
    private void WebFrame_Navigated(object sender, EventArgs e)
    { }
    ```

4. 生成解决方案。

## <a name="add-the-user-control-to-the-start-page"></a>将用户控件添加到起始页

若要使此控件可用于起始页项目，在起始页项目文件中，添加对新控件库的引用。 然后，可以将 控件添加到起始页 XAML 标记。

1. 在 **解决方案资源管理器** 中，在"起始页"项目中，右键单击"引用 **"，然后单击**"**添加引用"。**

2. 在"**项目"选项卡上**，选择 **"WebUserControl"，** 然后单击"确定 **"。**

3. 在 **“生成”** 菜单上，单击 **“生成解决方案”** 。

    生成解决方案后，IntelliSense 可以针对解决方案中其他文件使用用户控件。

    若要将控件添加到起始页 XAML 标记，请添加对程序集的命名空间引用，然后将控件放在页面上。

### <a name="to-add-the-control-to-the-markup"></a>将 控件添加到标记

1. 在 **解决方案资源管理器** 中，打开起始页 *.xaml* 文件。

2. 在 **"XAML"** 窗格中，将以下命名空间声明添加到顶级 <xref:System.Windows.Controls.Grid> 元素。

   ```xml
   xmlns:vsc="clr-namespace:WebUserControl;assembly=WebUserControl"
   ```

3. 在 **"XAML"** 窗格中，滚动到 \<Grid> 部分。

    部分包含 <xref:System.Windows.Controls.TabControl> 元素中的 <xref:System.Windows.Controls.Grid> 元素。

4. 添加 \<TabControl> 一个 元素， \<TabItem> 该元素包含对用户控件的引用。

    ```xml

    <TabItem Header="Web" Height="Auto">
        <vsc:UserControl1 />
    </TabItem>

    ```

    现在，可以测试控件。

## <a name="test-a-manually-created-custom-start-page"></a>测试手动创建的自定义起始页

1. 将 XAML 文件以及任何支持文本文件或标记文件复制到 *%USERPROFILE%\我的文档\Visual Studio 2015\StartPages \\* 文件夹。

2. 如果起始页引用程序集中未由 Visual Studio 安装的任何控件或类型，请复制这些程序集，然后将其粘贴到 _Visual Studio 安装文件夹_**\\ \Common7\IDE\PrivateAssemblies** 中。

3. 在命令Visual Studio，键入 **devenv /rootsuffix Exp** 以打开 Visual Studio。

4. 在实验实例中，转到"工具""选项""环境启动"页，然后从"自定义起始页"下拉列表中选择  >    >    >  XAML 文件。 

5. 在“视图”  菜单上，单击“起始页” 。

    应显示自定义起始页。 如果要更改任何文件，则必须关闭实验实例，进行更改，复制并粘贴更改的文件，然后重新打开实验实例以查看更改。

## <a name="see-also"></a>另请参阅

- [WPF 容器控件](/previous-versions/bb675291(v=vs.110))
- [演练：将自定义 XAML 添加到起始页](../extensibility/walkthrough-adding-custom-xaml-to-the-start-page.md)
---
title: 演练：在起始设置保存用户|Microsoft Docs
description: 了解如何通过使用本演练将设置保存到注册表，从而保留起始页的用户设置。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 754b9bf3-8681-4c77-b0a4-09146a4e1d2d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 3f312bb9b62ebbcc694a64ad485d19ca628b1e8e
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602322"
---
# <a name="walkthrough-save-user-settings-on-a-start-page"></a>演练：在起始页上保存用户设置

可以保留起始页的用户设置。 按照本演练操作，可以创建一个控件，该控件在用户单击按钮时将设置保存到注册表，然后每次加载起始页时检索该设置。 由于起始页项目模板包含可自定义的用户控件，以及默认的起始页 XAML 调用该控件，因此不必修改起始页本身。

本演练中实例化的设置存储是 接口的实例，该接口在调用 时读取和写入以下注册表 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWritableSettingsStore> 位置 **：HKCU\Software\Microsoft\VisualStudio\14.0 \\ \<CollectionName>**

在 Visual Studio 试验实例中运行时，设置存储对 **HKCU\Software\Microsoft\VisualStudio\14.0Exp 进行读取和写入 \\ \<CollectionName> 。**

若要详细了解如何保留设置，请参阅[扩展用户设置选项](../extensibility/extending-user-settings-and-options.md)。

## <a name="prerequisites"></a>先决条件

> [!NOTE]
> 要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅 [Visual Studio SDK](../extensibility/visual-studio-sdk.md)。
>
> 可以使用扩展管理器 下载起始页 **项目模板**。

## <a name="set-up-the-project"></a>设置项目

1. 如创建自定义起始页 中所述， [创建起始页项目](creating-a-custom-start-page.md)。 将项目命名 **SaveMySettings**。

2. 在 **解决方案资源管理器** 中，将以下程序集引用添加到 StartPageControl 项目：

    - EnvDTE

    - EnvDTE80

    - Microsoft.VisualStudio.OLE.Interop

    - Microsoft.VisualStudio.Shell.Interop.11.0

3. 打开 *MyControl.xaml*。

4. 在"XAML"窗格的顶级元素定义中，在命名空间声明 <xref:System.Windows.Controls.UserControl> 后添加以下事件声明。

    ```xml
    Loaded="OnLoaded"
    ```

5. 在设计窗格中，单击控件的主区域，然后按"删除 **"。**

     此步骤将删除 元素及其中 <xref:System.Windows.Controls.Border> 所有内容，并仅保留顶级 <xref:System.Windows.Controls.Grid> 元素。

6. 从" **工具箱"** 中， <xref:System.Windows.Controls.StackPanel> 将控件拖动到网格。

7. 现在， <xref:System.Windows.Controls.TextBlock> 将 、 和 <xref:System.Windows.Controls.TextBox> 按钮拖动到 <xref:System.Windows.Controls.StackPanel> 。

8. 为 **添加 x：Name** 属性，为 添加 事件 <xref:System.Windows.Controls.TextBox> `Click` <xref:System.Windows.Controls.Button> ，如以下示例所示。

    ```xml
    <StackPanel Width="300" HorizontalAlignment="Center" VerticalAlignment="Center">
        <TextBlock Width="140" FontSize="14">Enter your setting</TextBlock>
        <TextBox x:Name="txtblk" Margin="0, 5, 0, 10" Width="140" />
        <Button Click="Button_Click" Width="100">Save My Setting</Button>
    </StackPanel>
    ```

## <a name="implement-the-user-control"></a>实现用户控件

1. 在"XAML"窗格中，右键单击 元素的 属性，然后单击 `Click` <xref:System.Windows.Controls.Button> "**导航到事件处理程序"。**

     此步骤将 *打开 MyControl.xaml.cs*，并创建事件的存根 `Button_Click` 处理程序。

2. 将以下 `using` 指令添加到文件顶部。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/startpagedte/cs/startpagecontrol/mycontrol.xaml.cs" id="Snippet11":::

3. 添加私有 `SettingsStore` 属性，如以下示例所示。

    ```csharp
    private IVsWritableSettingsStore _settingsStore = null;
    private IVsWritableSettingsStore SettingsStore
    {
        get
        {
            if (_settingsStore == null)
            {
                // Get a reference to the DTE from the DataContext.
                var typeDescriptor = DataContext as ICustomTypeDescriptor;
                var propertyCollection = typeDescriptor.GetProperties();
                var dte = propertyCollection.Find("DTE", false).GetValue(
                    DataContext) as DTE2;

                // Get the settings manager from the DTE.
                var serviceProvider = new ServiceProvider(
                    (Microsoft.VisualStudio.OLE.Interop.IServiceProvider)dte);
                var settingsManager = serviceProvider.GetService(
                    typeof(SVsSettingsManager)) as IVsSettingsManager;

                // Write the user settings to _settingsStore.
                settingsManager.GetWritableSettingsStore(
                    (uint)__VsSettingsScope.SettingsScope_UserSettings,
                    out _settingsStore);
            }
            return _settingsStore;
        }
    }
    ```

     此属性首先从用户控件的 获取对包含自动化对象模型的 接口的引用，然后使用 DTE 获取接口 <xref:EnvDTE80.DTE2> <xref:System.Windows.FrameworkElement.DataContext%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSettingsManager> 的实例。 然后，它使用该实例返回当前用户设置。

4. 按如下所示 `Button_Click` 填写 事件。

    ```csharp
    private void Button_Click(object sender, RoutedEventArgs e)
    {
        int exists = 0;
        SettingsStore.CollectionExists("MySettings", out exists);
        if (exists != 1)
        {
            SettingsStore.CreateCollection("MySettings");
        }
        SettingsStore.SetString("MySettings", "MySetting", txtblk.Text);
    }
    ```

     这会将文本框的内容写入注册表中"MySettings"集合中的"MySetting"字段。 如果集合不存在，则创建它。

5. 为用户控件 `OnLoaded` 的 事件添加以下处理程序。

    ```csharp
    private void OnLoaded(Object sender, RoutedEventArgs e)
    {
        string value;
        SettingsStore.GetStringOrDefault(
            "MySettings", "MySetting", "", out value);
        txtblk.Text = value;
    }
    ```

     此代码将文本框的文本设置为"MySetting"的当前值。

6. 生成用户控件。

7. 在 **解决方案资源管理器** 中，打开 *source.extension.vsixmanifest*。

8. 在清单编辑器中，将 **"产品名称"设置为****"保存我的设置起始页"。**

     此功能设置起始页的名称，因为它将显示在"选项"对话框中的"自定义起始 **页"** 列表中。 

9. 生成 *StartPage.xaml*。

## <a name="test-the-control"></a>测试控件

1. 按 **F5**。

     将打开 Visual Studio实例。

2. 在实验实例的"工具"**菜单上**，单击"选项 **"。**

3. 在"**环境"** 节点中 **，单击**"启动"，然后在"自定义起始页"列表中，选择"[已安装的扩展] 保存我的设置 **起始页"。**

     单击“确定”。

4. 如果"起始页"已打开，请关闭"起始页"，然后在"视图 **"** 菜单上单击"**起始页"。**

5. 在"起始页"中，单击 **"MyControl"** 选项卡。

6. 在文本框中，键入 **"Cat"，** 然后单击"**保存我的设置"。**

7. 关闭起始页，然后再次打开它。

     文本框中应显示单词"Cat"。

8. 将单词"Cat"替换为单词"Dog"。 请勿单击按钮。

9. 关闭起始页，然后再次打开它。

     即使未保存设置，"Dog"一词也应显示在文本框中，因为 Visual Studio 将工具窗口保存在内存中，即使它们已关闭，直到 Visual Studio 本身关闭。

10. 关闭 Visual Studio 的实验实例。

11. 按 **F5** 重新打开实验实例。

12. 文本框中应显示单词"Cat"。

## <a name="next-steps"></a>后续步骤

可以通过使用不同的事件处理程序中的不同值来修改此用户控件，以保存和检索任意数目的自定义设置，以获取和设置 `SettingsStore` 属性。 只要每次调用 使用不同的参数，值就不会在注册表中相互 `propertyName` <xref:Microsoft.VisualStudio.Shell.Interop.IVsWritableSettingsStore.SetString%2A> 覆盖。

## <a name="see-also"></a>另请参阅

- <xref:EnvDTE80.DTE2?displayProperty=fullName>
- [将Visual Studio添加到起始页](../extensibility/adding-visual-studio-commands-to-a-start-page.md)

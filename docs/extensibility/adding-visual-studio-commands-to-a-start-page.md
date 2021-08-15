---
title: 将Visual Studio命令添加到起始页|Microsoft Docs
description: 了解在自定义起始Visual Studio中将命令绑定到 XAML 对象的不同Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- start page commands
- vs:VSCommands
ms.assetid: a8e2765c-cfb5-47b5-a414-6e48b434e0c2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 9ab2fc534b2ef986b15102667bd23e108ea4c69256fe64516b0df08595b1157c
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121403497"
---
# <a name="add-visual-studio-commands-to-a-start-page"></a>将Visual Studio添加到起始页

创建自定义起始页时，可以将Visual Studio添加到该起始页。 本文档讨论将命令绑定到起始Visual Studio XAML 对象的不同方法。

有关 XAML 中的命令详细信息，请参阅 [命令概述](/dotnet/framework/wpf/advanced/commanding-overview)

## <a name="add-commands-from-the-command-well"></a>从命令井添加命令

在创建自定义起始 [页中创建](../extensibility/creating-a-custom-start-page.md) 的起始页添加了 和 <xref:Microsoft.VisualStudio.PlatformUI?displayProperty=fullName> <xref:Microsoft.VisualStudio.Shell?displayProperty=fullName> 命名空间，如下所示。

```xml
xmlns:vs="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.14.0"
xmlns:vsfx="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.14.0"
```

从 程序集为 Microsoft.VisualStudio.Shell 添加另 *一Microsoft.VisualStudio.Shell.Immutable.11.0.dll。*  (可能需要在 project.) 中添加对此程序集的引用。

```xml
xmlns:vscom="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.Immutable.11.0"
```

通过将 控件的 属性Visual Studio，可以使用 别名将命令绑定到页面上 `vscom:` 的 XAML <xref:System.Windows.Controls.Primitives.ButtonBase.Command%2A> 控件 `vscom:VSCommands.ExecuteCommand` 。 然后，可以将 <xref:System.Windows.Controls.Primitives.ButtonBase.CommandParameter%2A> 属性设置为要执行的命令的名称，如以下示例所示。

```xml
<Button Name="btnNewProj" Content="New Project"
    Command="{x:Static vscom:VSCommands.ExecuteCommand}"
    CommandParameter="File.NewProject" >
</Button>
```

> [!NOTE]
> 所有命令的开头都需要别名（即 `x:` XAML 架构）。

 可以将 属性的值设置为任何可以从"命令"窗口 `Command` **访问的命令** 。 有关可用命令的列表，请参阅Visual Studio[别名](../ide/reference/visual-studio-command-aliases.md)。

 如果要添加的命令需要其他参数，可以将其添加到 属性的值 `CommandParameter` 。 使用空格将参数与命令分开，如以下示例所示。

```xml
<Button Content="Web Search"
        Command="{x:Static vscom:VSCommands.ExecuteCommand}"
        CommandParameter="View.WebBrowser www.bing.com" />
```

### <a name="call-extensions-from-the-command-well"></a>从命令井调用扩展
 可以使用用于调用其他命令的相同语法从已注册的 VSPackage Visual Studio命令。 例如，如果安装的 VSPackage 将"主页"命令添加到"视图"菜单，则可以通过将 设置为 来调用 `CommandParameter` 该命令 `View.HomePage` 。

> [!NOTE]
> 如果调用与 VSPackage 关联的命令，则必须在调用命令时加载包。

## <a name="add-commands-from-assemblies"></a>从程序集添加命令
 若要从程序集调用命令，或者访问与菜单命令不关联的 VSPackage 中的代码，必须为程序集创建别名，然后调用别名。

### <a name="to-call-a-command-from-an-assembly"></a>从程序集调用命令

1. 在解决方案中，添加对程序集的引用。

2. 在 *StartPage.xaml* 文件的顶部，为程序集添加命名空间指令，如以下示例所示。

    ```xml
    xmlns:vsc="clr-namespace:WebUserControl;assembly=WebUserControl"
    ```

3. 通过设置 XAML 对象的 属性来调用 命令 `Command` ，如以下示例所示。

     Xaml

    ```
    <vs:Button Text="Hide me" Command="{x:Static vsc:HideControl}" .../>
    ```

> [!NOTE]
> 必须复制程序集，然后将其粘贴到 *.中。 \\{Visual Studio安装文件夹}\Common7\IDE\PrivateAssemblies，以确保在调用之前 \* 加载它。

## <a name="add-commands-with-the-dte-object"></a>使用 DTE 对象添加命令
 可以在标记和代码中从起始页访问 DTE 对象。

 在标记中，可以使用绑定标记 [扩展语法调用](/dotnet/framework/wpf/advanced/binding-markup-extension) 对象来访问 <xref:EnvDTE.DTE> 它。 可以此方法绑定到简单属性，例如返回集合的属性，但不能绑定到方法或服务。 下面的示例演示一个绑定到 属性的 控件，以及一个枚举 由 属性返回的集合 <xref:System.Windows.Controls.TextBlock> <xref:EnvDTE._DTE.Name%2A> <xref:System.Windows.Controls.ListBox> <xref:EnvDTE.Window.Caption%2A> 属性的 <xref:EnvDTE._DTE.Windows%2A> 控件。

```xml
<TextBlock Text="{Binding Path=DTE.Name}" FontSize="12" HorizontalAlignment="Center"/>
<ListBox ItemsSource="{Binding Path=DTE.Windows}">
    <ListBox.ItemTemplate>
        <DataTemplate>
            <TextBlock Text="{Binding Path=Caption}"/>
        </DataTemplate>
    </ListBox.ItemTemplate>
</ListBox
```

 有关示例，请参阅 [演练：在起始页上保存用户设置](../extensibility/walkthrough-saving-user-settings-on-a-start-page.md)。

## <a name="see-also"></a>另请参阅

- [将用户控件添加到起始页](../extensibility/adding-user-control-to-the-start-page.md)

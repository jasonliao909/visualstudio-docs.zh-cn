---
title: 创建自定义起始页|Microsoft Docs
description: 了解如何创建自定义起始页。 从空白起始页开始，将控件添加到空的 UserControl 元素，然后测试页面。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: d67e0c53-9f5a-45fb-a929-b9d2125c3c82
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 34e8f64b0007231ef3c5208d7020d415d65e6d67
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600992"
---
# <a name="creating-a-custom-start-page"></a>创建自定义起始页

可以按照本文档中的步骤创建自定义起始页。

## <a name="create-a-blank-start-page"></a>创建空白起始页

首先，创建一个 *.xaml* 文件，该文件具有一个标记结构，Visual Studio起始页。 然后，添加标记和代码隐藏，以生成所需的外观和功能。

1. 在 **Visual C#** 桌面桌面 (创建类型为 **"WPF**  >  **应用程序Windows) 。**

2. 添加对 `Microsoft.VisualStudio.Shell.14.0` 的引用。

3. 在 XML 编辑器中打开 XAML 文件，将顶级元素更改为 元素，而不删除 \<Window> \<UserControl> 任何命名空间声明。

4. 从 `x:Class` 顶级元素中删除 声明。 这使得 XAML 内容与托管起始页Visual Studio工具窗口兼容。

5. 将以下命名空间声明添加到顶级 \<UserControl> 元素。

    ```vb
    xmlns:vs="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.14.0"
    xmlns:vsfx="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.14.0"
    ```

     这些命名空间允许访问Visual Studio控件和 UI 设置。 有关详细信息，请参阅向起始[Visual Studio添加命令](../extensibility/adding-visual-studio-commands-to-a-start-page.md)。

     以下示例显示了空白起始页 *的 .xaml* 文件中标记。 任何自定义内容都应进入内部 <xref:System.Windows.Controls.Grid> 元素中。

    ```vb
    <UserControl
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:MyNamespace="clr-namespace:ManualStartPage;assembly=ManualStartPage"
        xmlns:vs="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.14.0"
                xmlns:vsfx="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.14.0"
        xmlns:local="clr-namespace:StartPageHost"
        mc:Ignorable="d"
         Height="350" Width="525">
        <Grid>
        <!--Add content here.-->
        </Grid>
    </UserControl>
    ```

6. 将控件添加到空 \<UserControl> 元素以填充自定义起始页。 若要了解如何添加特定于 Visual Studio 的功能，请参阅将 Visual Studio[命令添加到起始页](../extensibility/adding-visual-studio-commands-to-a-start-page.md)。

## <a name="test-and-apply-the-custom-start-page"></a>测试并应用自定义起始页

在验证自定义起始页未Visual Studio之前，请不要设置该页的主Visual Studio。 相反，在实验实例中测试它。

### <a name="to-test-a-manually-created-custom-start-page"></a>测试手动创建的自定义起始页

1. 将 XAML 文件以及任何支持文本文件或标记文件复制到 *%USERPROFILE%\我的文档\Visual Studio 2015\StartPages \\* 文件夹。

2. 如果起始页引用程序集中未由 Visual Studio 安装的任何控件或类型，请复制这些程序集，然后将其粘贴到 *{Visual Studio installation \\ folder}\Common7\IDE\PrivateAssemblies* 中。

3. 在命令Visual Studio，键入 **devenv /rootsuffix Exp** 以打开 Visual Studio。

4. 在实验实例中，转到"工具""选项""环境启动"页，然后从"自定义起始页"下拉列表中选择  >    >    >  XAML 文件。 

5. 在“视图”  菜单上，单击“起始页” 。

     应显示自定义起始页。 如果要更改任何文件，则必须关闭实验实例，进行更改，复制并粘贴更改的文件，然后重新打开实验实例以查看更改。

### <a name="to-apply-the-custom-start-page-in-the-primary-instance-of-visual-studio"></a>在主实例中应用自定义起始页Visual Studio

- 测试起始页并发现起始页稳定后，使用"选项"对话框中的"自定义起始页"选项将其选作主实例中的起始Visual Studio

## <a name="see-also"></a>另请参阅

- [演练：将自定义 XAML 添加到起始页](../extensibility/walkthrough-adding-custom-xaml-to-the-start-page.md)
- [将用户控件添加到起始页](../extensibility/adding-user-control-to-the-start-page.md)
- [将Visual Studio添加到起始页](../extensibility/adding-visual-studio-commands-to-a-start-page.md)
- [演练：在起始页上保存用户设置](../extensibility/walkthrough-saving-user-settings-on-a-start-page.md)
- [部署自定义起始页](../extensibility/deploying-custom-start-pages.md)

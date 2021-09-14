---
title: 创建 WPF 工具箱控件|Microsoft Docs
description: 了解如何使用 WPF 工具箱控件模板创建可分发给其他用户的工具箱控件。
ms.custom: SEO-VS-2020
ms.date: 3/16/2019
ms.topic: how-to
helpviewer_keywords:
- toolbox control
- toolbox
- wpf
ms.assetid: 9cc34db9-b0d1-4951-a02f-7537fbbb51ad
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 6bf8dae61373b8a9ba5814930298896f3ba41da6
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600985"
---
# <a name="create-a-wpf-toolbox-control"></a>创建 WPF 工具箱控件

使用 WPF (Windows框架) 工具箱控件模板，可以创建在安装扩展时自动添加到工具箱的 WPF 控件。  本演练演示如何使用模板创建可分发给其他用户的工具箱控件。 

从 2015 Visual Studio开始，不会从下载Visual Studio安装 Visual Studio SDK。 它作为可选功能包含在安装程序Visual Studio中。 也可稍后安装 VS SDK。 有关详细信息，请参阅安装[Visual Studio SDK。](../extensibility/installing-the-visual-studio-sdk.md)

## <a name="create-the-toolbox-control"></a>创建工具箱控件

### <a name="create-an-extension-with-a-wpf-toolbox-control"></a>使用 WPF 工具箱控件创建扩展

1. 创建名为 的 VSIX 项目 `MyToolboxControl` 。 可以通过搜索"vsix"在"新建Project"找到 VSIX 项目模板。 

2. 项目打开时，添加名为 **的 WPF 工具箱控件** 项模板 `MyToolboxControl` 。 在“解决方案资源管理器”中，右键单击项目节点并选择“添加” > “新建项”  。 在"**添加新项"对话框中**，转到 **"Visual C#**  >  **扩展性"，** 然后选择 **"WPF 工具箱控件"。** 在 **窗口底部的**"名称"字段中，将命令文件名更改为 *MyToolboxControl.cs。*

    该解决方案现在包含一个用户控件、一个将控件添加到工具箱的 ，以及 VSIX 清单中用于部署的 `ProvideToolboxControlAttribute` <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute> **Microsoft.VisualStudio.ToolboxControl** 资产条目。 

#### <a name="to-create-the-control-ui"></a>创建控件 UI

1. 在 *设计器中打开 MyToolboxControl.xaml。*

    此设计器显示包含 <xref:System.Windows.Controls.Button> 控件的 <xref:System.Windows.Controls.Grid> 控件。

2. 排列网格布局。 选择控件时 <xref:System.Windows.Controls.Grid> ，蓝色控件条显示在网格的顶部和左边缘。 可以通过单击栏向网格添加行和列。

3. 将子控件添加到网格。 可以通过将子控件从"工具箱"拖动到网格的一部分，或在 XAML 中设置其 和 属性来定位 `Grid.Row` `Grid.Column` 子控件。 以下示例在网格顶部行添加两个标签，将按钮添加到第二行。

    ```xaml
    <Grid>
        <Label Grid.Row="0" Grid.Column="0" Name="label1" />
        <Label Grid.Row="0" Grid.Column="1" Name="label2" />
        <Button Name="button1" Click="button1_Click" Grid.Row="1" Grid.ColumnSpan="2" />
    </Grid>
    ```

## <a name="renaming-the-control"></a>重命名控件

 默认情况下，控件将在名为 **MyToolboxControl.MyToolboxControl** 的组中作为 **MyToolboxControl** 显示在"工具箱"中。 可以在 *MyToolboxControl.xaml.cs 文件中更改这些* 名称。

1. 在 *代码视图中打开 MyToolboxControl.xaml.cs。*

2. 找到 类 `MyToolboxControl` 并将其重命名为 TestControl。  (最快的方法就是重命名 类，然后从 **上下文菜单中选择** "重命名"并完成步骤。  (有关 **Rename** 命令的信息，请参阅重命名重构 ([C#)](../ide/reference/rename.md).) 

3. 转到 属性 `ProvideToolboxControl` ，将第一个参数的值更改为"测试 **"。** 这是将包含工具箱 中的 控件的组 **的名称**。

    生成的代码应如下所示：

    ```csharp
    [ProvideToolboxControl("Test", true)]
    public partial class TestControl : UserControl
    {
        public TestControl()
        {
            InitializeComponent();
        }
    }
    ```

## <a name="build-test-and-deployment"></a>生成、测试和部署

 调试项目时，应找到已安装在试验实例的"工具箱"中的控件Visual Studio。

### <a name="to-build-and-test-the-control"></a>生成并测试控件

1. 重新生成项目并开始调试。

2. 在 Visual Studio 的新实例中，创建 WPF 应用程序项目。 确保XAML 设计器打开。

3. 在“工具箱”  中查找控件，并将其拖动到设计图面上。

4. 开始调试 WPF 应用程序。

5. 验证控件是否显示。

### <a name="to-deploy-the-control"></a>部署控件

1. 生成测试的项目后，可以在项目的 *\bin\debug 文件夹中找到 *.vsix* \* 文件。

2. 可以通过双击 *.vsix* 文件并遵循安装过程，在本地计算机上安装它。 若要卸载控件，请转到"**工具** 扩展和更新"并查找控件  >  扩展，然后单击"卸载 **"。**

3. Upload *.vsix* 文件连接到网络或网站。

    如果将文件上传到 Visual Studio [Marketplace](https://marketplace.visualstudio.com/)网站，其他用户可以使用 Visual Studio 中的工具扩展和更新来联机查找并  >  安装控件。

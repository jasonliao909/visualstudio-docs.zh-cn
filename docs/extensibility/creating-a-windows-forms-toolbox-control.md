---
title: 创建Windows窗体工具箱控件|Microsoft Docs
description: 本演练演示如何使用 Windows 窗体工具箱控件模板，通过 Visual Studio SDK 创建简单的计数器控件。
ms.date: 3/16/2019
ms.topic: how-to
helpviewer_keywords:
- winforms
- toolbox
- windows forms
ms.assetid: 0be6ffc1-8afd-4d02-9a5d-e27dde05fde6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: f7937c3e78a9f9d113fa3394a7d7be948a22059e
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600988"
---
# <a name="create-a-windows-forms-toolbox-control"></a>创建Windows窗体工具箱控件

Windows扩展工具 (VS SDK) 中包含的 Visual Studio 窗体工具箱控件项模板，用于创建在安装扩展时自动添加的工具箱控件。  本演练演示如何使用模板创建可分发给其他用户的简单计数器控件。

## <a name="prerequisites"></a>先决条件

从 Visual Studio 2015 开始，不会从下载Visual Studio安装 Visual Studio SDK。 它作为可选功能包含在安装程序Visual Studio中。 也可稍后安装 VS SDK。 有关详细信息，请参阅安装[Visual Studio SDK。](../extensibility/installing-the-visual-studio-sdk.md)

## <a name="create-the-toolbox-control"></a>创建工具箱控件

"Windows窗体工具箱控件"模板创建未定义的用户控件，并提供将控件添加到工具箱 所需的 **全部功能**。

### <a name="create-an-extension-with-a-windows-forms-toolbox-control"></a>使用窗体工具箱Windows创建扩展

1. 创建名为 的 VSIX 项目 `MyWinFormsControl` 。 可以通过搜索"vsix"，在"新建Project"找到 VSIX 项目模板。

2. 项目打开时，添加名为 的Windows **工具箱控件** 项模板 `Counter` 。 在“解决方案资源管理器”中，右键单击项目节点并选择“添加” > “新建项”  。 在"**添加新项"对话框中**，转到 **"Visual C#** 扩展性"，然后选择Windows  >  **窗体工具箱控件"**

3. 这会添加用户控件、将控件放在"工具箱"中，在 VSIX 清单中添加 `ProvideToolboxControlAttribute` <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute> **Microsoft.VisualStudio.ToolboxControl** 资产条目以用于部署。 

### <a name="build-a-user-interface-for-the-control"></a>生成控件的用户界面

控件 `Counter` 需要两个子控件：用于显示当前计数的 ，以及 <xref:System.Windows.Forms.Label> 用于 <xref:System.Windows.Forms.Button> 将计数重置为 0 的 。 无需其他子控件，因为调用方将以编程方式递增计数器。

#### <a name="to-build-the-user-interface"></a>构建用户界面

1. 在 **解决方案资源管理器** 中，双击 *Counter.cs* 以在设计器中打开它。

2. 删除" **单击此处！"** 按钮，默认情况下在添加"窗体工具箱控件"Windows控件项模板时包含。

3. 从" **工具箱**"中， `Label` 将控件及其下面的 `Button` 控件拖动到设计图面。

4. 将总体用户控件的大小调整为 150、50 像素，将按钮控件的大小调整为 50、20 像素。

5. 在 **"属性** "窗口中，为设计图面上的控件设置以下值。

    |控制|属性|值|
    |-------------|--------------|-----------|
    |`Label1`|**文本**|""|
    |`Button1`|**名称**|btnReset|
    |`Button1`|**文本**|重置|

### <a name="code-the-user-control"></a>编写用户控件代码

控件将公开递增计数器的方法、每当计数器递增时要引发的事件、"重置"按钮以及用于存储当前计数的三个属性、显示文本以及显示还是隐藏"重置" `Counter` 按钮。 `ProvideToolboxControl` 特性确定 **控件会出现在“工具箱”**`Counter` 的什么位置。

#### <a name="to-code-the-user-control"></a>编写用户控件代码

1. 双击窗体，在代码窗口中打开其加载事件处理程序。

2. 在事件处理程序方法的上方，在 控件类中创建一个整数来存储计数器值，并创建一个字符串来存储显示文本，如以下示例所示。

    ```csharp
    int currentValue;
    string displayText;
    ```

3. 创建以下公共属性声明。

    ```csharp
    public int Value {
        get { return currentValue; }
    }

    public string Message {
        get { return displayText; }
        set { displayText = value; }
    }

    public bool ShowReset {
        get { return btnReset.Visible; }
        set { btnReset.Visible = value; }
    }

    ```

    调用方可以访问这些属性，获取和设置计数器的显示文本，以及显示或隐藏"重置 **"** 按钮。 调用方可以获取只读属性的当前值 `Value` ，但不能直接设置该值。

4. 将以下代码放入 `Load` 控件的 事件。

    ```csharp
    private void Counter_Load(object sender, EventArgs e)
    {
        currentValue = 0;
        label1.Text = Message + Value;
    }

    ```

    设置 **事件中的** Label <xref:System.Windows.Forms.UserControl.Load> 文本可使目标属性在应用其值之前加载。 在 **构造函数中** 设置 Label 文本将导致 **空的** Label 。

5. 创建以下公共方法以递增计数器。

    ```csharp
    public void Increment()
    {
        currentValue++;
        label1.Text = displayText + Value;
        Incremented(this, EventArgs.Empty);
    }

    ```

6. 将 事件的声明 `Incremented` 添加到 控件类。

    ```csharp
    public event EventHandler Incremented;
    ```

    调用方可以将处理程序添加到此事件，以响应计数器值的变化。

7. 返回到设计视图，然后双击"重置 **"** 按钮以生成 `btnReset_Click` 事件处理程序。 然后，按照以下示例中所示填写它。

    ```csharp
    private void btnReset_Click(object sender, EventArgs e)
    {
        currentValue = 0;
        label1.Text = displayText + Value;
    }

    ```

8. 在类定义正上方的 `ProvideToolboxControl` 特性声明中，将第一个参数的值从 `"MyWinFormsControl.Counter"` 改为 `"General"`。 这会设置将在“工具箱” 中托管控件的项组名称。

    以下示例演示了 `ProvideToolboxControl` 特性和调整后的类定义。

    ```csharp
    [ProvideToolboxControl("General", false)]
    public partial class Counter : UserControl
    ```

### <a name="test-the-control"></a>测试控件

 若要测试 **工具箱** 控件，请首先在开发环境中测试它，然后在已编译的应用程序中测试它。

#### <a name="to-test-the-control"></a>测试控件

1. 按 **F5** **开始调试**。

    此命令生成项目，并打开安装了 控件Visual Studio的第二个试验实例。

2. 在 Visual Studio 的实验实例中，Windows **窗体应用程序** 项目。

3. 在 **解决方案资源管理器** 中，双击 *Form1.cs* 以在设计器中打开它（如果尚未打开）。

4. 在 **"工具箱**" `Counter` 中，控件应显示在"常规 **"** 部分。

5. 将控件 `Counter` 拖动到窗体，然后选择它。 、 和 属性将连同从 继承的属性一起显示在"属性 `Value` `Message` `ShowReset` "窗口中 <xref:System.Windows.Forms.UserControl> 。

6. 将 `Message` 属性设置为 `Count:`。

7. 将 <xref:System.Windows.Forms.Button> 控件拖动到窗体，然后将按钮的名称和文本属性设置为 `Test` 。

8. 双击该按钮，在代码视图中打开 *Form1.cs* 并创建单击处理程序。

9. 在单击处理程序中，调用 `counter1.Increment()` 。

10. 在构造函数中，在调用 后 `InitializeComponent` 键入 ， `counter1``.``Incremented +=` 然后按 **Tab** 两次。

    Visual Studio事件生成窗体级 `counter1.Incremented` 处理程序。

11. 突出显示事件处理程序中的 语句，键入 ，然后按 Tab 两次，以从 mbox 代码片段生成 `Throw` `mbox` 消息框。 

12. 下一行添加以下 `if` / `else` 块以设置"重置"按钮 **的** 可见性。

    ```csharp
    if (counter1.Value < 5) counter1.ShowReset = false;
    else counter1.ShowReset = true;
    ```

13. 按 **F5**。

    窗体随即打开。 控件 `Counter` 显示以下文本。

    **计数：0**

14. 选择“测试”。

    计数器递增和Visual Studio显示一个消息框。

15. 关闭消息框。

    " **重置"** 按钮消失。

16. 选择 **"测试** "，直到计数器每次达到 **5** 个关闭消息框。

    " **重置"** 按钮将再次出现。

17. 选择“重置”。

    计数器重置为 **0。**

## <a name="next-steps"></a>后续步骤

生成 **工具箱控件时**，Visual Studio在项目的 \bin\debug\ 文件夹中创建名为 *ProjectName.vsix* 的文件。 可以通过将 *.vsix* 文件上传到网络或网站来部署控件。 当用户打开 *.vsix* 文件时，将安装 控件并添加到Visual Studio"工具箱"中。  或者，可以将 *.vsix* 文件上传到 Visual Studio [Marketplace，](https://marketplace.visualstudio.com/)以便用户可以通过在"工具扩展和更新"对话框中浏览找到  >  它。

## <a name="see-also"></a>另请参阅

- [扩展其他部分Visual Studio](../extensibility/extending-other-parts-of-visual-studio.md)
- [创建 WPF 工具箱控件](../extensibility/creating-a-wpf-toolbox-control.md)
- [扩展其他部分Visual Studio](../extensibility/extending-other-parts-of-visual-studio.md)
- [Windows窗体控件开发基础知识](/dotnet/framework/winforms/controls/windows-forms-control-development-basics)

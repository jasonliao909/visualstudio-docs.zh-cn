---
title: "\"创建选项\"页|Microsoft Docs"
description: 了解如何创建使用属性网格检查和设置属性的简单"工具/选项"页。
ms.custom: SEO-VS-2020
ms.date: 3/16/2019
ms.topic: how-to
helpviewer_keywords:
- Tools Options pages [Visual Studio SDK], creating
ms.assetid: 9f4e210c-4b47-4daa-91fa-1c301c4587f9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: f7ff61649cfa9c2d78256751e9c25fb0a4b670bb
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122146077"
---
# <a name="create-an-options-page"></a>"创建选项"页

本演练创建一个简单的"工具/选项"页，该页面使用属性网格来检查和设置属性。

 若要将这些属性保存到 设置文件并将其从设置文件中还原，请执行以下步骤，然后查看 [创建设置类别](../extensibility/creating-a-settings-category.md)。

 MPF 提供两个类来帮助你创建"工具选项"页 <xref:Microsoft.VisualStudio.Shell.Package> ：类和 <xref:Microsoft.VisualStudio.Shell.DialogPage> 类。 通过子类化 类，创建 VSPackage 来为这些页面提供 `Package` 容器。 通过从 类派生来创建每个工具选项 `DialogPage` 页。

## <a name="prerequisites"></a>必备条件

 从 2015 Visual Studio开始，不会从下载Visual Studio安装 Visual Studio SDK。 它作为可选功能包含在安装程序Visual Studio中。 也可稍后安装 VS SDK。 有关详细信息，请参阅安装[Visual Studio SDK。](../extensibility/installing-the-visual-studio-sdk.md)

## <a name="create-a-tools-options-grid-page"></a>"创建工具选项"网格页

 在本部分，你将创建一个简单的"工具选项"属性网格。 使用此网格可以显示和更改属性的值。

### <a name="to-create-the-vsix-project-and-add-a-vspackage"></a>创建 VSIX 项目并添加 VSPackage

1. 每个Visual Studio扩展都从 VSIX 部署项目开始，该项目将包含扩展资产。 创建名为 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 的 VSIX 项目 `MyToolsOptionsExtension` 。 可以通过搜索"vsix"在"新建Project"找到 VSIX 项目模板。 

2. 通过添加名为 的包项Visual Studio添加 `MyToolsOptionsPackage` VSPackage。 在“解决方案资源管理器”中，右键单击项目节点并选择“添加” > “新建项”  。 在"**添加新项"对话框中**，转到 **"Visual C#** 项  >  **扩展性**"，然后选择"Visual Studio **包"。** 在 **对话框** 底部的"名称"字段中，将文件名更改为 `MyToolsOptionsPackage.cs` 。 若要详细了解如何创建 VSPackage，请参阅 [使用 VSPackage 创建扩展](../extensibility/creating-an-extension-with-a-vspackage.md)。

### <a name="to-create-the-tools-options-property-grid"></a>创建"工具选项"属性网格

1. 在 *代码编辑器中打开 MyToolsOptionsPackage* 文件。

2. 添加以下 using 语句。

   ```csharp
   using System.ComponentModel;
   ```

3. 声明一 `OptionPageGrid` 个类，然后从 派生 <xref:Microsoft.VisualStudio.Shell.DialogPage> 该类。

   ```csharp
   public class OptionPageGrid : DialogPage
   {  }
   ```

4. 将 <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> 应用于 `VSPackage` 类，以向类分配 OptionPageGrid 的选项类别和选项页名称。 结果应如下所示：

    ```csharp
    [PackageRegistration(UseManagedResourcesOnly = true)]
    [InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)]
    [ProvideMenuResource("Menus.ctmenu", 1)]
    [Guid(GuidList.guidMyToolsOptionsPkgString)]
    [ProvideOptionPage(typeof(OptionPageGrid),
        "My Category", "My Grid Page", 0, 0, true)]
    public sealed class MyToolsOptionsPackage : Package
    ```

5. 将 `OptionInteger` 属性添加到 `OptionPageGrid` 类。

    - 应用 <xref:System.ComponentModel.CategoryAttribute?displayProperty=fullName> 以将属性网格类别分配给属性。

    - 应用 <xref:System.ComponentModel.DisplayNameAttribute?displayProperty=fullName> 以向属性分配名称。

    - 应用 <xref:System.ComponentModel.DescriptionAttribute?displayProperty=fullName> 以向属性分配说明。

    ```csharp
    public class OptionPageGrid : DialogPage
    {
        private int optionInt = 256;

        [Category("My Category")]
        [DisplayName("My Integer Option")]
        [Description("My integer option")]
        public int OptionInteger
        {
            get { return optionInt; }
            set { optionInt = value; }
        }
    }
    ```

    > [!NOTE]
    > 的默认实现支持具有适当转换器的属性，或者具有可扩展为具有适当转换器的属性 <xref:Microsoft.VisualStudio.Shell.DialogPage> 的结构或数组的属性。 有关转换器的列表，请参阅 <xref:System.ComponentModel> 命名空间。

6. 生成项目并启动调试。

7. 在 Visual Studio 实验实例中，单击"**工具"菜单** 上的"选项 **"。**

     在左窗格中，应会看到"我的 **类别"。**  (选项类别按字母顺序列出，因此它应出现在列表的大约一半。) **打开"** 我的类别"，然后单击"我的 **网格页"。** 选项网格显示在右窗格中。 属性类别为 **"我的选项"，** 属性名称为"**我的整数选项"。** 属性说明" **我的整数"** 选项显示在窗格底部。 将值从初始值 256 更改为其他值。 单击 **"确定**"，然后重新打开"**我的网格页"。** 可以看到新值仍然存在。

     也可通过搜索框Visual Studio选项页。 在 IDE 顶部附近的搜索框中，键入"我的类别"，你将看到结果 **>"我的网格** 页"。

## <a name="create-a-tools-options-custom-page"></a>"创建工具""选项"自定义页

 在本部分，你将使用自定义 UI 创建"工具选项"页。 使用此页可以显示和更改属性的值。

1. 在 *代码编辑器中打开 MyToolsOptionsPackage* 文件。

2. 添加以下 using 语句。

    ```csharp
    using System.Windows.Forms;
    ```

3. 添加 `OptionPageCustom` 类，就在 类 `OptionPageGrid` 之前。 从 派生新类 `DialogPage` 。

    ```csharp
    public class OptionPageCustom : DialogPage
    {
        private string optionValue = "alpha";

        public string OptionString
        {
            get { return optionValue; }
            set { optionValue = value; }
        }
    }
    ```

4. 添加 GUID 属性。 添加 OptionString 属性：

    ```csharp
    [Guid("00000000-0000-0000-0000-000000000000")]
    public class OptionPageCustom : DialogPage
    {
        private string optionValue = "alpha";

        public string OptionString
        {
            get { return optionValue; }
            set { optionValue = value; }
        }
    }
    ```

5. 将第二 <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> 个 应用于 VSPackage 类。 此属性为类分配选项类别和选项页名称。

    ```csharp
    [PackageRegistration(UseManagedResourcesOnly = true)]
    [InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)]
    [ProvideMenuResource("Menus.ctmenu", 1)]
    [Guid(GuidList.guidMyToolsOptionsPkgString)]
    [ProvideOptionPage(typeof(OptionPageGrid),
        "My Category", "My Grid Page", 0, 0, true)]
    [ProvideOptionPage(typeof(OptionPageCustom),
        "My Category", "My Custom Page", 0, 0, true)]
    public sealed class MyToolsOptionsPackage : Package
    ```

6. 将名为MyUserControl 的新用户控件添加到项目。

7. 向 **用户控件添加 TextBox** 控件。

     在" **属性** "窗口中的工具栏上，单击" **事件** "按钮，然后双击" **离开"** 事件。 新的事件处理程序显示在 *MyUserControl.cs* 代码中。

8. 将公共 `OptionsPage` 字段、方法添加到控件类，并更新事件处理程序以将选项值设置为 `Initialize` 文本框的内容：

    ```csharp
    public partial class MyUserControl : UserControl
    {
        public MyUserControl()
        {
            InitializeComponent();
        }

        internal OptionPageCustom optionsPage;

        public void Initialize()
        {
            textBox1.Text = optionsPage.OptionString;
        }

        private void textBox1_Leave(object sender, EventArgs e)
        {
            optionsPage.OptionString = textBox1.Text;
        }
    }
    ```

     `optionsPage`字段保存对父实例 `OptionPageCustom` 的引用。 方法 `Initialize` 显示在 `OptionString` **TextBox 中**。 当焦点离开 TextBox 时，事件处理程序会将 **TextBox** `OptionString` 的当前值 **写入**。

9. 在包代码文件中，将 属性的重写添加到 类， `OptionPageCustom.Window` `OptionPageCustom` 以创建、初始化和返回 的实例 `MyUserControl` 。 类现在应如下所示：

    ```csharp
    [Guid("00000000-0000-0000-0000-000000000000")]
    public class OptionPageCustom : DialogPage
    {
        private string optionValue = "alpha";

        public string OptionString
        {
            get { return optionValue; }
            set { optionValue = value; }
        }

        protected override IWin32Window Window
        {
            get
            {
                MyUserControl page = new MyUserControl();
                page.optionsPage = this;
                page.Initialize();
                return page;
            }
        }
    }
    ```

10. 生成并运行该项目。

11. 在实验实例中，单击"**工具选项**  >  **"。**

12. 找到 **"我的类别**"，然后 **找到"我的自定义页"。**

13. 更改 **OptionString 的值**。 单击 **"确定**"，然后重新打开 **"我的自定义页"。** 可以看到新值已持久化。

## <a name="access-options"></a>访问选项

 在本部分，你将从托管关联工具选项页的 VSPackage 获取选项的值。 同一技术可用于获取任何公共属性的值。

1. 在包代码文件中，将名为 **OptionInteger** 的公共属性添加到 **MyToolsOptionsPackage** 类。

    ```csharp
    public int OptionInteger
    {
        get
        {
            OptionPageGrid page = (OptionPageGrid)GetDialogPage(typeof(OptionPageGrid));
            return page.OptionInteger;
        }
    }

    ```

     此代码 <xref:Microsoft.VisualStudio.Shell.Package.GetDialogPage%2A> 调用 来创建或检索 `OptionPageGrid` 实例。 `OptionPageGrid` 调用 <xref:Microsoft.VisualStudio.Shell.DialogPage.LoadSettingsFromStorage%2A> 以加载其选项，即公共属性。

2. 现在，添加名为 **MyToolsOptionsCommand** 的自定义命令项模板以显示值。 在"**添加新项"对话框中**，转到 **"Visual C#**  >  **扩展性"，** 然后选择"**自定义命令"。** 在 **窗口底部的** "名称"字段中，将命令文件名更改为 *MyToolsOptionsCommand.cs*。

3. 在 *MyToolsOptionsCommand* 文件中，将命令的 方法的正文 `ShowMessageBox` 替换为以下内容：

    ```csharp
    private void ShowMessageBox(object sender, EventArgs e)
    {
        MyToolsOptionsPackage myToolsOptionsPackage = this.package as MyToolsOptionsPackage;
        System.Windows.Forms.MessageBox.Show(string.Format(CultureInfo.CurrentCulture, "OptionInteger: {0}", myToolsOptionsPackage.OptionInteger));
    }

    ```

4. 生成项目并启动调试。

5. 在实验实例的"工具"**菜单上**，单击"**调用 MyToolsOptionsCommand"。**

     消息框显示 的当前值 `OptionInteger` 。

## <a name="see-also"></a>请参阅

- ["选项"和"选项"页](../extensibility/internals/options-and-options-pages.md)

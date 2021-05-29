---
title: 创建设置类别 |Microsoft Docs
description: 了解如何创建 Visual Studio 设置类别并使用它来保存和还原设置文件中的值。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- profile settings, creating categories
ms.assetid: 97c88693-05ff-499e-8c43-352ee073dcb7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: fe46ea835a119978fd3decd26949db3d59944e5e
ms.sourcegitcommit: 63cb90e8cea112aa2ce8741101b309dbc709e393
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2021
ms.locfileid: "110687615"
---
# <a name="create-a-settings-category"></a>创建设置类别

在本演练中，您将创建一个 Visual Studio 设置类别，并使用它将值保存到并从设置文件还原值。 设置类别是一组显示为 "自定义设置点" 的相关属性;即 **导入和导出设置** 向导中的复选框。  (你可以在 " **工具** " 菜单上找到它。 ) 设置保存或还原为类别，并且不会在向导中显示各个设置。 有关详细信息，请参阅[环境设置](../ide/environment-settings.md)。

您可以通过从类中派生来创建设置类别 <xref:Microsoft.VisualStudio.Shell.DialogPage> 。

若要开始本演练，必须先完成 " [创建选项" 页面](../extensibility/creating-an-options-page.md)的第一个部分。 "生成的选项" 属性网格使你可以检查和更改类别中的属性。 将属性类别保存到设置文件中后，将检查该文件以查看属性值的存储方式。

## <a name="prerequisites"></a>先决条件
 从 Visual Studio 2015 开始，你不需要从下载中心安装 Visual Studio SDK。 它作为 Visual Studio 安装程序中的可选功能提供。 也可稍后安装 VS SDK。 有关详细信息，请参阅 [安装 Visual STUDIO SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-settings-category"></a>创建设置类别
 在本部分中，将使用自定义设置点保存和还原 "设置" 类别的值。

### <a name="to-create-a-settings-category"></a>创建设置类别

1. 完成 " [创建选项" 页](../extensibility/creating-an-options-page.md)。

2. 打开 *VSPackage* 文件并添加以下三个字符串资源：

    |名称|值|
    |----------|-----------|
    |106|我的类别|
    |107|我的设置|
    |108|OptionInteger 和 OptionFloat|

     这会创建将类别"My Category"、对象"My Settings"和类别描述"OptionInteger and OptionFloat"命名的资源。

    > [!NOTE]
    > 在这三个向导中，只有类别名称不会出现在" **导入和导出设置"** 向导中。

3. 在 *MyToolsOptionsPackage.cs* 中，将名为 的属性添加到 `float` `OptionFloat` `OptionPageGrid` 类，如以下示例所示。

    ```csharp
    public class OptionPageGrid : DialogPage
    {
        private int optionInt = 256;
        private float optionFloat = 3.14F;

        [Category("My Options")]
        [DisplayName("My Integer option")]
        [Description("My integer option")]
        public int OptionInteger
        {
            get { return optionInt; }
            set { optionInt = value; }
        }
        [Category("My Options")]
        [DisplayName("My Float option")]
        [Description("My float option")]
        public float OptionFloat
        {
            get { return optionFloat; }
            set { optionFloat = value; }
        }
    }
    ```

    > [!NOTE]
    > 名为 `OptionPageGrid` "My Category"的类别现在由两个属性 `OptionInteger` 和 组成 `OptionFloat` 。

4. 将 添加到 类，并赋予 <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> `MyToolsOptionsPackage` CategoryName"My Category"，为它指定 ObjectName"My Settings"，将 isToolsOptionPage 设置为 true。 将 categoryResourceID、objectNameResourceID 和 DescriptionResourceID 设置为前面创建的相应字符串资源 ID。

    ```csharp
    [ProvideProfileAttribute(typeof(OptionPageGrid),
        "My Category", "My Settings", 106, 107, isToolsOptionPage:true, DescriptionResourceID = 108)]
    ```

5. 生成项目并启动调试。 在实验实例中，应会看到" **我的网格页** "现在同时具有整数和浮点数值。

## <a name="examine-the-settings-file"></a>检查设置文件
 在本部分，你将属性类别值导出到设置文件。 检查文件，然后将值导入回属性类别。

1. 按 F5 在调试模式下 **启动项目**。 这会启动实验实例。

2. 打开"**工具**  >  **选项"** 对话框。

3. 在左窗格中的树视图中，展开"**我的类别"，** 然后单击"**我的网格页"。**

4. 将 **OptionFloat** 的值更改为 3.1416，将 **OptionInteger** 的值更改为 12。 单击 **“确定”** 。

5. 在“工具”菜单上，单击“导入和导出设置”。

     将显示 **"导入和导出设置"** 向导。

6. 确保已 **选择"导出所选环境设置**"，然后单击"下一 **步"。**

     将显示 **"选择要导出的设置"** 页。

7. 单击 **"我的设置"。**

     " **说明"** 将更改到 **OptionInteger 和 OptionFloat**。

8. 请确保 " **我的设置** " 是所选的唯一类别，然后单击 " **下一步**"。

     显示 **设置文件** 页的名称。

9. 将新的设置文件命名为 *mysetting* ，并将其保存到相应的目录中。 单击“完成”  。

   `.vssettings`文件是 Visual Studio 设置文件。 已打开文件的架构。 最常见的情况是，架构遵循一个 XML 结构，其中每个类别都是一个标记，它本身就包含子类别标记。 这些子类别标记可以包含属性值标记。 尽管大多数包都使用 common 结构，但 Visual Studio 中的任何包都可以使用它选择的架构向文件提供任意 XML。

   " **导出完成** " 页将报告你的设置已成功导出。

10. 在“文件”菜单中，指向“打开”，再单击“文件”。 找到 *mysetting .vssettings* 并将其打开。

     你可以在文件的以下部分中找到导出的属性类别 (你的 Guid 将) 不同。

    ```
    <Category name="My Category_My Settings"
          Category="{4802bc3e-3d9d-4591-8201-23d1a05216a6}"
          Package="{6bb6942e-014c-489e-a612-a935680f703d}"
          RegisteredName="My Category_My Settings">
          PackageName="MyToolsOptionsPackage">
       <PropertyValue name="OptionFloat">3.1416</PropertyValue>
       <PropertyValue name="OptionInteger">12</PropertyValue>
    </Category>
    ```

     请注意，通过将下划线添加到类别名称后接对象名称，来形成完整的类别名称。 "OptionFloat" 和 "OptionInteger" 显示在 "类别" 中，及其导出值。

11. 关闭设置文件而不进行更改。

12. 在 " **工具** " 菜单上，依次单击 " **选项**"、 **"我的类别**"、" **我的网格" 页** ，然后将 **OptionFloat** 的值更改为1.0，并将 **OptionInteger** 更改为1。 单击 **“确定”** 。

13. 单击 " **工具** " 菜单上的 " **导入和导出设置**"，选择 " **导入选定的环境设置**"，然后单击 " **下一步**"

     此时将显示 " **保存当前设置** " 页。

14. 选择 **"否，仅导入新设置"** ，然后单击 " **下一步**"。

     此时将显示 " **选择要导入的设置集合** " 页。

15. 在树视图的 "**我的设置**" 节点中选择 " *mysetting" .vssettings* 文件。 如果文件未显示在树视图中， **请单击"浏览** "并找到它。 单击“下一步”  。

     将出现 **"选择要导入的设置** "对话框。

16. 确保选中"**我的设置**"，然后单击"完成 **"。** 当"**导入完成"** 页出现时，单击"关闭 **"。**

17. 在"**工具"** 菜单上，单击"选项 **"，展开****"我的类别**"，单击"**我的网格** 页"，并验证属性类别值是否已还原。

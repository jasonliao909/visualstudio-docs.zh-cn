---
title: 创建设置类别|Microsoft Docs
description: 了解如何创建一个Visual Studio设置类别，并使用它从设置文件中保存和还原值。
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

本演练将创建一Visual Studio设置类别，并使用它将值保存到设置文件中并还原设置文件的值。 设置类别是显示为"自定义设置点"的相关属性组;即，作为"导入和导出设置"向导 **中的** 复选框。  (可以在"工具"菜单上找到它。) 将"设置"保存或还原为类别，并且向导中不显示单个设置。  有关详细信息，请参阅[环境设置](../ide/environment-settings.md)。

通过从 类派生设置类别来创建 <xref:Microsoft.VisualStudio.Shell.DialogPage> 设置类别。

若要开始本演练，必须先完成"创建选项"页 [的第一部分](../extensibility/creating-an-options-page.md)。 生成的"选项"属性网格可用于检查和更改类别中的属性。 在设置文件中保存属性类别后，检查该文件以查看属性值是如何存储的。

## <a name="prerequisites"></a>先决条件
 从 2015 Visual Studio开始，不会从下载Visual Studio安装 Visual Studio SDK。 它作为可选功能包含在安装程序Visual Studio中。 也可稍后安装 VS SDK。 有关详细信息，请参阅安装[Visual Studio SDK。](../extensibility/installing-the-visual-studio-sdk.md)

## <a name="create-a-settings-category"></a>创建设置类别
 在本部分，你将使用自定义设置点保存和还原设置类别的值。

### <a name="to-create-a-settings-category"></a>创建设置类别

1. 完成" [创建选项"页](../extensibility/creating-an-options-page.md)。

2. 打开 *VSPackage.resx* 文件并添加以下三个字符串资源：

    |名称|值|
    |----------|-----------|
    |106|我的类别|
    |107|我的设置|
    |108|OptionInteger 和 OptionFloat|

     这会创建将类别命名为 "我的类别"、对象 "我的设置" 和类别说明 "OptionInteger and OptionFloat" 的资源。

    > [!NOTE]
    > 在这三种情况下，" **导入和导出设置** 向导" 中将不显示类别名称。

3. 在 *MyToolsOptionsPackage* 中，将一个 `float` 名为的属性添加 `OptionFloat` 到 `OptionPageGrid` 类，如下面的示例中所示。

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
    > `OptionPageGrid`名为 "My category" 的类别现在包含两个属性，即 `OptionInteger` 和 `OptionFloat` 。

4. 将添加 <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> 到 `MyToolsOptionsPackage` 类，并将其命名为 "my Category"，为其指定 ObjectName "my Settings"，并将 isToolsOptionPage 设置为 true。 将 categoryResourceID、objectNameResourceID 和 DescriptionResourceID 设置为前面创建的相应字符串资源 Id。

    ```csharp
    [ProvideProfileAttribute(typeof(OptionPageGrid),
        "My Category", "My Settings", 106, 107, isToolsOptionPage:true, DescriptionResourceID = 108)]
    ```

5. 生成项目并启动调试。 在实验实例中，应会看到 **"我的网格" 页** 现在包含整数值和浮点值。

## <a name="examine-the-settings-file"></a>检查设置文件
 在本部分中，将属性类别值导出到设置文件。 检查该文件，然后将这些值导入回属性类别。

1. 通过按 **F5** 在调试模式下启动项目。 这将启动实验实例。

2. 打开 "**工具**  >  **选项**" 对话框。

3. 在左侧窗格中的树视图中，展开 **"我的类别** "，然后单击 **"我的网格" 页**。

4. 将 **OptionFloat** 的值更改为3.1416，将 **OptionInteger** 更改为12。 单击 **“确定”** 。

5. 在“工具”菜单上，单击“导入和导出设置”。

     此时将显示 **导入和导出设置** 向导。

6. 确保选中 " **导出所选环境设置** "，然后单击 " **下一步**"。

     此时将显示 " **选择要导出的设置** " 页。

7. 单击 **"我的设置"**。

     **说明** 更改为 " **OptionInteger" 和 "OptionFloat**"。

8. 确保"**我的设置**"是唯一选择的类别，然后单击"下一步 **"。**

     将显示 **"命名设置文件** "页。

9. 将新设置文件命名 *MySettings.vssettings，* 并将其保存到相应的目录中。 单击“完成”  。

   该文件 `.vssettings` 是Visual Studio文件。 文件的架构已打开。 大多数情况下，架构遵循 XML 结构，其中每个类别都是标记，该标记本身可以包含子类别标记。 这些子类别标记可以包含属性值标记。 虽然大多数包都使用通用结构，但Visual Studio包都可以使用它选择的架构向文件提供任意 XML。

   " **导出完成** "页报告已成功导出设置。

10. 在“文件”菜单中，指向“打开”，再单击“文件”。 找到 *MySettings.vssettings* 并打开它。

     可以在文件的以下部分找到导出的属性类别， (GUID 将因) 。

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

     请注意，完整的类别名称由向类别名称添加下划线后跟对象名称构成。 OptionFloat 和 OptionInteger 及其导出值一起显示在类别中。

11. 关闭设置文件而不更改该文件。

12. 在"**工具"** 菜单上，单击"选项"，展开"**我的** 类别"，单击"**我的网格** 页"，然后将 **OptionFloat** 的值更改为 1.0，将 **OptionInteger** 的值更改为 1。 单击 **“确定”** 。

13. 在"**工具"** 菜单上，单击 **"导入和导出设置"，** 选择 **"导入所选环境设置**"，然后单击"下一 **步"。**

     将显示 **"保存当前设置"** 页。

14. 选择 **"否"，只需导入新设置，** 然后单击"下一 **步"。**

     将显示 **"选择要导入的设置的集合"** 页。

15. 在 *树视图的"我的设置"节点中选择 MySettings.vssettings* 文件。  如果该文件未出现在树视图中，请单击 " **浏览** " 并找到该文件。 单击“下一步”  。

     此时将显示 " **选择要导入的设置** " 对话框。

16. 请确保选择 **"我的设置** "，然后单击 " **完成**"。 出现 " **导入完成** " 页后，单击 " **关闭**"。

17. 在 " **工具** " 菜单上，依次单击 " **选项**"、 **"我的类别**"、" **我的网格页** " 和 "验证属性类别值已还原"。

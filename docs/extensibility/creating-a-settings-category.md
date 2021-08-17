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
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: bbdc247e11930f05649b8e7b3c9d6d4cb1740aab
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122043708"
---
# <a name="create-a-settings-category"></a>创建设置类别

本演练将创建一Visual Studio设置类别，并使用它将值保存到设置文件中，然后从设置文件中还原值。 设置类别是显示为"自定义设置点"的相关属性组;即，作为导入和导出 **向导中的设置** 复选框。  (可以在"工具"菜单上找到它。) 设置保存或还原为类别，并且向导中不显示单个设置。  有关详细信息，请参阅[环境设置](../ide/environment-settings.md)。

通过从 类派生设置类别来创建 <xref:Microsoft.VisualStudio.Shell.DialogPage> 设置类别。

若要开始本演练，必须先完成"创建选项"页 [的第一部分](../extensibility/creating-an-options-page.md)。 生成的"选项"属性网格可用于检查和更改类别中的属性。 在设置文件中保存属性类别后，检查该文件以查看属性值是如何存储的。

## <a name="prerequisites"></a>必备条件
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

     这会创建将类别"My Category"、对象"My 设置"和类别描述"OptionInteger and OptionFloat"的资源。

    > [!NOTE]
    > 在这三个向导中，只有类别名称不会出现在"导入和导出 **设置向导中**。

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

4. 将 添加到 类，并赋予 <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> `MyToolsOptionsPackage` CategoryName"My Category"，赋予 ObjectName"My 设置"，将 isToolsOptionPage 设置为 true。 将 categoryResourceID、objectNameResourceID 和 DescriptionResourceID 设置为前面创建的相应字符串资源 ID。

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

4. 将 **OptionFloat** 的值更改为 3.1416，将 **OptionInteger** 的值更改为 12。 单击“确定”。

5. 在“工具”菜单上，单击“导入和导出设置”。

     将显示 **"导入和导出设置** 向导。

6. 确保已 **选择"导出所选环境设置**"，然后单击"下一 **步"。**

     将显示 **"设置导出"** 页。

7. 单击 **"我的设置"。**

     " **说明"** 将更改到 **OptionInteger 和 OptionFloat**。

8. 确保"**我的设置** 是唯一选择的类别，然后单击"下一步 **"。**

     将显示 **"命名设置文件**"页。

9. 将新设置文件命名 *为 MySettings.vssettings，* 并将其保存到相应的目录中。 单击“完成”。

   该文件 `.vssettings` 是Visual Studio文件。 文件的架构是开放的。 大多数情况下，架构遵循 XML 结构，其中每个类别都是一个标记，该标记本身可以包含子类别标记。 这些子类别标记可以包含属性值标记。 虽然大多数包都使用相同结构，但 Visual Studio 中的包都可以使用它选择的架构向文件提供任意 XML。

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

12. 在"**工具"** 菜单上，单击"选项"，展开"**我的类别**"，单击"**我的网格** 页"，然后将 **OptionFloat** 的值更改为 1.0，将 **OptionInteger** 的值更改为 1。 单击“确定”。

13. 在"**工具"** 菜单上，单击"导入 **和导出设置，** 选择 **"导入所选环境设置**"，然后单击"下一 **步"。**

     将显示 **"保存当前设置** 页。

14. 选择 **"否"，只需导入新设置，** 然后单击"下一 **步"。**

     将显示 **"选择要导入设置集合**"页。

15. 在树视图的"My 设置"**节点** 中选择 *MySettings.vssettings* 文件。 如果文件未显示在树视图中， **请单击"浏览** "并找到它。 单击“下一步”。

     将出现 **"设置导入**"对话框。

16. 确保选中"**我的设置"，** 然后单击"完成 **"。** 当"**导入完成"** 页出现时，单击"关闭 **"。**

17. 在"**工具"** 菜单上，单击"选项 **"，展开****"我的类别**"，单击"**我的网格** 页"，并验证属性类别值是否已还原。
